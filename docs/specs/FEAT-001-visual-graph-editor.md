# Spec: FEAT-001 — Visual Graph Editor

**Spec ID:** FEAT-001
**Type:** Feature
**Status:** Draft
**Date:** 2026-06-08
**Author:** Agent

## 1. Overview
1.1 Purpose — Specifies user-facing graph editing.
1.2 Context — Users need typed nodes and relationships without writing YAML first.
1.3 Related artifacts
   1.3.A ADR: [ADR-0001 Repository Purpose](../adr/ADR-0001-repository-purpose.md)
   1.3.B Research: [Research Summary](../research/initial-research.md)
   1.3.C Open questions: [Open Questions](../open-questions.md) — none unresolved in this initialized package.
   1.3.D Plan: [Bootstrap Plan](../plans/PLAN-001-bootstrap.md)

## 2. Scope
2.1 Goals
   2.1.A Create nodes.
   2.1.B Create relationships.
   2.1.C Select objects.
   2.1.D Edit properties.
2.2 Non-Goals (out of scope)
   2.2.A Does not implement every renderer.
   2.2.B Does not implement collaboration.

## 3. Requirements
3.1 Functional requirements
   3.1.A Editor must render typed nodes.
   3.1.B Editor must render typed relationships.
   3.1.C Editor must update TAKG.
   3.1.D Editor must separate layout from semantic data.
3.2 Non-functional requirements
   3.2.A Interactions responsive for MVP graphs.
   3.2.B Invalid states must not crash.

## 4. Interface / Data
4.1 Type-specific detail
   4.1.A Inputs are UI gestures.
   4.1.B Outputs are TAKG mutations.

## 5. Behavior
5.1 Happy path
   5.1.A User creates BackendService.
   5.1.B User connects Database.
   5.1.C Inspector edits properties.
5.2 Edge cases
   5.2.A Dangling edge is cancelled or diagnosed.
   5.2.B Moving node changes layout only.
5.3 Error states
   5.3.A Invalid relationship shows warning.
   5.3.B Missing property marks object incomplete.

## 6. Acceptance Criteria
6.1 Criteria
   6.1.A [ ] Node creation updates TAKG (verifies §3.1.A) — Verified by: [—]
   6.1.B [ ] Relationship creation updates TAKG (verifies §3.1.B) — Verified by: [—]
   6.1.C [ ] Layout separate (verifies §3.1.D) — Verified by: [—]

## 7. Open Questions & Assumptions
7.1 Open questions — No unresolved open questions are allowed in this initialized documentation package. Future uncertainty must be recorded in [Open Questions](../open-questions.md) before implementation continues.
7.2 Assumptions
   7.2.A React Flow is canvas library. — Validated: ../research/initial-research.md and ../adr/ADR-0001-repository-purpose.md.
