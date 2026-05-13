# Aportes Individuales por Release — QrTicket

> Documento de aportes individuales basado en [templates/APORTES_TEMPLATE.md](../../templates/APORTES_TEMPLATE.md).

## 0. Metadatos

| Campo | Valor |
|-------|-------|
| Producto | Qrticket |
| Grupo | `S6` |
| Release evaluable | `release/1.0.0` |
| Sesión asociada | `S6` |
| Fecha de cierre | `13/05/2026` |
| Integrantes del grupo (n) | `Antonio Ovando, @carlicode, Carla Marcela Florida Roman` (n = `2`) |
| Branch del release | `release/1.0.0` |
| Commit de cierre (HEAD) | `pendiente` |

## 1. Tabla de tareas atribuidas

| # | Integrante | Tarea concreta | Categoría | Referencia | Fecha |
|---|------------|----------------|-----------|------------|-------|
| 1 | Antonio Ovando | Resumen ejecutivo y business case del BRD | BRD | `docs/brd/BRD_v0.1.md` §1, §15 | 13/05 |
| 2 | Antonio Ovando | Definición de KPIs y objetivos SMART | BRD | `docs/brd/BRD_v0.1.md` §8, §9 | 13/05 |
| 3 | Antonio Ovando | Segmentos, personas y JTBD del MRD | MRD | `docs/mrd/MRD_v0.1.md` §4, §5 | 13/05 |
| 4 | Antonio Ovando | Go-to-market y pricing del MRD | MRD | `docs/mrd/MRD_v0.1.md` §8, §9 | 13/05 |
| 5 | Antonio Ovando | User journeys del PRD | PRD | `docs/prd/PRD_v0.1.md` §4.2 | 13/05 |
| 6 | Antonio Ovando | Historias PRD-US-001 a PRD-US-013 | PRD | `docs/prd/PRD_v0.1.md` §5 | 13/05 |
| 7 | Antonio Ovando | Casos de uso FSD-UC-001 a FSD-UC-005 | UC | `docs/fsd/FSD_v0.1.md` §4 | 13/05 |
| 8 | Antonio Ovando | ADR-0001, ADR-0002, ADR-0005 | ADR | `docs/adr/*.md` | 13/05 |
| 9 | Antonio Ovando | Diagrama C4 de contexto y contenedores del DTI | Diagrama | `docs/DTI.md` §2.1, §3.2 | 13/05 |
| 10 | Antonio Ovando | Matriz principal de trazabilidad | Bitácora | `docs/traceability.md` | 13/05 |
| 11 | Antonio Ovando | Quality gate inicial | Bitácora | `docs/quality-gate-findings.md` | 13/05 |
| 12 | Antonio Ovando | Prompt mapping del release | Prompt | `docs/PROMPT_MAPPING.md` | 13/05 |
| 13 | Carla Marcela Florida Roman | Personas operativas del BRD y panorama competitivo | BRD | `docs/brd/BRD_v0.1.md` §4, §6 | 13/05 |
| 14 | Carla Marcela Florida Roman | Tendencias, competencia y riesgos del MRD | MRD | `docs/mrd/MRD_v0.1.md` §3.2, §6, §13 | 13/05 |
| 15 | Carla Marcela Florida Roman | Historias PRD-US-014 a PRD-US-026 | PRD | `docs/prd/PRD_v0.1.md` §5 | 13/05 |
| 16 | Carla Marcela Florida Roman | Requisitos funcionales y NFRs del PRD | PRD | `docs/prd/PRD_v0.1.md` §7, §8 | 13/05 |
| 17 | Carla Marcela Florida Roman | Casos de uso FSD-UC-006 a FSD-UC-010 | UC | `docs/fsd/FSD_v0.1.md` §4 | 13/05 |
| 18 | Carla Marcela Florida Roman | Reglas de negocio, modelo de datos y NFRs del FSD | FSD | `docs/fsd/FSD_v0.1.md` §5, §6, §10 | 13/05 |
| 19 | Carla Marcela Florida Roman | ADR-0003, ADR-0004, ADR-0006 | ADR | `docs/adr/*.md` | 13/05 |
| 20 | Carla Marcela Florida Roman | Guía UI/UX operativa | Diagrama | `docs/design/ui-ux-ticketing-guidelines.md` | 13/05 |
| 21 | Carla Marcela Florida Roman | Bounded contexts, puertos y eventos del DTI | FSD | `docs/DTI.md` §4, §5, §7 | 13/05 |
| 22 | Carla Marcela Florida Roman | Integraciones y POCs del DTI | FSD | `docs/DTI.md` §8, §10 | 13/05 |
| 23 | Carla Marcela Florida Roman | Documento de aportes individuales | Bitácora | `docs/aportes/release-1.0.0.md` | 13/05 |
| 24 | Carla Marcela Florida Roman | Revisión de consistencia BRD→MRD→PRD→FSD | Otro | `docs/*` | 13/05 |

## 2. Resumen por integrante

| Integrante | Total de tareas | Categorías cubiertas (#) | Observación |
|------------|-----------------|--------------------------|-------------|
| Antonio Ovando | 12 | 8 | lideró negocio, trazabilidad y calidad |
| Carla Marcela Florida Roman | 12 | 8 | lideró especificación funcional, ADRs y DTI |
| **Total grupo** | **24** | — | — |

## 3. Cálculo del factor de aporte individual

```text
aporte_promedio_grupo = total_tareas_grupo / n_integrantes = 24 / 2 = 12
factor_i              = clamp(tareas_i / aporte_promedio_grupo, 0.5, 1.1)
nota_individual_i     = nota_grupal × factor_i
```

### Aplicación

| Integrante | Tareas | factor sin clamp | factor (clamp 0.5–1.1) | Nota individual |
|------------|--------|------------------|-------------------------|-----------------|
| Antonio Ovando | 12 | 1.0 | 1.0 | `Nota_grupal × 1.0` |
| Carla Marcela Florida Roman | 12 | 1.0 | 1.0 | `Nota_grupal × 1.0` |

> **Aporte promedio del grupo**: `24 / 2 = 12` tareas por persona.

## 4. Reglas del grupo sobre qué cuenta como tarea

- Una sección sustantiva de documento cuenta como 1 tarea.
- Un grupo de historias o casos de uso coherente cuenta como 1 tarea cuando se entrega completo.
- Un ADR aceptado cuenta como 1 tarea.
- Una matriz de trazabilidad o quality gate cuenta como 1 tarea.
- No cuentan cambios cosméticos aislados.

## 5. Auditoría del docente (opcional)

| Integrante | Factor calculado | Factor final aplicado | Justificación del ajuste |
|------------|------------------|------------------------|---------------------------|
| Pendiente | — | — | — |

## 6. Checklist de cierre del release

- [x] Metadatos completos.
- [x] Cada tarea tiene integrante, categoría y referencia verificable.
- [x] Suma de tareas por integrante = total del grupo.
- [x] Factor calculado para cada integrante.
- [x] Granularidad documentada.
