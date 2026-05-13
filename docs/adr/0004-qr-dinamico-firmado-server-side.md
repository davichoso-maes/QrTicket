# ADR-0004 — Proteger tickets con QR firmado y validación server-side

## Metadatos

| Campo | Valor |
|-------|-------|
| Número | `0004` |
| Título | Proteger tickets con QR firmado y validación server-side |
| Fecha | `13/05/2026` |
| Autor(es) | Equipo QrTicket |
| Estado | **Aceptada** |
| Alcance | Tickets y antifraude |
| Stakeholders consultados | Backend, seguridad, operaciones |

## 1. Contexto

Un QR meramente visual o con datos fáciles de alterar no es suficiente en el contexto del producto. Se requiere antifraude contra reenvío, alteración y reutilización. La tensión es seguridad versus simplicidad de implementación.

## 2. Alternativas consideradas

| Alternativa | Pros | Contras | Costo aproximado |
|-------------|------|---------|-------------------|
| QR con texto plano | simple | inseguro | bajo |
| QR con UUID simple | fácil | depende demasiado de secreto operacional | bajo |
| **QR firmado + estado server-side** | más seguro y auditable | requiere validación y rotación cuidadosa | medio |

## 3. Decisión

> **Elegimos QR firmado con validación contra estado server-side y soporte offline controlado.**

El QR representa un token verificable, y la verdad operativa del ticket vive en el backend o en el dataset offline autorizado.

## 4. Consecuencias

### 4.1 Positivas

- Menor riesgo de tickets alterados.
- Mejor trazabilidad antifraude.
- Compatible con validación online y offline.

### 4.2 Negativas / costos

- Mayor complejidad en generación y rotación de secretos.
- Necesidad de manejar compatibilidad entre versiones de token.

### 4.3 Neutras / observables

- La interfaz del ticket puede seguir siendo simple para el usuario.

## 5. Impacto en el sistema

- **Código**: servicios de tokenización y validación.
- **Seguridad**: llaves, firmas y auditoría de fraude.
- **Operaciones**: rotación controlada de secretos.

## 6. Plan de reversión

- Plan B: degradar temporalmente a UUID con lookup server-side, manteniendo logs reforzados.

## 7. Validación

- tasa de fraude `< 1%`.
- pruebas de tampering y reuso.

## 8. Referencias

- `docs/fsd/FSD_v0.1.md` UC-005, UC-008, UC-009

## 9. Historial

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 1 | 13/05/2026 | Equipo QrTicket | propuesta inicial |
