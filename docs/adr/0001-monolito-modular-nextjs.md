# ADR-0001 — Adoptar monolito modular con Next.js + backend por dominios

## Metadatos

| Campo | Valor |
|-------|-------|
| Número | `0001` |
| Título | Adoptar monolito modular con Next.js + backend por dominios |
| Fecha | `13/05/2026` |
| Autor(es) | Equipo QrTicket |
| Estado | **Aceptada** |
| Alcance | Todo el sistema |
| Stakeholders consultados | Producto, frontend, backend |

## 1. Contexto

QrTicket necesita moverse rápido con un equipo pequeño, pero también separar dominios como eventos, pagos, tickets, accesos y reportes. Microservicios puros agregan costo operativo temprano; un monolito sin módulos claros volvería difícil evolucionar el sistema. La tensión principal es velocidad de entrega versus mantenibilidad futura.

## 2. Alternativas consideradas

| Alternativa | Pros | Contras | Costo aproximado |
|-------------|------|---------|-------------------|
| Monolito simple | rápido de iniciar | alto acoplamiento | bajo |
| Microservicios | escalabilidad independiente | complejidad operativa temprana | alto |
| **Monolito modular** | balance entre velocidad y separación por dominio | requiere disciplina arquitectónica | medio |

## 3. Decisión

> **Elegimos un monolito modular con Next.js/TypeScript y módulos explícitos por dominio.**

La decisión permite construir rápido, compartir modelos y autenticación, y dejar fronteras claras para una futura extracción de servicios si el volumen lo exige.

## 4. Consecuencias

### 4.1 Positivas

- Menor complejidad operativa inicial.
- Mejor velocidad de desarrollo.
- Separación clara por dominios del negocio.

### 4.2 Negativas / costos

- Riesgo de acoplamiento si no se respetan módulos.
- Escalado independiente limitado al inicio.

### 4.3 Neutras / observables

- Requiere convenciones de carpetas, contratos y ownership por dominio.

## 5. Impacto en el sistema

- **Código**: módulos `auth`, `events`, `payments`, `tickets`, `access`, `reports`, `notifications`.
- **Operaciones**: un solo despliegue principal.
- **Seguridad**: RBAC centralizado.
- **Equipo**: menor carga DevOps inicial.
- **Costo**: menor que microservicios en fase MVP.

## 6. Plan de reversión

- Señal temprana: despliegues muy lentos, incidentes por acoplamiento o picos asimétricos.
- Costo estimado: medio.
- Plan B: extraer primero `payments` o `access` como servicios independientes.

## 7. Validación

- Métricas: lead time, defectos por módulo, tiempo de build, incidentes por acoplamiento.
- Revisión: fin de Q4 2026.

## 8. Referencias

- `docs/DTI.md`
- `docs/fsd/FSD_v0.1.md`

## 9. Historial

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| 1 | 13/05/2026 | Equipo QrTicket | propuesta inicial |
