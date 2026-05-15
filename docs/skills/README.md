---
title: Catálogo de Skills — QrTicket
release: release/1.0.0
fecha: 2026-05-13
mantenedor: Equipo QrTicket
---

# Skills accionables — QrTicket

> Skills de dominio para QrTicket, alineadas al formato de [templates/SKILL.md](../../templates/SKILL.md).
> Las skills de procesos transversales (C4, DTI, POC) viven en [templates/skills/](../../templates/skills/) y se reutilizan tal cual.

## Catálogo

| ID | Skill | Archivo | Activador (cuándo) | UC / NFR / ADR cubierto |
|----|-------|---------|--------------------|--------------------------|
| SK-01 | `qr-token-author` | [`qr-token-author.md`](qr-token-author.md) | generar/validar token firmado QR | FSD-UC-005/008/009, NFR-005/006, ADR-0004 |
| SK-02 | `payments-adapter-author` | [`payments-adapter-author.md`](payments-adapter-author.md) | crear adaptador a pasarela QR Bolivia | FSD-UC-004/005, NFR-005, ADR-0005 |
| SK-03 | `offline-sync-reviewer` | [`offline-sync-reviewer.md`](offline-sync-reviewer.md) | revisar/lintar sync SQLite ↔ Postgres | FSD-UC-007/009, NFR-004, ADR-0003/0006 |
| SK-04 | `tenant-isolation-reviewer` | [`tenant-isolation-reviewer.md`](tenant-isolation-reviewer.md) | enforzar RBAC + multi-tenant en endpoints | BR-F-008/012, ADR-0001 |
| SK-05 | `gherkin-to-tests` | [`gherkin-to-tests.md`](gherkin-to-tests.md) | convertir Gherkin de UCs FSD a tests | FSD §4 (todos los UC), §10 (NFR) |

## Skills transversales reutilizadas (no replicadas aquí)

| Skill | Ubicación canónica | Propósito |
|-------|---------------------|-----------|
| `c4-architect` | [`templates/skills/c4.md`](../../templates/skills/c4.md) | autor/validador C4 Mermaid (Niveles 1-3) |
| `dti-author` | [`templates/skills/dti-author.md`](../../templates/skills/dti-author.md) | consolidador DTI con bounded contexts y C4 |
| `poc-runner` | [`templates/skills/poc-runner.md`](../../templates/skills/poc-runner.md) | bootstrapea/ejecuta POCs reproducibles |

## Total

- **Skills de dominio QrTicket**: 5 (SK-01 a SK-05).
- **Skills transversales del módulo**: 3.
- **Total accionable**: 8 (≥ 5 requerido por rúbrica §9).

## Cómo activarlas

Para activar en Claude Code: copiar la skill a `.claude/skills/<nombre>/SKILL.md` en el repo, o a `~/.claude/skills/<nombre>/` para alcance global.
Las cursor rules complementarias viven en [`.cursor/rules/`](../../.cursor/rules/).
