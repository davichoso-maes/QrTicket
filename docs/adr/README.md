# ADRs — QrTicket

> Registro de decisiones arquitectónicas de QrTicket. Basado en [templates/ADR_TEMPLATE.md](../../templates/ADR_TEMPLATE.md).

## Índice

| ADR | Título | Estado | Alcance | Cita FSD/NFR | Reversión |
|-----|--------|--------|---------|--------------|-----------|
| [ADR-0001](0001-monolito-modular-nextjs.md) | Adoptar monolito modular con Next.js + backend por dominios | Aceptada | Arquitectura core | FSD global, NFR-010 | media |
| [ADR-0002](0002-postgresql-prisma-fuente-de-verdad.md) | Usar PostgreSQL + Prisma como fuente transaccional central | Aceptada | Persistencia central | UC-001..010, NFR-003 | media |
| [ADR-0003](0003-sqlite-offline-first-guardias.md) | Usar SQLite local en la app de guardias para operación offline | Aceptada | Mobile / acceso | UC-007, UC-009, NFR-004 | baja |
| [ADR-0004](0004-qr-dinamico-firmado-server-side.md) | Proteger tickets con QR firmado y validación server-side | Aceptada | Seguridad / tickets | UC-005, UC-008, NFR-006 | baja |
| [ADR-0005](0005-adaptadores-de-pago-y-webhooks.md) | Encapsular pagos QR mediante adaptadores y webhooks idempotentes | Aceptada | Pagos | UC-004, UC-005, NFR-005 | media |
| [ADR-0006](0006-sync-incremental-y-reconciliacion.md) | Sincronización incremental con reconciliación explícita de accesos | Aceptada | Offline sync | UC-007, UC-009, NFR-004 | media |
