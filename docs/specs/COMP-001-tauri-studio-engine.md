# Spec: COMP-001 — Tauri Studio Engine

**Spec ID:** COMP-001
**Type:** Component
**Status:** Draft
**Date:** 2026-06-08
**Author:** Agent

## 1. Overview
1.1 Purpose — Specifies Rust local engine for file IO, compiler integration, and graph inspection.
1.2 Context — React frontend should not own filesystem/compiler system behavior.
1.3 Related artifacts
   1.3.A ADR: [ADR-0001 Repository Purpose](../adr/ADR-0001-repository-purpose.md)
   1.3.B Research: [Research Summary](../research/initial-research.md)
   1.3.C Open questions: [Open Questions](../open-questions.md) — none unresolved in this initialized package.
   1.3.D Plan: [Bootstrap Plan](../plans/PLAN-001-bootstrap.md)

## 2. Scope
2.1 Goals
   2.1.A Expose Tauri commands.
   2.1.B Open/save files.
   2.1.C Call compiler.
   2.1.D Return diagnostics.
2.2 Non-Goals (out of scope)
   2.2.A Does not implement React UI.
   2.2.B Does not redefine core model.
   2.2.C Does not contain compiler logic beyond integration.

## 3. Requirements
3.1 Functional requirements
   3.1.A Engine must expose open/save/compile/validate/export/inspect.
   3.1.B Engine must use UAG-core/UAG-compiler types.
   3.1.C Errors serialize to frontend.
3.2 Non-functional requirements
   3.2.A Commands must not block UI unnecessarily.
   3.2.B File writes safe and explicit.

## 4. Interface / Data
4.1 Type-specific detail
   4.1.A Inputs are command payloads.
   4.1.B Outputs are serializable responses.

## 5. Behavior
5.1 Happy path
   5.1.A Frontend invokes command.
   5.1.B Rust performs operation.
   5.1.C Response returns.
5.2 Edge cases
   5.2.A Compiler diagnostics pass through.
   5.2.B Invalid paths return safe errors.
5.3 Error states
   5.3.A Filesystem permission error returns command error.
   5.3.B Compiler panic converted to failure if recoverable.

## 6. Acceptance Criteria
6.1 Criteria
   6.1.A [ ] Open command exists (verifies §3.1.A) — Verified by: [—]
   6.1.B [ ] Compile command exists (verifies §3.1.A) — Verified by: [—]
   6.1.C [ ] Errors serialize (verifies §3.1.C) — Verified by: [—]

## 7. Open Questions & Assumptions
7.1 Open questions — No unresolved open questions are allowed in this initialized documentation package. Future uncertainty must be recorded in [Open Questions](../open-questions.md) before implementation continues.
7.2 Assumptions
   7.2.A Tauri is desktop integration. — Validated: ../research/initial-research.md and ../adr/ADR-0001-repository-purpose.md.
