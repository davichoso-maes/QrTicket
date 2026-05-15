---
name: gherkin-to-tests
description: >
  Convierte los criterios de aceptación Gherkin de los UCs del FSD (`docs/fsd/`)
  en tests automatizados ejecutables (Vitest/Jest + Playwright para E2E,
  Wiremock para integraciones del §8 y k6 para NFR del §10). Adaptación del
  skill canónico `fsd-gherkin-a-tests-aceptacion` al stack TypeScript/Next.js
  de QrTicket. No inventa AC; sólo traduce los existentes.
allowed-tools:
  - read
  - edit
  - run-tests
model-tier: sonnet
fsd-version-min: v0.1
status: stable
owner: QA / backend — QrTicket
---

# Skill: `gherkin-to-tests` — del Gherkin del FSD a tests ejecutables

> Skill canónica adaptada al stack TS/Next.js de QrTicket. Cubre los 10 UCs
> del FSD §4 y los 10 NFRs del FSD §10.

## 1. Cuándo activarla (triggers)

- DURANTE: implementación o cierre de un UC ya codificado.
- ARRANCA cuando: el usuario invoca `"@gherkin-to-tests FSD-UC-NNN"` o abre PR que cierra el UC.
- NO ACTIVAR cuando: el UC aún no tiene bloque ` ```gherkin … ``` ` en su sección de criterios de aceptación.

## 2. Entradas obligatorias (Inputs)

- `FSD-UC-NNN` con bloque Gherkin presente.
- §10 del FSD si el AC referencia un `NFR-NNN`.
- Fixtures realistas: `eventId` (UUID), `eventoSlug` (`congreso-medicina-2026`), `ticketType` (`general | vip | estudiante`), `currency = BOB`, `amount` con 2 decimales.

Si falta cualquiera, responder: `"Necesito el UC con Gherkin presente y los NFR referenciados antes de generar tests."`

## 3. Fuentes de verdad (orden de precedencia)

1. Bloque Gherkin del UC en `docs/fsd/FSD_v0.1.md` §4.
2. FSD §10 (NFR cuantificables).
3. FSD §8 (integraciones externas y SLA).
4. `AGENTS.md` §7 (stack: Next.js, TS, Prisma, Postgres, SQLite).
5. Diagramas `.mmd` en `docs/diagrams/` (para entender flujo esperado).

## 4. Procedimiento

1. **Elegir nivel de prueba** según el AC:
   - regla de dominio pura → **Vitest unit** con `describe.each`.
   - flujo del UC end-to-end → **Playwright** con steps Given/When/Then.
   - integración a DB → **Vitest + Testcontainers (Postgres 16)**.
   - integración a proveedor (§8) → **Wiremock** con stubs en `test/wiremock/<provider>/`.
   - AC con umbral NFR → **k6** en `infra/perf/<uc>.js` con `thresholds`.
2. **Fixtures dominio QrTicket Bolivia**:
   - Organizaciones: `umss-medicina`, `univalle-cs`, `productora-zelaya`.
   - Eventos: `congreso-medicina-2026`, `festival-cala-cala-25`.
   - Tickets: `general`, `vip`, `early-bird`, `estudiante`.
   - Pagos: `BOB` con 2 decimales; referencias `LIB-2026-000NNN`.
   - Zona horaria: `America/La_Paz`.
3. **Tag de trazabilidad obligatorio**: cada test lleva `it.tag(['FSD-UC-NNN','AC-<n>'])` o `test.describe('FSD-UC-NNN', ...)`.
4. **Stubs Wiremock** para proveedor QR (Libélula, BNB...) con: `200` confirmado, `200` rechazado, `5xx`, timeout.
5. **k6** para NFR-001 (validación QR `<= 1500 ms` p95), NFR-002 (creación orden `<= 1000 ms`), NFR-008 (`>= 50 scans/min/puerta`).
6. **Reporte de cobertura por AC**: generar `coverage/fsd-coverage.md` con tabla `AC ↔ test ↔ resultado`.

## 5. Salida esperada

- Archivos `*.spec.ts` (Vitest) o `*.e2e.ts` (Playwright).
- Stubs en `test/wiremock/<provider>/`.
- Si hay NFR: `infra/perf/<uc>.js` con `export const options = { thresholds: { ... } }`.
- Tabla de cierre de PR:

| AC FSD | NFR | Archivo | Tipo |
|--------|-----|---------|------|
| FSD-UC-005 AC1 | — | `tickets/emit.spec.ts` | Vitest unit |
| FSD-UC-005 AC2 | — | `tickets/idempotency.spec.ts` | Vitest + Testcontainers |
| FSD-UC-008 AC1 | NFR-001 | `infra/perf/uc-008.js` | k6 (p95 < 1500ms) |

## 6. Verificación (criterios de "bien hecho")

- 100% de los AC tienen al menos un test verde con sus tags.
- Cada AC con umbral NFR tiene prueba que **falla** si el umbral se viola.
- Stubs Wiremock reflejan failure modes documentados en FSD §7 (Prompt-contracts).
- `pnpm test` y `pnpm test:e2e` pasan en CI; k6 corre contra entorno staging local.
- Cero AC sin test, cero test sin AC asociado.

## 7. Anti-patrones específicos del dominio

- AC con "el sistema responde rápido" sin umbral — STOP, completar §10 NFR primero.
- Mockear el dominio completo (`order`, `payment`, `ticket`) para que el test pase — no verifica reglas.
- Ignorar la rama de fallo del pago QR — el callback `5xx` y `signature inválida` deben tener tests propios.
- Fixtures con emails `test@test.com` — usar `medicina@umss.edu.bo` para detectar regex demasiado estrictos.
- Correr k6 contra producción — siempre staging o local con Testcontainers.

## 8. Mini ejemplo de invocación

> "@gherkin-to-tests FSD-UC-008 'Validar ticket QR online'. Generar Vitest + integración Testcontainers + k6 para NFR-001 (p95 ≤ 1500 ms)."

## 9. Modos de fallo conocidos

- El AC referencia un `NFR-NNN` inexistente → STOP, abrir issue de spec.
- El AC contradice un `BR-F-NNN` → STOP, reabrir el UC; el skill no decide qué regla gana.
- Falta `Given` observable (`Dado el sistema funcionando`) → STOP, pedir precondición concreta.

## 10. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 0.1.0 | 2026-05-13 | Equipo QrTicket | versión inicial (adapta el skill canónico al stack TS/Next.js) |
