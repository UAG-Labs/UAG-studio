# Plan: PLAN-106 - Compiler Diagnostics and Exports

**Status:** Draft
**Repo Scope:** `UAG-studio`

## Goal
Integrate compiler results, diagnostics, source maps, loss reports, and export UX.

## Tasks
1. Call compiler through Rust/Tauri engine or stable library boundary.
2. Display compile status, diagnostics, source-map links, and stale result state.
3. Display loss reports with preserved, omitted, degraded, category, fidelity, and remediation.
4. Add export target picker based on compiler capability data.
5. Block or warn on policy-sensitive AI/public exports.

## Success Criteria
1. Compile does not freeze UI.
2. Diagnostics navigate to object, source path, package issue, or artifact.
3. Loss reports are visible even when export succeeds.
4. Export UX reflects compiler-supported targets.
