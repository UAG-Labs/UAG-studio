# Spec: SYS-001 — Studio Application

**Spec ID:** SYS-001
**Type:** System-overview
**Status:** Draft
**Date:** 2026-06-08
**Author:** Agent

## 1. Overview
1.1 Purpose — Defines Studio as visual editor for UAG projects.
1.2 Context — Studio is the human-facing app editing TAKG and calling compiler.
1.3 Related artifacts
   1.3.A ADR: [ADR-0001 Repository Purpose](../adr/ADR-0001-repository-purpose.md)
   1.3.B Research: [Research Summary](../research/initial-research.md)
   1.3.C Open questions: [Open Questions](../open-questions.md) — none unresolved in this initialized package.
   1.3.D Plan: [Bootstrap Plan](../plans/PLAN-001-bootstrap.md)

## 2. Scope
2.1 Goals
   2.1.A Define app architecture.
   2.1.B Define UI panel responsibilities.
   2.1.C Define React/Rust split.
   2.1.D Define dependencies.
2.2 Non-Goals (out of scope)
   2.2.A Does not define core model.
   2.2.B Does not implement compiler logic inside UI.
   2.2.C Does not make UAGL native editable format.

## 3. Requirements
3.1 Functional requirements
   3.1.A Studio must edit TAKG.
   3.1.B Studio must show canvas and inspectors.
   3.1.C Studio must call compiler.
   3.1.D Studio must display diagnostics/loss reports.
3.2 Non-functional requirements
   3.2.A UI must tolerate invalid TAKG.
   3.2.B Large graphs use views/subgraphs.

## 4. Interface / Data
4.1 Type-specific detail
   4.1.A Frontend interface is React components/stores.
   4.1.B Rust interface is Tauri commands/studio-engine.

## 5. Behavior
5.1 Happy path
   5.1.A User opens Studio.
   5.1.B User edits graph.
   5.1.C User compiles.
   5.1.D Studio displays results.
5.2 Edge cases
   5.2.A Invalid TAKG does not crash UI.
   5.2.B UAGL opens read-only/import.
5.3 Error states
   5.3.A Compiler unavailable shows actionable error.
   5.3.B Save failure preserves dirty state.

## 6. Acceptance Criteria
6.1 Criteria
   6.1.A [ ] TAKG editing exists (verifies §3.1.A) — Verified by: [—]
   6.1.B [ ] Canvas/inspectors exist (verifies §3.1.B) — Verified by: [—]
   6.1.C [ ] Diagnostics display exists (verifies §3.1.C) — Verified by: [—]

## 7. Open Questions & Assumptions
7.1 Open questions — No unresolved open questions are allowed in this initialized documentation package. Future uncertainty must be recorded in [Open Questions](../open-questions.md) before implementation continues.
7.2 Assumptions
   7.2.A Tauri is desktop shell. — Validated: ../research/initial-research.md and ../adr/ADR-0001-repository-purpose.md.
