# Spec: FEAT-002 - Project Open Save

**Spec ID:** FEAT-002
**Type:** Feature
**Status:** Draft
**Date:** 2026-06-08
**Author:** Agent

## 1. Overview
1.1 Purpose - Specifies project file open/save.
1.2 Context - Users need reliable `.takg.yaml`, `.uagl.yaml`, and future `.uagpkg` workflows.
1.3 Related artifacts
   1.3.A ADR: [ADR-0001 Repository Purpose](../adr/ADR-0001-repository-purpose.md)
   1.3.B Research: [Research Summary](../research/initial-research.md)
   1.3.C Open questions: [Open Questions](../open-questions.md) - none unresolved in this initialized package.
   1.3.D Plan: [Bootstrap Plan](../plans/PLAN-001-bootstrap.md)

## 2. Scope
2.1 Goals
   2.1.A Open TAKG.
   2.1.B Save TAKG.
   2.1.C Open UAGL read-only/import.
   2.1.D Track recent projects.
   2.1.E Preserve package/import metadata, unknown compatible fields, and policy fields.
2.2 Non-Goals (out of scope)
   2.2.A Does not implement cloud sync.
   2.2.B Does not implement collaboration.
   2.2.C Does not implement `.uagdb` MVP.

## 3. Requirements
3.1 Functional requirements
   3.1.A Studio must open `.takg.yaml` editable.
   3.1.B Studio must save deterministic TAKG.
   3.1.C Studio must warn before overwrite.
   3.1.D Studio must not silently drop unknown fields.
   3.1.E Studio must preserve invalid/partial TAKG and compiler diagnostics.
   3.1.F Studio must open `.uagl.yaml` read-only and defer import-to-TAKG until reverse loss reports exist.
   3.1.G Studio must validate package/import namespace collisions before save when schemas are available.
3.2 Non-functional requirements
   3.2.A File IO uses Rust/Tauri desktop.
   3.2.B Unsaved changes tracked.
   3.2.C Save output must be canonical enough to avoid unnecessary diffs.

## 4. Interface / Data
4.1 Type-specific detail
   4.1.A Inputs are paths and commands.
   4.1.B Outputs are saved files and UI state.
   4.1.C File metadata includes file kind, schema version, compatibility, package ID, namespace, dirty state, and read-only status.

## 5. Behavior
5.1 Happy path
   5.1.A User opens file.
   5.1.B Studio parses TAKG.
   5.1.C Graph appears.
   5.1.D User saves.
5.2 Edge cases
   5.2.A Opening UAGL prompts read-only/import.
   5.2.B Unknown version warns.
   5.2.C Schema unavailable allows open but records a compatibility warning.
5.3 Error states
   5.3.A Read failure shows error.
   5.3.B Write failure leaves dirty state.
   5.3.C Unknown field that cannot be preserved blocks save unless user exports a sanitized copy.

## 6. Acceptance Criteria
6.1 Criteria
   6.1.A [ ] Editable TAKG open works (verifies 3.1.A) - Verified by: [--]
   6.1.B [ ] Save writes TAKG (verifies 3.1.B) - Verified by: [--]
   6.1.C [ ] UAGL direct edit prevented/imported (verifies 3.1.C) - Verified by: [--]
   6.1.D [ ] Partial TAKG save preserves diagnostics (verifies 3.1.E) - Verified by: [--]
   6.1.E [ ] Unknown compatible fields are preserved or diagnosed (verifies 3.1.D) - Verified by: [--]

## 7. Open Questions & Assumptions
7.1 Open questions - No unresolved open questions are allowed in this initialized documentation package. Future uncertainty must be recorded in [Open Questions](../open-questions.md) before implementation continues.
7.2 Assumptions
   7.2.A Desktop file IO uses Tauri/Rust. - Validated: ../research/initial-research.md and ../adr/ADR-0001-repository-purpose.md.
