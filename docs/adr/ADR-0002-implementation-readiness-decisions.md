# ADR-0002 - Implementation Readiness Decisions for UAG-studio

## Status
Accepted

## Context
The first documentation audit identified open implementation-readiness questions for UAG-studio. The questions covered project format, invalid TAKG editing, React Flow mapping, layout persistence, compiler integration, command boundaries, palette, diagnostics, UAGL inspection, and app target. Each question received an AI recommendation after reviewing the repository documentation and comparable systems.

## Decision
Adopt the AI recommendations recorded in [open-questions.md](../open-questions.md) as the planning baseline for the first implementation plans. These decisions are not final product law; they are the current accepted defaults that implementation plans should use unless a later ADR supersedes them.

## Decisions
| Question | Topic | Decision |
|---|---|---|
| Q-001 | What is the first supported Studio project format? | Support single `.takg.yaml` first, then add project directories once assets/layout sidecars are needed. Defer `.uagpkg` authoring until compiler package semantics are stable. |
| Q-002 | How should Studio represent invalid or partial TAKG? | Save TAKG with unresolved references and compiler diagnostics. The editor should preserve draft intent instead of blocking saves until the graph is valid. |
| Q-003 | What maps React Flow nodes/handles/edges to TAKG semantics? | Use an adapter layer between TAKG views and React Flow nodes/edges/handles so canvas implementation details never become language semantics. |
| Q-004 | Where does layout live? | Store layout in explicit TAKG `layouts` metadata for milestone one, scoped by view ID, and keep it excluded from UAGL during compilation. |
| Q-005 | How does Studio call the compiler? | Call the compiler as a Rust library from `studio-engine` first. Keep the CLI invocation path as an integration fallback for later debugging and version testing. |
| Q-006 | What is the frontend/backend command boundary? | Frontend owns immediate graph editing, selection, undo/redo, and viewport; Rust owns open/save/compile/export/package operations through typed commands. |
| Q-007 | What is the first useful node palette? | Generate the node palette from the loaded dialect registry, but ship a curated core palette first so the UI can be useful before dialect authoring is complete. |
| Q-008 | How should diagnostics appear on the canvas? | Use canvas badges plus a diagnostics panel, backed by compiler source maps. Package-level diagnostics should appear only in the panel. |
| Q-009 | What does read-only/import UAGL mean? | Open UAGL as read-only inspection first. Defer import-to-TAKG until the compiler can emit a trustworthy reverse/loss report. |
| Q-010 | What is the first app target: desktop only or web plus desktop? | Build desktop-only first with a clean adapter boundary, then add a web target once project IO and compiler execution abstractions are stable. |

## Consequences
- Implementation plans can proceed from a concrete baseline instead of unresolved ambiguity.
- Future disagreement should create a new open question and, if accepted, a superseding ADR.
- Specs and plans should cite this ADR when they rely on these decisions.

## Follow-up
- Update implementation plans to reference this ADR.
- Promote decisions into detailed specs when implementation starts.
