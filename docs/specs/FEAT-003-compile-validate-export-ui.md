# Spec: FEAT-003 - Compile Validate Export UI

**Spec ID:** FEAT-003
**Type:** Feature
**Status:** Draft
**Date:** 2026-06-08
**Author:** Agent

## 1. Overview
1.1 Purpose - Specifies UI for compiler, validation, export, diagnostics, and loss reports.
1.2 Context - Studio must expose compiler value inside editor.
1.3 Related artifacts
   1.3.A ADR: [ADR-0001 Repository Purpose](../adr/ADR-0001-repository-purpose.md)
   1.3.B Research: [Research Summary](../research/initial-research.md)
   1.3.C Open questions: [Open Questions](../open-questions.md) - none unresolved in this initialized package.
   1.3.D Plan: [Bootstrap Plan](../plans/PLAN-001-bootstrap.md)

## 2. Scope
2.1 Goals
   2.1.A Add compile button.
   2.1.B Add validation panel.
   2.1.C Add export panel.
   2.1.D Add diagnostics and loss reports.
   2.1.E Add source-map navigation from diagnostics to canvas objects and source paths.
2.2 Non-Goals (out of scope)
   2.2.A Does not implement compiler algorithms.
   2.2.B Does not define exporter syntax.

## 3. Requirements
3.1 Functional requirements
   3.1.A Studio must call UAG-compiler.
   3.1.B Studio must show affected diagnostics.
   3.1.C Studio must show loss reports with preserved, omitted, degraded, category, fidelity, and remediation details.
   3.1.D Studio must select export target.
   3.1.E Studio must display stale compile results after graph edits without treating them as current.
   3.1.F Studio must apply classification/redaction policy warnings before AI context or public exports.
   3.1.G Studio must display runtime observations as overlays and drift diagnostics, not as editable TAKG entities.
3.2 Non-functional requirements
   3.2.A Compiler calls must not freeze UI.
   3.2.B Errors must be actionable.
   3.2.C Large result sets must be filterable by severity, category, stage, source object, and active view.

## 4. Interface / Data
4.1 Type-specific detail
   4.1.A Inputs are current TAKG/options.
   4.1.B Outputs are UAGL/diagnostics/source maps/artifacts/loss reports.
   4.1.C UI consumes the same machine-readable compile result shape exposed by the CLI.
   4.1.D Diagnostics can navigate to canvas object, source path, package-level panel, or export artifact depending on affected ref type.

## 5. Behavior
5.1 Happy path
   5.1.A User clicks compile.
   5.1.B Compiler returns result.
   5.1.C Studio displays diagnostics and source-map links.
   5.1.D User exports target.
5.2 Edge cases
   5.2.A Warnings allow output unless strict.
   5.2.B Strict failure prevents export.
   5.2.C Loss report can be non-empty even when export succeeds.
5.3 Error states
   5.3.A Compiler failure shows error.
   5.3.B Unsupported target lists options.
   5.3.C Export blocked by policy explains required redaction or classification change.

## 6. Acceptance Criteria
6.1 Criteria
   6.1.A [ ] Compile action calls compiler (verifies 3.1.A) - Verified by: [--]
   6.1.B [ ] Diagnostics show refs (verifies 3.1.B) - Verified by: [--]
   6.1.C [ ] Loss report displays omissions (verifies 3.1.C) - Verified by: [--]
   6.1.D [ ] Source-map navigation exists (verifies 2.1.E) - Verified by: [--]
   6.1.E [ ] Policy warning appears before AI/public export (verifies 3.1.F) - Verified by: [--]

## 7. Open Questions & Assumptions
7.1 Open questions - No unresolved open questions are allowed in this initialized documentation package. Future uncertainty must be recorded in [Open Questions](../open-questions.md) before implementation continues.
7.2 Assumptions
   7.2.A Compiler callable from Studio through Rust/Tauri. - Validated: ../research/initial-research.md and ../adr/ADR-0001-repository-purpose.md.
