# ADR-0006 — Sincronización incremental con reconciliación explícita de accesos

## Metadatos

| Campo | Valor |
|-------|-------|
| Número | `0006` |
| Título | Sincronización incremental con reconciliación explícita de accesos |
| Fecha | `13/05/2026` |
| Autor(es) | Equipo QrTicket |
| Estado | **Aceptada** |
| Alcance | Offline sync y access logs |
| Stakeholders consultados | Mobile, backend, operaciones |

## 1. Contexto

Descargar siempre el dataset completo del evento no escala bien y subir escaneos offline sin reglas claras puede producir conflictos difíciles de auditar. La tensión es simplicidad de implementación versus capacidad de operar múltiples puertas con conectividad irregular.

## 2. Alternativas consideradas

| Alternativa | Pros | Contras | Costo aproximado |
|-------------|------|---------|-------------------|
| Snapshot completo siempre | muy simple | costoso y lento en eventos grandes | medio |
| **Sync incremental + reconciliación** | eficiente y trazable | requiere versionado y reglas | medio |
| P2P entre guardias | reduce dependencia central | complejidad muy alta | alto |

## 3. Decisión

> **Elegimos sincronización incremental por versión y reconciliación explícita de accesos offline.**

Cada descarga y cada lote de escaneos lleva versión, timestamps e identificadores necesarios para reconstruir el historial y resolver conflictos sin pérdida de evidencia.

## 4. Consecuencias

### 4.1 Positivas

- Menor volumen de datos transferidos.
- Mejor trazabilidad de conflictos.
- Escala mejor a eventos con más tickets y guardias.

### 4.2 Negativas / costos

- Lógica de sync más compleja.
- Requiere pruebas cuidadosas de idempotencia y conflicto.

### 4.3 Neutras / observables

- El dashboard debe informar cuando hay datos pendientes de reconciliar.

## 5. Impacto en el sistema

- **Código**: tablas de snapshots, sync cursors y pending logs.
- **Operaciones**: monitoreo de sync lag.
- **Seguridad**: integridad de lotes y autenticación del guardia.

## 6. Plan de reversión

- Plan B: snapshot completo por evento mientras se resuelve la reconciliación, manteniendo lote de pendientes.

## 7. Validación

- sync success `>= 95%`.
- cero pérdida silenciosa de escaneos.
- conflictos detectados y auditados.

## 8. Referencias

- `docs/fsd/FSD_v0.1.md` UC-007, UC-009, NFR-004

## 9. Historial

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 1 | 13/05/2026 | Equipo QrTicket | propuesta inicial |
