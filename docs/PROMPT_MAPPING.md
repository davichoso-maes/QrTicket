# PROMPT_MAPPING — QrTicket

> Catálogo de prompts utilizados para producir los artefactos documentales de QrTicket. Sigue la estructura de [templates/PROMPT_TEMPLATE.md](../templates/PROMPT_TEMPLATE.md).

## Índice

| ID | Artefacto producido | Skill / Rol | Modelo sugerido | Fecha |
|----|---------------------|-------------|------------------|-------|
| PR-BRD-001 | `docs/brd/BRD_v0.1.md` | `brd-author-qrticket` | GPT-5 | 2026-05-13 |
| PR-MRD-001 | `docs/mrd/MRD_v0.1.md` | `mrd-author-qrticket` | GPT-5 | 2026-05-13 |
| PR-PRD-001 | `docs/prd/PRD_v0.1.md` | `prd-author-qrticket` | GPT-5 | 2026-05-13 |
| PR-FSD-001 | `docs/fsd/FSD_v0.1.md` | `fsd-author-qrticket` | GPT-5 | 2026-05-13 |
| PR-ADR-001..006 | `docs/adr/*.md` | `adr-recorder-qrticket` | GPT-5 | 2026-05-13 |
| PR-DTI-001 | `docs/DTI.md` | `dti-author-qrticket` | GPT-5 | 2026-05-13 |
| PR-DESIGN-001 | `docs/design/ui-ux-ticketing-guidelines.md` | `design-guidelines-qrticket` | GPT-5 | 2026-05-13 |
| PR-TRC-001 | `docs/traceability.md` | `traceability-compiler-qrticket` | GPT-5 | 2026-05-13 |
| PR-QG-001 | `docs/quality-gate-findings.md` | `quality-gate-qrticket` | GPT-5 | 2026-05-13 |
| PR-APR-001 | `docs/aportes/release-1.0.0.md` | `aportes-author-qrticket` | GPT-5 | 2026-05-13 |

## Resumen de prompts

### PR-BRD-001

- **Role**: estratega de negocio SaaS/eventtech.
- **Task**: traducir `CLAUDE.md` a un BRD con negocio, KPIs, BMC y riesgos.
- **Output**: `docs/brd/BRD_v0.1.md`.

### PR-MRD-001

- **Role**: product manager orientado a mercado boliviano.
- **Task**: derivar segmentos, JTBD, competencia, GTM y pricing.
- **Output**: `docs/mrd/MRD_v0.1.md`.

### PR-PRD-001

- **Role**: product manager técnico.
- **Task**: convertir BRD/MRD en historias, journeys, requisitos y NFRs.
- **Output**: `docs/prd/PRD_v0.1.md`.

### PR-FSD-001

- **Role**: solutions architect de plataforma de ticketing.
- **Task**: especificar casos de uso, reglas, modelo de datos, contratos y pruebas.
- **Output**: `docs/fsd/FSD_v0.1.md`.

### PR-ADR-001..006

- **Role**: arquitecto de software.
- **Task**: registrar decisiones arquitectónicas críticas de QrTicket.
- **Output**: `docs/adr/*.md`.

### PR-DTI-001

- **Role**: arquitecto técnico principal.
- **Task**: consolidar la visión técnica, C4, bounded contexts y despliegue.
- **Output**: `docs/DTI.md`.

### PR-DESIGN-001

- **Role**: UX strategist de producto operacional.
- **Task**: definir pautas de UI/UX para dashboard, checkout y guardias.
- **Output**: `docs/design/ui-ux-ticketing-guidelines.md`.

### PR-TRC-001

- **Role**: auditor de trazabilidad.
- **Task**: mapear BRD → MRD → PRD → FSD → NFR → ADR.
- **Output**: `docs/traceability.md`.

### PR-QG-001

- **Role**: quality gate reviewer.
- **Task**: revisar consistencia, cobertura y gaps documentales.
- **Output**: `docs/quality-gate-findings.md`.

### PR-APR-001

- **Role**: coordinador de entrega académica.
- **Task**: documentar aportes individuales por release.
- **Output**: `docs/aportes/release-1.0.0.md`.
