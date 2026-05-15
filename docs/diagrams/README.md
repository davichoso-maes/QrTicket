---
title: Catálogo de diagramas Mermaid — QrTicket
release: release/1.0.0
fecha: 2026-05-13
mantenedor: Equipo QrTicket
---

# Diagramas Mermaid — QrTicket

> Catálogo de diagramas `.mmd` derivados del [FSD](../fsd/FSD_v0.1.md), [PRD](../prd/PRD_v0.1.md) y [DTI](../DTI.md).
> Cada diagrama está en un archivo separado para ser diff-friendly, renderizable en `mermaid.live` y trazable por UC.

## Mapeo Caso de uso ↔ Diagrama

| ID Diagrama | Archivo | Tipo Mermaid | UC / Sección relacionada | Trazabilidad |
|-------------|---------|--------------|--------------------------|--------------|
| DIA-01 | [`c4_level1_context.mmd`](c4_level1_context.mmd) | `C4Context` | Sistema completo | DTI §2.1 |
| DIA-02 | [`c4_level2_containers.mmd`](c4_level2_containers.mmd) | `C4Container` | Arquitectura QrTicket | DTI §3.2 |
| DIA-03 | [`c4_level3_checkout_components.mmd`](c4_level3_checkout_components.mmd) | `flowchart LR` | FSD-UC-004, FSD-UC-005 | DTI §3.3 |
| DIA-04 | [`seq_uc004_generar_orden_qr.mmd`](seq_uc004_generar_orden_qr.mmd) | `sequenceDiagram` | FSD-UC-004 | FSD §4.4 |
| DIA-05 | [`seq_uc005_confirmar_pago.mmd`](seq_uc005_confirmar_pago.mmd) | `sequenceDiagram` | FSD-UC-005 | FSD §4.5 |
| DIA-06 | [`seq_uc008_validar_qr_online.mmd`](seq_uc008_validar_qr_online.mmd) | `sequenceDiagram` | FSD-UC-008 | FSD §4.8 |
| DIA-07 | [`seq_uc009_validar_offline_sync.mmd`](seq_uc009_validar_offline_sync.mmd) | `sequenceDiagram` | FSD-UC-009 | FSD §4.9 |
| DIA-08 | [`state_orden_pago.mmd`](state_orden_pago.mmd) | `stateDiagram-v2` | FSD-UC-004/005 | DTI §7.2 |
| DIA-09 | [`state_ticket_lifecycle.mmd`](state_ticket_lifecycle.mmd) | `stateDiagram-v2` | FSD §6.2 (`tickets.status`) | FSD §4.5/4.8/4.9 |
| DIA-10 | [`state_evento_lifecycle.mmd`](state_evento_lifecycle.mmd) | `stateDiagram-v2` | FSD-UC-001/003 | FSD §6.2 |
| DIA-11 | [`er_modelo_datos.mmd`](er_modelo_datos.mmd) | `erDiagram` | Modelo de datos funcional | FSD §6.1 |
| DIA-12 | [`gantt_roadmap_release_1_0_0.mmd`](gantt_roadmap_release_1_0_0.mmd) | `gantt` | Roadmap MVP | PRD §3.3, BRD §17 |

## Cobertura por tipo (rúbrica §8)

| Tipo Mermaid | Requerido | Archivos |
|--------------|-----------|----------|
| `sequenceDiagram` | ✅ | DIA-04, DIA-05, DIA-06, DIA-07 |
| `stateDiagram-v2` | ✅ | DIA-08, DIA-09, DIA-10 |
| `erDiagram` | ✅ | DIA-11 |
| `gantt` | ✅ | DIA-12 |
| `C4Context` / `C4Container` | bonus | DIA-01, DIA-02 |
| `flowchart` | bonus | DIA-03 |

## Cobertura UC crítica ↔ Diagrama de secuencia

| FSD-UC | Diagrama de secuencia |
|--------|------------------------|
| FSD-UC-004 | DIA-04 |
| FSD-UC-005 | DIA-05 |
| FSD-UC-008 | DIA-06 |
| FSD-UC-009 | DIA-07 |

## Verificación

- 12 archivos `.mmd` separados (rúbrica pide ≥ 10).
- Tipos requeridos (`secuencia, estado, ER, Gantt`): los 4 cubiertos.
- Cada UC crítico de validación o pago tiene su diagrama de secuencia mapeado.
- Diagramas renderizan en [mermaid.live](https://mermaid.live).
