# ADR-0005 — Encapsular pagos QR mediante adaptadores y webhooks idempotentes

## Metadatos

| Campo | Valor |
|-------|-------|
| Número | `0005` |
| Título | Encapsular pagos QR mediante adaptadores y webhooks idempotentes |
| Fecha | `13/05/2026` |
| Autor(es) | Equipo QrTicket |
| Estado | **Aceptada** |
| Alcance | Módulo de pagos |
| Stakeholders consultados | Backend, producto |

## 1. Contexto

El producto debe convivir con varios proveedores de cobro y confirmación. Implementar lógica específica de cada banco en el núcleo haría frágil el sistema. La tensión es velocidad de integración hoy versus flexibilidad futura.

## 2. Alternativas consideradas

| Alternativa | Pros | Contras | Costo aproximado |
|-------------|------|---------|-------------------|
| Integrar banco directo en core | rápido al inicio | alto acoplamiento | bajo |
| **Adaptadores por proveedor** | extensible y testeable | más trabajo inicial | medio |
| Broker externo único | simplifica integración | dependencia externa alta | medio-alto |

## 3. Decisión

> **Elegimos una capa de adaptadores de pago con webhooks idempotentes y contrato común de conciliación.**

Así el producto puede incorporar QR Simple, bancos específicos o futuras pasarelas sin romper el dominio central de órdenes y tickets.

## 4. Consecuencias

### 4.1 Positivas

- Más flexibilidad frente a proveedores.
- Menor acoplamiento al cambiar pasarela.
- Mejor testabilidad de callbacks y errores.

### 4.2 Negativas / costos

- Más código de orquestación inicial.
- Necesidad de definir contratos y mapping por proveedor.

### 4.3 Neutras / observables

- Los estados internos de pago siguen siendo unificados.

## 5. Impacto en el sistema

- **Código**: interfaces/adapters para `createPayment`, `verifyPayment`, `parseWebhook`.
- **Operaciones**: manejo de secretos y replay seguro.
- **Seguridad**: validación de firma, idempotencia y auditoría.

## 6. Plan de reversión

- Si sólo sobrevive un proveedor en la práctica, se simplifica la implementación conservando el contrato interno.

## 7. Validación

- confirmaciones duplicadas sin doble emisión.
- integración de un segundo proveedor con cambios acotados.

## 8. Referencias

- `docs/fsd/FSD_v0.1.md` UC-004, UC-005
- `docs/DTI.md`

## 9. Historial

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 1 | 13/05/2026 | Equipo QrTicket | propuesta inicial |
