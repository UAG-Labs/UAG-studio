# Plan: PLAN-102 - Project State and Bindings

**Status:** Draft
**Repo Scope:** `UAG-studio`

## Goal
Implement testable state and type boundaries.

## Tasks
1. Implement project, graph, view, layout, selection, diagnostics, compile-result, export-result, policy, and recent-file stores.
2. Add mutation functions for semantic edits and layout edits.
3. Add bindings for core/compiler data shapes.
4. Add stale compile-result tracking.
5. Add undo/redo for editor mutations.

## Success Criteria
1. State mutations are unit-tested.
2. Semantic changes and layout changes are separate.
3. Compile snapshots are immutable and revision-linked.
4. Unknown or unsupported compiler payloads fail safely.
