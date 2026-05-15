---
name: tenant-isolation-reviewer
description: >
  Enforce el aislamiento multi-tenant de QrTicket (BR-F-012, RB-07) en todo
  endpoint, servicio y query. Garantiza que un organizador nunca pueda leer
  ni mutar recursos de otra organización y que los guardias sólo accedan a
  eventos asignados (BR-F-008). Activar en cualquier PR que toque controllers,
  use cases o repositorios.
allowed-tools:
  - read
  - edit
model-tier: sonnet
fsd-version-min: v0.1
status: stable
owner: backend / security — QrTicket
---

# Skill: `tenant-isolation-reviewer` — auditor de aislamiento multi-tenant

> Skill de revisión obligatoria. QrTicket es multi-tenant por diseño y un
> bug de aislamiento es una incidencia P0.

## 1. Cuándo activarla (triggers)

- DURANTE: revisión de cualquier endpoint nuevo o modificado.
- ARRANCA cuando: el usuario invoca `"@tenant-isolation-reviewer <ruta>"` o un PR añade controllers/use cases.
- NO ACTIVAR cuando: el cambio es puramente cosmético (CSS, copy) o sólo agrega tests.

## 2. Entradas obligatorias (Inputs)

- Diff o lista de archivos modificados.
- Rol(es) que pueden ejecutar el endpoint (`super_admin | manager | guard | attendee`).
- Recurso(s) tocados y su FK a `organization_id` o `event_id`.

Si falta cualquiera, responder: `"Necesito diff + roles + recurso (con FK a organization/event) antes de revisar."`

## 3. Fuentes de verdad (orden de precedencia)

1. FSD §5 BR-F-012 (organizador sólo opera recursos de su organización).
2. FSD §5 BR-F-008 (guardias sólo descargan eventos asignados).
3. BRD §12 RB-07 (aislamiento multi-tenant a nivel negocio).
4. PRD §5.6 PRD-US-017 (guardia ve sólo eventos asignados).
5. ADR-0001 (monolito modular Next.js, define dónde vive la autorización).

## 4. Procedimiento

1. **Identificar el "tenant boundary"** del endpoint:
   - Para `manager` → `organization_id` derivada del JWT.
   - Para `guard` → conjunto de `event_id` activos en `guard_assignments`.
   - Para `attendee` → `user_id` (propietario de la orden/ticket).
   - Para `super_admin` → sin restricción, pero auditar siempre.
2. **Verificar inyección de tenant en queries**:
   - Toda query a `events`, `tickets`, `orders`, `payments`, `access_logs` debe incluir el predicado de aislamiento.
   - Repositorios con métodos `findById` deben recibir el `tenantCtx` o derivarlo del request scope.
3. **Verificar autorización antes de la operación**:
   - 401 si no autenticado, 403 si autenticado pero sin pertenencia.
   - `404` (no `403`) cuando el recurso existe pero no pertenece — para no filtrar existencia.
4. **Detectar fugas por joins**: cualquier `JOIN` que cruce tenants debe estar justificado y limitado por `WHERE`.
5. **Auditoría**: toda operación cross-tenant intencional (super_admin) debe quedar en `audit_logs` con razón.

## 5. Salida esperada

- Tabla de revisión en el PR:

| Endpoint | Rol(es) | Tenant boundary | Predicado en query | Test de isolation |
|----------|---------|------------------|---------------------|-------------------|
| `GET /events/:id` | manager | `org_id` del JWT | `WHERE org_id = :org_id` | `events.isolation.spec.ts` |
| `POST /sync/:eventId` | guard | `event_id ∈ assignments` | `EXISTS(guard_assignments...)` | `sync.isolation.spec.ts` |

- Diff sugerido para añadir el predicado faltante.
- Marcar como **bloqueante** cualquier endpoint sin test de isolation.

## 6. Verificación (criterios de "bien hecho")

- 100% de endpoints listan su tenant boundary en la tabla.
- Cada endpoint tiene un test que intenta acceso cross-tenant y obtiene `404` o `403`.
- Repositorios prohíben `findById` sin contexto de tenant (compile-time si TS).
- Ningún log expone IDs de tenants ajenos.

## 7. Anti-patrones específicos del dominio

- **Confiar en filtros del cliente** (`?organization_id=...` enviado por el cliente).
- **Devolver `403` cuando el recurso no es del tenant** — filtra existencia; usar `404`.
- **Joins entre `events` y `tickets` sin chequear `events.organization_id`** — vector clásico de IDOR.
- **Cache compartida sin clave por tenant** — un manager puede ver KPIs del tenant anterior.
- **Permitir al guardia ver KPIs/dashboards** del evento — su rol es operativo, no analítico.
- **Endpoints `super_admin` sin auditoría** — el rol más poderoso debe ser el más auditado.

## 8. Mini ejemplo de invocación

> "@tenant-isolation-reviewer revisa el PR #57 que agrega `GET /events/:id/orders`. Rol: manager. Recurso: `orders` filtradas por `event_id`."

## 9. Modos de fallo conocidos

- Endpoint público (landing) accidentalmente requiere JWT — verificar lista de endpoints públicos antes de marcar 401 como correcto.
- `super_admin` actuando en nombre de un tenant — exigir header `X-Acting-Org` y registrar en `audit_logs`.
- Tests pasan en SQLite local pero la query real corre en Postgres con RLS deshabilitado — verificar contra Postgres en CI.

## 10. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 0.1.0 | 2026-05-13 | Equipo QrTicket | versión inicial |
