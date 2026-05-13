# ADR-0003 — Usar SQLite local en la app de guardias para operación offline

## Metadatos

| Campo | Valor |
|-------|-------|
| Número | `0003` |
| Título | Usar SQLite local en la app de guardias para operación offline |
| Fecha | `13/05/2026` |
| Autor(es) | Equipo QrTicket |
| Estado | **Aceptada** |
| Alcance | Aplicación móvil de guardias |
| Stakeholders consultados | Mobile, operaciones |

## 1. Contexto

La validación en puerta no puede depender totalmente de internet. El sistema necesita almacenar tickets válidos, registrar escaneos y reconciliar luego. La tensión principal es simplicidad local versus robustez de sincronización.

## 2. Alternativas consideradas

| Alternativa | Pros | Contras | Costo aproximado |
|-------------|------|---------|-------------------|
| Sin modo offline | implementación simple | riesgo operativo inaceptable | bajo |
| Caché en memoria | rápida | no sobrevive reinicios y es frágil | bajo |
| **SQLite local** | persistencia real, consultas rápidas, soporte móvil amplio | requiere reconciliación cuidadosa | medio |

## 3. Decisión

> **Elegimos SQLite local como base offline de la app de guardias.**

Permite persistir datasets descargados y escaneos pendientes con baja complejidad relativa y buen rendimiento en dispositivos móviles.

## 4. Consecuencias

### 4.1 Positivas

- Continuidad operativa en eventos sin red.
- Persistencia de escaneos pendientes.
- Simplicidad de consulta local.

### 4.2 Negativas / costos

- Necesidad de diseñar bien conflictos y versiones de sync.
- Riesgo si el dataset descargado está desactualizado.

### 4.3 Neutras / observables

- La UX debe mostrar claramente estado de sincronización.

## 5. Impacto en el sistema

- **Código**: capa local mobile y motor de sync.
- **Operaciones**: procedimientos previos al evento para descarga.
- **Seguridad**: mínimos datos necesarios en el dispositivo.
- **Costo**: bajo-medio.

## 6. Plan de reversión

- Señal temprana: demasiados conflictos o corrupción local.
- Plan B: mantener cache cifrada simplificada y reducir offline a listas hashadas.

## 7. Validación

- Éxito de sync `>= 95%`.
- cero pérdida silenciosa de escaneos.
- pruebas de reinicio sin red.

## 8. Referencias

- `docs/fsd/FSD_v0.1.md` UC-007, UC-009
- `docs/DTI.md`

## 9. Historial

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 1 | 13/05/2026 | Equipo QrTicket | propuesta inicial |
