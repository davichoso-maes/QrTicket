# ADR-0002 — Usar PostgreSQL + Prisma como fuente transaccional central

## Metadatos

| Campo | Valor |
|-------|-------|
| Número | `0002` |
| Título | Usar PostgreSQL + Prisma como fuente transaccional central |
| Fecha | `13/05/2026` |
| Autor(es) | Equipo QrTicket |
| Estado | **Aceptada** |
| Alcance | Persistencia central |
| Stakeholders consultados | Backend, datos |

## 1. Contexto

El sistema necesita consistencia para órdenes, pagos, tickets y access logs. También necesita velocidad de iteración con TypeScript. La tensión es entre productividad del ORM y control explícito de SQL, y entre sencillez operativa y potencia relacional.

## 2. Alternativas consideradas

| Alternativa | Pros | Contras | Costo aproximado |
|-------------|------|---------|-------------------|
| PostgreSQL + Prisma | productividad, migraciones, buen soporte relacional | requiere vigilar queries complejas | medio |
| PostgreSQL + SQL manual | máximo control | menor velocidad de entrega | medio |
| MongoDB | flexibilidad documental | peor ajuste para transacciones relacionales core | medio |

## 3. Decisión

> **Elegimos PostgreSQL como base transaccional y Prisma como capa de acceso principal.**

Esto encaja con órdenes, pagos, tickets y auditoría, donde la consistencia y las relaciones explícitas importan más que la flexibilidad documental.

## 4. Consecuencias

### 4.1 Positivas

- Modelo consistente para el core del negocio.
- Buen soporte para transacciones e índices.
- Velocidad de desarrollo con TypeScript.

### 4.2 Negativas / costos

- Algunas consultas analíticas complejas pueden requerir SQL optimizado.
- Riesgo de depender demasiado del ORM en paths críticos.

### 4.3 Neutras / observables

- La reportería pesada puede moverse luego a vistas o pipelines separados.

## 5. Impacto en el sistema

- **Código**: schemas Prisma y repositorios de dominio.
- **Operaciones**: backups, tuning de índices, observabilidad DB.
- **Seguridad**: cifrado en tránsito y control de acceso DB.
- **Costo**: asumible para MVP.

## 6. Plan de reversión

- Señal temprana: cuellos de botella no resueltos o límites fuertes del ORM.
- Plan B: mantener PostgreSQL y reemplazar parcialmente Prisma en rutas críticas por SQL explícito.

## 7. Validación

- p95 de órdenes y validaciones.
- estabilidad de migraciones.
- incidentes por integridad de datos.

## 8. Referencias

- `docs/fsd/FSD_v0.1.md` §6, §10
- `docs/DTI.md`

## 9. Historial

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 1 | 13/05/2026 | Equipo QrTicket | propuesta inicial |
