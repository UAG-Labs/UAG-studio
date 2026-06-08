# Plan: PLAN-002 - Studio Authoring Slice

**Status:** Draft
**Derived From:** ../specs/SYS-001-studio-application.md, ../specs/FEAT-001-visual-graph-editor.md, ../specs/FEAT-002-project-open-save.md, ../specs/FEAT-003-compile-validate-export-ui.md, ../specs/DATA-001-studio-project-state.md, ../specs/COMP-001-tauri-studio-engine.md
**Derivation Status:** Current

## Objective
Implement the first usable Studio loop: open a TAKG fixture, display a semantic view, edit graph/layout through an adapter, save deterministic TAKG, call the compiler, and display diagnostics/loss reports without leaking canvas state into language semantics.

## Preconditions
1. `UAG-core` exposes generated schemas and TypeScript/Rust-friendly model contracts or bindings.
2. `UAG-compiler` exposes a stable compile-result JSON shape or Rust library command boundary.
3. At least one canonical TAKG fixture from `UAG` is available.

## Work Packages
| Work Package | Scope | Primary Specs | Exit Criteria |
|---|---|---|---|
| WP1 Workspace skeleton | Create `apps/desktop`, `packages/editor-core`, `packages/graph-canvas`, `packages/ui`, `packages/bindings`, and `rust/studio-engine`. | SYS-001 | Build tooling discovers packages. |
| WP2 Project state | Implement stores for graph, active view, layout, selection, diagnostics, compile result, policy, dirty state, and recent files. | DATA-001 | State mutations are unit-tested. |
| WP3 TAKG/canvas adapter | Map TAKG views into React Flow nodes/edges and keep canvas fields out of semantics. | FEAT-001 | Moving a node changes layout only. |
| WP4 Open/save | Open `.takg.yaml`, preserve partial-invalid state, save deterministic TAKG, and open `.uagl.yaml` read-only. | FEAT-002 | Fixture round-trip preserves semantics. |
| WP5 Inspector editing | Edit entity and relationship fields including protocol, mode, cardinality, data, auth, and failure behavior. | FEAT-001 | Edited fields serialize to TAKG. |
| WP6 Compiler bridge | Call compiler through Rust/Tauri engine or library boundary and store immutable compile snapshots. | COMP-001, FEAT-003 | Compile result appears without freezing UI. |
| WP7 Diagnostics/loss UI | Show diagnostics, source-map navigation, hidden-object/package-level diagnostics, and loss report details. | FEAT-003 | User can navigate from diagnostic to affected object or panel. |
| WP8 Policy-aware export affordance | Warn or block AI/public exports based on classification/redaction policy. | FEAT-003 | Policy warning appears before export. |

## Suggested Layout
```text
apps/desktop/
packages/
  editor-core/
  graph-canvas/
  ui/
  bindings/
rust/studio-engine/
```

## Test Plan
1. Unit tests for editor-core mutations.
2. Adapter tests proving layout and semantics stay separate.
3. Open/save fixture round-trip tests.
4. Compile-result fixture display tests.
5. Diagnostics navigation tests.
6. Policy warning tests for AI/public export paths.

## Dependencies
1. Compiler compile-result contract.
2. Core schema/model contract.
3. React Flow adapter boundary.
4. Tauri file IO and compiler command bridge.

## Risks
1. Building UI before model/compiler contracts stabilize will cause churn.
2. Treating canvas handles as semantics would corrupt TAKG.
3. Importing UAGL too early could lose author intent.

## Exit Criteria
1. User can open, inspect, edit, save, compile, and view diagnostics for one canonical TAKG fixture.
2. UAGL opens read-only.
3. Layout-only edits do not alter semantic TAKG objects.
4. Compiler diagnostics and loss reports display with source-map navigation.
5. Studio can continue planning broader UX without changing language semantics.
