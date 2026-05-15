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
| PR-DIA-001 | `docs/diagrams/*.mmd` (12 archivos) | `mermaid-extractor-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-SK-001 | `docs/skills/qr-token-author.md` | `skill-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-SK-002 | `docs/skills/payments-adapter-author.md` | `skill-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-SK-003 | `docs/skills/offline-sync-reviewer.md` | `skill-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-SK-004 | `docs/skills/tenant-isolation-reviewer.md` | `skill-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-SK-005 | `docs/skills/gherkin-to-tests.md` | `skill-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-RULE-001 | `.cursor/rules/tenant-isolation.mdc` | `cursor-rule-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-RULE-002 | `.cursor/rules/payments-idempotency.mdc` | `cursor-rule-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-RULE-003 | `.cursor/rules/qr-security.mdc` | `cursor-rule-author-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-TRC-002 | `docs/traceability.md` (v0.2 — métricas AI-SDLC) | `traceability-compiler-qrticket` | Claude Opus 4.7 | 2026-05-15 |
| PR-QG-002 | `docs/quality-gate-findings.md` (v0.2) | `quality-gate-qrticket` | Claude Opus 4.7 | 2026-05-15 |

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

### PR-DIA-001

- **Role**: extractor y empaquetador de diagramas Mermaid.
- **Task**: derivar diagramas `.mmd` separados desde FSD/PRD/DTI cubriendo `sequenceDiagram`, `stateDiagram-v2`, `erDiagram` y `gantt`.
- **Output**: `docs/diagrams/*.mmd` (12 archivos) + `docs/diagrams/README.md` con catálogo.

### PR-SK-001..005

- **Role**: autor de skills accionables para Claude Code / Cursor.
- **Task**: crear 5 skills de dominio QrTicket siguiendo `templates/SKILL.md` y cubriendo UC críticos.
- **Output**: 5 archivos en `docs/skills/` (`qr-token-author`, `payments-adapter-author`, `offline-sync-reviewer`, `tenant-isolation-reviewer`, `gherkin-to-tests`) + `docs/skills/README.md`.

### PR-RULE-001..003

- **Role**: autor de cursor rules de dominio.
- **Task**: enforzar reglas duras del dominio (aislamiento multi-tenant, idempotencia de pagos, seguridad QR) en PRs.
- **Output**: 3 archivos `.mdc` en `.cursor/rules/`.

### PR-TRC-002

- **Role**: auditor de trazabilidad y métricas AI-SDLC.
- **Task**: ampliar la matriz con métricas (`prompt coverage`, `spec fidelity`, `traceability density`, `gherkin coverage`, `NFR quantification rate`).
- **Output**: `docs/traceability.md` v0.2.

### PR-QG-002

- **Role**: quality gate reviewer (segunda pasada).
- **Task**: cerrar hallazgos H-03 y H-04 con evidencia de los nuevos artefactos; mapear cobertura contra la rúbrica de Avance Intermedio.
- **Output**: `docs/quality-gate-findings.md` v0.2.
