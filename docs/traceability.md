# Trazabilidad — QrTicket

> Matriz bidireccional `BRD -> MRD -> PRD -> FSD -> NFR -> ADR` para el release documental 1.0.0.

## Última actualización

- Fecha: 2026-05-13
- Artefacto orquestador: `docs/PROMPT_MAPPING.md`

## Forward (BRD -> ADR/NFR)

| BR | MRD-N | PRD-REQ | PRD-US | FSD-UC | NFR | ADR | Estado |
|----|-------|---------|--------|--------|-----|-----|--------|
| BR-001 | MRD-N-01 | PRD-REQ-001 | PRD-US-001..003 | FSD-UC-001 | NFR-007 | ADR-0001, ADR-0002 | applied |
| BR-001 | MRD-N-01 | PRD-REQ-002 | PRD-US-004..006 | FSD-UC-002 | NFR-007 | ADR-0001, ADR-0002 | applied |
| BR-002 | MRD-N-02 | PRD-REQ-003 | PRD-US-007 | FSD-UC-003 | NFR-002 | ADR-0001 | applied |
| BR-002 | MRD-N-02 | PRD-REQ-004 | PRD-US-008..010 | FSD-UC-004 | NFR-002 | ADR-0001, ADR-0005 | applied |
| BR-003 | MRD-N-03 | PRD-REQ-006 | PRD-US-012 | FSD-UC-005 | NFR-006 | ADR-0004 | applied |
| BR-004 | MRD-N-04 | PRD-REQ-011 | PRD-US-021..023 | FSD-UC-008, FSD-UC-009 | NFR-001, NFR-008 | ADR-0004, ADR-0006 | applied |
| BR-005 | MRD-N-05 | PRD-REQ-009, PRD-REQ-010, PRD-REQ-011 | PRD-US-017..023 | FSD-UC-007, FSD-UC-009 | NFR-004, NFR-009 | ADR-0003, ADR-0006 | applied |
| BR-006 | MRD-N-06 | PRD-REQ-005, PRD-REQ-007 | PRD-US-009, PRD-US-011 | FSD-UC-004, FSD-UC-005 | NFR-005 | ADR-0005 | applied |
| BR-007 | MRD-N-07 | PRD-REQ-007 | PRD-US-011 | FSD-UC-005 | NFR-007 | ADR-0005 | applied |
| BR-008 | MRD-N-08 | PRD-REQ-013 | PRD-US-024, PRD-US-025 | FSD-UC-010 | NFR-007 | ADR-0002 | applied |
| BR-009 | MRD-N-09 | PRD-REQ-014 | PRD-US-017, PRD-US-026 | transversal | NFR-005 | ADR-0001 | applied |
| BR-010 | MRD-N-10 | PRD-REQ-012 | PRD-US-022, PRD-US-023 | FSD-UC-008, FSD-UC-009 | NFR-006 | ADR-0004, ADR-0006 | applied |
| BR-011 | MRD-N-11 | PRD-REQ-015 | PRD-US-002, PRD-US-007 | FSD-UC-003 | NFR-002 | ADR-0001 | applied |
| BR-012 | MRD-N-12 | PRD-REQ-008, PRD-REQ-016 | PRD-US-013..016 | FSD-UC-006 | NFR-007 | ADR-0001 | applied |

## Trazabilidad transversal NFR

| PRD-NFR | FSD NFR | ADR | Estado |
|---------|---------|-----|--------|
| PRD-NFR-001 | NFR-001 | ADR-0004, ADR-0006 | applied |
| PRD-NFR-002 | NFR-002 | ADR-0002 | applied |
| PRD-NFR-003 | NFR-003 | ADR-0002 | applied |
| PRD-NFR-004 | NFR-006 | ADR-0004 | applied |
| PRD-NFR-005 | NFR-005 | ADR-0005 | applied |
| PRD-NFR-006 | NFR-004 | ADR-0003, ADR-0006 | applied |
| PRD-NFR-007 | NFR-008 | ADR-0006 | applied |
| PRD-NFR-008 | NFR-007 | ADR-0001, ADR-0005 | applied |
| PRD-NFR-009 | NFR-009 | ADR-0003 | applied |
| PRD-NFR-010 | NFR-010 | ADR-0001 | applied |

## Cobertura

| Verificación | Esperado | Actual | Estado |
|--------------|----------|--------|--------|
| Cada BR aparece en al menos 1 MRD-N | sí | 12/12 | OK |
| Cada MRD-N aparece en al menos 1 PRD-REQ | sí | 12/12 | OK |
| Cada PRD-REQ aparece en FSD o trazabilidad transversal | sí | 16/16 | OK |
| Cada FSD-UC tiene Gherkin | sí | 10/10 | OK |
| Cada FSD-UC tiene contrato funcional | sí | 10/10 | OK |
| Cada NFR tiene métrica y umbral | sí | 10/10 | OK |
| ADRs registradas | >= 3 | 6 | OK |

## Reverse (IDs huérfanos)

| ID huérfano | Aparece en | Debería citarse en |
|-------------|------------|---------------------|
| (vacío) | | |

## Cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| v0.1 | 2026-05-13 | Equipo QrTicket | matriz inicial |
