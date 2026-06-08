# Spec: DATA-001 - Studio Project State

**Spec ID:** DATA-001
**Type:** Data
**Status:** Draft
**Date:** 2026-06-08
**Author:** Agent

## 1. Overview
1.1 Purpose - Defines frontend project state while editing UAG projects.
1.2 Context - Studio needs state for partial TAKG, selection, active view, diagnostics, and dirty status.
1.3 Related artifacts
   1.3.A ADR: [ADR-0001 Repository Purpose](../adr/ADR-0001-repository-purpose.md)
   1.3.B Research: [Research Summary](../research/initial-research.md)
   1.3.C Open questions: [Open Questions](../open-questions.md) - none unresolved in this initialized package.
   1.3.D Plan: [Bootstrap Plan](../plans/PLAN-001-bootstrap.md)

## 2. Scope
2.1 Goals
   2.1.A Define project store.
   2.1.B Define graph store.
   2.1.C Define selection store.
   2.1.D Define view store.
   2.1.E Define diagnostics, source-map, compile-result, export-result, and policy state.
2.2 Non-Goals (out of scope)
   2.2.A Does not replace UAG-core model.
   2.2.B Does not persist UI-only state into UAGL.

## 3. Requirements
3.1 Functional requirements
   3.1.A State tracks file path, dirty state, graph, active view, selection, diagnostics, source maps, compile result, export status, policy, and recent files.
   3.1.B Semantic state serializes to TAKG.
   3.1.C Layout remains separate.
   3.1.D Compile results are immutable snapshots linked to the TAKG revision that produced them.
   3.1.E UAGL opens read-only until reverse import and import loss reports exist.
   3.1.F Runtime observations and generated artifacts are displayed as overlays/references and must not mutate TAKG design intent.
3.2 Non-functional requirements
   3.2.A State updates predictable/testable.
   3.2.B No hidden mutation outside mutation functions.
   3.2.C Undo/redo must operate on TAKG/editor mutations, not compiler output.

## 4. Interface / Data
4.1 Type-specific detail
   4.1.A Data includes project metadata, graph objects, layout, selection, diagnostics, source maps, compile result, export status, policy, and dirty status.
   4.1.B Stores are TypeScript modules.
   4.1.C Store adapters convert between TAKG, canvas view models, compiler results, and diagnostics.
   4.1.D Diagnostic refs can target visible objects, hidden objects, package-level issues, source spans, or export artifacts.

## 5. Behavior
5.1 Happy path
   5.1.A User edits node.
   5.1.B Mutation updates store.
   5.1.C Dirty flag set.
   5.1.D Save serializes TAKG.
5.2 Edge cases
   5.2.A Selection may reference deleted object until cleanup.
   5.2.B Diagnostics can reference hidden objects.
   5.2.C Compile result becomes stale after any semantic edit and remains inspectable as prior output.
5.3 Error states
   5.3.A Invalid mutation returns controlled error.
   5.3.B Save with missing graph returns error.
   5.3.C Attempt to edit read-only UAGL creates a controlled error and offers import only when supported.

## 6. Acceptance Criteria
6.1 Criteria
   6.1.A [ ] Dirty state tracked (verifies 3.1.A) - Verified by: [--]
   6.1.B [ ] Graph serializes TAKG (verifies 3.1.B) - Verified by: [--]
   6.1.C [ ] Layout separate (verifies 3.1.C) - Verified by: [--]
   6.1.D [ ] Compile snapshots are revision-linked (verifies 3.1.D) - Verified by: [--]
   6.1.E [ ] UAGL read-only state exists (verifies 3.1.E) - Verified by: [--]

## 7. Open Questions & Assumptions
7.1 Open questions - No unresolved open questions are allowed in this initialized documentation package. Future uncertainty must be recorded in [Open Questions](../open-questions.md) before implementation continues.
7.2 Assumptions
   7.2.A A simple testable state store may be used. - Validated: ../research/initial-research.md and ../adr/ADR-0001-repository-purpose.md.
