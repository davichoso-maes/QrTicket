---
name: payments-adapter-author
description: >
  Genera adaptadores de pasarela QR Bolivia (Libélula, BNB, Tigo Money, Unión)
  para QrTicket, respetando el `PaymentProviderPort` definido por la arquitectura
  hexagonal (DTI §5.1) y el ADR-0005 (adaptadores de pago y webhooks).
  Cubre creación de cobro (FSD-UC-004), verificación de webhook idempotente
  (FSD-UC-005) y manejo de failure modes.
allowed-tools:
  - read
  - edit
  - run-tests
model-tier: sonnet
fsd-version-min: v0.1
status: stable
owner: backend / pagos — QrTicket
---

# Skill: `payments-adapter-author` — autor de adaptadores QR Bolivia

> Skill de dominio. Activar mediante `"@payments-adapter-author <proveedor>"`
> o al editar `infra/payments/<proveedor>/*`.

## 1. Cuándo activarla (triggers)

- DURANTE: alta de un nuevo proveedor QR boliviano o modificación de uno existente.
- ARRANCA cuando: el usuario invoca `"@payments-adapter-author libelula|bnb|tigo|union|qrsimple"` o edita archivos en `infra/payments/`.
- NO ACTIVAR cuando: el cambio sólo toca el dominio (`domain/payments`) sin tocar el adaptador (es trabajo del use case, no de este skill).

## 2. Entradas obligatorias (Inputs)

El usuario MUST proporcionar:

- Proveedor objetivo (uno de `libelula | bnb | tigo | union | qrsimple` o nombre del POC).
- Credenciales de sandbox (no productivas) o referencia al secret manager.
- Documento del proveedor o link a su contrato (esquemas de request/response, firmas).
- ID de la POC asociada en `pocs/POC-NN` si es la primera integración.

Si falta cualquiera, responder: `"Necesito proveedor + sandbox credentials + spec del proveedor antes de crear el adaptador."`

## 3. Fuentes de verdad (orden de precedencia)

1. ADR-0005 (`docs/adr/0005-adaptadores-de-pago-y-webhooks.md`) — contrato del puerto.
2. FSD §4 UC-004 y UC-005 — comportamiento esperado.
3. FSD §5 BR-F-004/005 — referencia única por orden e idempotencia de callbacks.
4. FSD §8 — SLA esperado (`>= 99%`) y autenticación firmada.
5. POC `POC-01` y `POC-03` — aprendizajes de proveedor concreto.
6. `AGENTS.md` §9.5 — métodos de pago soportados (QR, Libélula, Tigo Money, transferencia).

## 4. Procedimiento

1. **Implementar `PaymentProviderPort`**: métodos mínimos `createCharge(order)`, `verifyWebhook(payload, signature)`, `fetchStatus(reference)`.
2. **Firma del webhook**:
   - validar firma antes de cualquier lookup en DB.
   - rechazar con `E_PAYMENT_SIGNATURE` si firma inválida y registrar intento en audit.
3. **Idempotencia (BR-F-005)**:
   - el procesamiento de `verifyWebhook` debe ser idempotente por `(provider, reference)`.
   - segundo callback con misma `reference` y estado `confirmed` ya aplicado → responder `200 OK` sin re-emitir tickets.
4. **Mapeo de estados** del proveedor → estados internos (`pending | confirmed | rejected | expired | refunded`).
5. **Reintentos**: exponencial con jitter, máximo `5` intentos en 24h para `fetchStatus`.
6. **Observabilidad**: tracing del round-trip con tags `provider`, `reference`, `latency_ms`, `outcome`.
7. **Fallback documentado**: si el proveedor cae, dejar la orden en `pending`, no inventar `confirmed`.

## 5. Salida esperada

- Carpeta `infra/payments/<proveedor>/` con:
  - `index.ts` exportando el adaptador.
  - `signature.ts` con verificación de firma.
  - `mapper.ts` con mapeo de estados.
  - `<proveedor>.spec.ts` y stubs Wiremock en `test/mappings/<proveedor>/`.
- Registro en el `payment_provider_registry` (factory) sin tocar el dominio.
- Diff propuesto a `docs/DTI.md` §8 si se agrega un nuevo SLA o método.
- Tabla obligatoria al PR:

| Operación | Método | Test | Failure modes |
|-----------|--------|------|----------------|
| crear cobro | `createCharge` | `<proveedor>.createCharge.spec.ts` | `E_PROVIDER_DOWN`, `E_INVALID_AMOUNT` |
| verificar webhook | `verifyWebhook` | `<proveedor>.webhook.spec.ts` | `E_PAYMENT_SIGNATURE`, `E_DUPLICATE_CALLBACK` |
| consultar estado | `fetchStatus` | `<proveedor>.fetchStatus.spec.ts` | `E_PROVIDER_DOWN`, `E_REFERENCE_NOT_FOUND` |

## 6. Verificación (criterios de "bien hecho")

- El adaptador implementa `PaymentProviderPort` y no tiene dependencias directas al dominio.
- Webhook idempotente verificable con test que envía 2 veces el mismo callback y emite tickets sólo una vez.
- Firma siempre validada antes de tocar DB.
- 100% de los estados del proveedor mapeados; estados desconocidos quedan `pending` y disparan alerta.
- Sandbox y producción seleccionados por configuración (no por código duplicado).
- Cobertura `>= 85%` del adaptador.

## 7. Anti-patrones específicos del dominio

- **Confiar en `200 OK` del webhook sin firma** — Bolivia tiene proveedores con auth heterogénea; siempre firmar.
- **Marcar `confirmed` por timeout** — sin confirmación bancaria no hay confirmación.
- **Loguear el secret del proveedor** o el `signature` en claro.
- **Re-emitir tickets en cada callback** — falla BR-F-005 y duplica entradas.
- **Adaptador que conoce el dominio** — viola hexagonal; el use case orquesta, el adaptador sólo habla con el proveedor.
- **Polling agresivo** sin backoff — bloqueado por el proveedor y caro.

## 8. Mini ejemplo de invocación

> "@payments-adapter-author libelula. POC: POC-01. Sandbox: secrets/libelula-sandbox. Generar adaptador completo con verificación de firma HMAC-SHA256 y stubs Wiremock para los 3 métodos."

## 9. Modos de fallo conocidos

- El proveedor no expone webhook → caer a `fetchStatus` por polling con backoff y documentar en ADR-0005.
- El proveedor no firma sus webhooks → STOP, escalar y, si no hay alternativa, restringir el adaptador a uso interno (no producción) y dejar issue de seguridad abierto.
- Conflicto entre `reference` de proveedor y `payments.reference` interno — usar `reference` interno como identidad y guardar `provider_reference` aparte.

## 10. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 0.1.0 | 2026-05-13 | Equipo QrTicket | versión inicial |
