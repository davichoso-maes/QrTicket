---
name: qr-token-author
description: >
  Genera y valida el token QR firmado server-side de QrTicket de forma
  consistente con BR-F-006 ("todo ticket emitido debe tener un token QR único
  y verificable"). Cubre emisión (FSD-UC-005), validación online (FSD-UC-008),
  validación offline (FSD-UC-009) y respeta el ADR-0004 (QR dinámico firmado).
  Activar cuando se edite cualquier módulo que produzca, persista o verifique
  un `qr_token` de la entidad `tickets`.
allowed-tools:
  - read
  - edit
  - run-tests
model-tier: sonnet
fsd-version-min: v0.1
status: stable
owner: backend / security — QrTicket
---

# Skill: `qr-token-author` — generador y validador del QR firmado de QrTicket

> Skill de dominio del producto. Para activarla en Claude Code, copiar a
> `.claude/skills/qr-token-author/SKILL.md` en el repo del grupo o a
> `~/.claude/skills/qr-token-author/` para alcance global.

## 1. Cuándo activarla (triggers)

- DURANTE: implementación o revisión de los módulos `tickets`, `access` o `payments` que toquen `qr_token`.
- ARRANCA cuando: el usuario invoca `"@qr-token-author <acción>"` o edita archivos en `infra/tickets/qr/*` o `domain/tickets/QrToken*`.
- NO ACTIVAR cuando: el código sólo lee `tickets.id` sin involucrar el token QR (p. ej. listado en dashboard).

## 2. Entradas obligatorias (Inputs)

El usuario MUST proporcionar al menos una de:

- Ruta al UC que justifica el cambio (`FSD-UC-005`, `FSD-UC-008`, `FSD-UC-009`).
- Operación deseada: `emit | verify | revoke`.
- Algoritmo de firma autorizado por ADR-0004 (por defecto `HS256` con secret rotado).
- Política de TTL si el token es dinámico (default: TTL `<= 5 min` para QR de pago, sin TTL para QR de ticket emitido).

Si falta cualquiera, responder: `"Necesito el UC objetivo y la operación (emit/verify/revoke) antes de tocar qr_token."`

## 3. Fuentes de verdad (orden de precedencia)

1. ADR-0004 (`docs/adr/0004-qr-dinamico-firmado-server-side.md`) — algoritmo, rotación, anti-replay.
2. FSD §4 (UC-005, UC-008, UC-009) — contratos y reglas de uso.
3. FSD §5 BR-F-006/007 — invariantes de unicidad y reuso.
4. FSD §10 NFR-005/006 — cifrado y antifraude cuantificable.
5. `AGENTS.md` §17/§18 — seguridad y antifraude.

## 4. Procedimiento

1. **Definir payload mínimo del token**: `{ ticketId, eventId, organizationId, ticketTypeId, iat, exp?, nonce }`.
   - Nunca incluir PII del comprador en el payload.
2. **Firma**: HMAC con secret server-side gestionado en KMS/Secrets Manager; rotación documentada.
3. **Persistencia**: guardar `qr_token` en `tickets.qr_token` con índice único; nunca regenerar si ya está emitido.
4. **Verificación**:
   - validar firma → si falla → `E_QR_INVALID`.
   - validar `eventId` coincide con escaneo → si no → `E_WRONG_EVENT`.
   - validar `tickets.status == active` → si `used` → `E_TICKET_USED`.
   - si `exp` presente y vencido → `E_QR_EXPIRED`.
5. **Anti-replay offline**: marcar el ticket como `used` localmente y reconciliar (UC-009); ningún escaneo offline se descarta.
6. **Auditoría**: cada `emit/verify` produce `access_logs` con `result` y `mode` (BR-F-009).

## 5. Salida esperada

- Funciones puras `QrToken.emit(payload)`, `QrToken.verify(token, ctx)`.
- Tests asociados con tag `FSD-UC-005`, `FSD-UC-008`, `FSD-UC-009`.
- Diff propuesto a ADR-0004 si el algoritmo cambia o si se introduce un nuevo failure mode.
- Tabla de cobertura al cerrar el PR:

| Operación | Función | Test | Failure modes cubiertos |
|-----------|---------|------|-------------------------|
| emit | `QrToken.emit` | `qrtoken.emit.spec.ts` | `E_TICKET_NOT_FOUND` |
| verify | `QrToken.verify` | `qrtoken.verify.spec.ts` | `E_QR_INVALID`, `E_TICKET_USED`, `E_WRONG_EVENT`, `E_QR_EXPIRED` |

## 6. Verificación (criterios de "bien hecho")

- `qr_token` cumple unicidad a nivel de DB (constraint + índice).
- Verificación server-side rechaza tokens manipulados (firma rota) **antes** de cualquier query a `tickets`.
- Anti-replay: una segunda llamada con el mismo token sobre un ticket `active` lo marca `used`; una tercera devuelve `E_TICKET_USED`.
- Cobertura de tests `>= 90%` para `domain/tickets/QrToken`.
- Logs de auditoría se generan **siempre**, exitosos o fallidos (BR-F-009).

## 7. Anti-patrones específicos del dominio

- **QR como JSON plano en base64** sin firma → falla en NFR-005 y NFR-006.
- **Incluir PII en el payload** (nombre completo, email) — el QR es público en pantalla.
- **Verificar primero por DB y después por firma** — invertir el orden filtra info a atacantes.
- **Generar QR distinto cada vez para el mismo ticket emitido** sin razón operativa — rompe casos offline (UC-009).
- **Reusar el mismo secret entre tenants** — viola aislamiento multi-tenant (BR-F-012).
- **Borrar `access_logs` al reconciliar conflictos** — viola BR-F-010.

## 8. Mini ejemplo de invocación

> "@qr-token-author emit. UC: FSD-UC-005. Algoritmo: HS256. TTL: ninguno (ticket emitido permanente hasta `used`). Genera la función `QrToken.emit`, persistencia y test que verifique unicidad y rechazo de duplicados."

## 9. Modos de fallo conocidos

- ADR-0004 no fija aún proveedor de secrets → STOP, pedir cierre del ADR.
- El UC pide TTL pero el frontend mostrará el QR > TTL → STOP, reabrir UC.
- Conflicto con `payments` (referencia QR de pago vs token de ticket) — son entidades distintas; no compartir secret ni función.

## 10. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 0.1.0 | 2026-05-13 | Equipo QrTicket | versión inicial |
