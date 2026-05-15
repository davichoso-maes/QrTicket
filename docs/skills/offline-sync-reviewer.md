---
name: offline-sync-reviewer
description: >
  Revisa y endurece el código de sincronización offline-first de la app de
  guardias (SQLite local ↔ PostgreSQL central), enforce las reglas BR-F-008
  (sólo eventos asignados), BR-F-010 (sin pérdida de evidencia) y NFR-004
  (sync `>= 95%`). Cubre FSD-UC-007 (descarga) y FSD-UC-009 (validación
  offline + reconciliación). Alineada a ADR-0003 y ADR-0006.
allowed-tools:
  - read
  - edit
  - run-tests
model-tier: sonnet
fsd-version-min: v0.1
status: stable
owner: mobile / guardias — QrTicket
---

# Skill: `offline-sync-reviewer` — revisor de sync SQLite ↔ Postgres

> Skill de dominio crítica para QrTicket. La operación offline es uno de los
> pilares del producto (AGENTS.md §4.3). Activarla siempre que se modifique
> código de sync o el dataset offline.

## 1. Cuándo activarla (triggers)

- DURANTE: cambios en `mobile/access/sync/*`, `domain/access/OfflineSnapshot*`, `api/access/sync/*`.
- ARRANCA cuando: el usuario invoca `"@offline-sync-reviewer <ruta>"` o abre un PR que toque la cadena de sync.
- NO ACTIVAR cuando: el cambio es puramente UI de la app de guardias sin tocar SQLite ni endpoints de sync.

## 2. Entradas obligatorias (Inputs)

El usuario MUST proporcionar:

- Ruta(s) al diff o archivos modificados.
- UC objetivo (`FSD-UC-007`, `FSD-UC-009`).
- Versión de sync esperada (`sync_version` monótona).
- Estrategia de reconciliación declarada (last-writer-wins, append-only logs, etc.).

Si falta cualquiera, responder: `"Necesito el diff + UC + sync_version + estrategia de reconciliación."`

## 3. Fuentes de verdad (orden de precedencia)

1. ADR-0003 (`docs/adr/0003-sqlite-offline-first-guardias.md`) — uso de SQLite y estrategia.
2. ADR-0006 (`docs/adr/0006-sync-incremental-y-reconciliacion.md`) — incremental + reconciliación.
3. FSD §4 UC-007 y UC-009.
4. FSD §5 BR-F-008, BR-F-009, BR-F-010.
5. FSD §10 NFR-004 (`>= 95%` sync exitoso) y NFR-008 (throughput).
6. `AGENTS.md` §16 (offline first).

## 4. Procedimiento

1. **RBAC en sync (BR-F-008)**: el endpoint `/sync` debe filtrar por `guard_assignments` activos del usuario. Cualquier `eventId` sin asignación → `403 Forbidden`.
2. **Versionado monótono**: `sync_version` debe ser monotónica (timestamp + secuencia o ULID). Nunca permitir downgrade.
3. **Incremental**: si el cliente envía `since=<sync_version>`, el servidor responde **delta**, no full snapshot. Snapshot completo sólo si `since == null` o `gap > threshold`.
4. **Idempotencia del upload de escaneos**: `(ticket_id, mode=offline, scanned_at)` como clave natural para deduplicar lotes reenviados.
5. **Resolución de conflictos**:
   - Si local marcó `used` y server ya tenía `used` por otro guardia → marcar `conflict` y crear incidencia (no borrar el primer log).
   - Nunca sobrescribir un `used` con `active`.
6. **Marca de parcialidad**: si hay validaciones pendientes de sync, los reportes (UC-010) deben mostrar `syncWarning` (BR-F-011).
7. **Pruebas obligatorias**:
   - sync offline → reconexión → reconciliación sin pérdida.
   - doble escaneo offline (mismo guardia) → uno aplicado, segundo `used`.
   - escaneo offline en 2 dispositivos → 1 aplicado, 1 marcado `conflict`.
   - dataset stale (`sync_version` muy antigua) → forzar full snapshot.

## 5. Salida esperada

- Comentarios en PR estructurados como `[BR-F-NNN]`, `[NFR-004]`, `[ADR-0006]`.
- Diff sugerido cuando se detecte violación.
- Tabla de hallazgos al final del review:

| Severidad | Ruta:linea | Regla violada | Acción sugerida |
|-----------|------------|----------------|------------------|
| crítica | `api/access/sync.ts:42` | BR-F-008 (sin filtro de assignments) | añadir `WHERE guard_user_id = :userId` |
| media | `mobile/.../syncQueue.ts:88` | NFR-004 (sin retry idempotente) | añadir backoff y clave natural |

## 6. Verificación (criterios de "bien hecho")

- Cero acceso cross-evento sin assignment activo.
- Reconciliación pasa 4 escenarios de prueba (single-guard happy, doble offline, dual-device, dataset stale).
- Throughput de sync `>= 50 scans/min/puerta` validado en NFR-008 (stress test).
- Logs de auditoría con `mode = offline | reconciled` siempre presentes.
- Tasa de éxito de sync `>= 95%` medida en logs de los últimos 7 días previos al release.

## 7. Anti-patrones específicos del dominio

- **Full snapshot en cada sync** → mata batería del guardia y NFR-008.
- **Borrar `scan_pending` antes de confirmar reconciliación server-side**.
- **Last-writer-wins ciego** sobre `tickets.status = used` → puede revertir un acceso ya marcado por otro guardia.
- **Permitir login del guardia y descarga sin assignment** → fuga de tickets de eventos ajenos.
- **No mostrar `syncWarning` en reportes con datos parciales** → el organizador toma decisiones con datos incompletos.
- **Resolver el conflicto borrando el primer log** — viola BR-F-010 ("nunca se descarta evidencia").

## 8. Mini ejemplo de invocación

> "@offline-sync-reviewer revisa el diff de PR #42 contra `mobile/access/syncQueue.ts` y `api/access/sync.ts`. UC: FSD-UC-009. Estrategia: append-only + conflict markers."

## 9. Modos de fallo conocidos

- El cliente envía lotes sin `sync_version` → STOP, devolver `400` y pedir el header.
- El reloj del dispositivo está desincronizado → usar `received_at` del server como ground truth, no `scanned_at` del cliente.
- Backend recibe lote enorme (`>10k` escaneos) — procesar en chunks con savepoints transaccionales.

## 10. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 0.1.0 | 2026-05-13 | Equipo QrTicket | versión inicial |
