# Open Questions - `UAG-studio`

## Status
All initial audit questions have been answered for planning purposes. Future editor/product uncertainty should be added as new open questions.

## Research Basis
- React Flow models interactive flowgraphs as nodes, handles, edges, connection lines, and viewport state: https://reactflow.dev/learn/concepts/introduction
- Tauri commands expose Rust functions to the frontend through an invoke/command system: https://v1.tauri.app/v1/guides/features/command/
- Structurizr distinguishes source and compiled workspace files, with compiled representation including layout/editor data: https://docs.structurizr.com/workspaces/file-types
- D2 and Structurizr demonstrate that layout/export fidelity is a separate concern from semantic source modeling: https://d2lang.com/tour/intro and https://docs.structurizr.com/dsl/language

## Question Format
```markdown
## Q-001 - Title
Status: Open | Resolved
Raised by:
Question:
Why it matters:
Options:
Impacts:
Decision needed before:
Resolution evidence:
```

## Q-001 - What is the first supported Studio project format?
Status: Resolved
Raised by: Audit of project open/save specs and compiler package questions.
Question: Does Studio open a single `.takg.yaml`, a project directory, a future `.uagpkg`, or all three?
Why it matters: Open/save behavior drives UI, Rust engine APIs, examples, and user workflows.
Options:
- Single TAKG file first.
- Directory project with manifest and assets.
- Package-first workflow using `.uagpkg`.
AI recommendation: Support single `.takg.yaml` first, then add project directories once assets/layout sidecars are needed. Defer `.uagpkg` authoring until compiler package semantics are stable.
Decision: Support single `.takg.yaml` first, then add project directories once assets/layout sidecars are needed. Defer `.uagpkg` authoring until compiler package semantics are stable.
Impacts: Tauri engine, project explorer, compiler integration, docs.
Decision needed before: Implementing open/save.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-002 - How should Studio represent invalid or partial TAKG?
Status: Resolved
Raised by: Studio must tolerate invalid TAKG; compiler may reject unresolved references.
Question: What state model lets users edit incomplete graphs while still seeing compiler diagnostics?
Why it matters: Architecture editing is iterative; the app cannot require a fully valid graph after every click.
Options:
- Store partial graph state separately and serialize only when valid.
- Save TAKG with unresolved references and compiler diagnostics.
- Maintain a local draft layer over last valid TAKG.
AI recommendation: Save TAKG with unresolved references and compiler diagnostics. The editor should preserve draft intent instead of blocking saves until the graph is valid.
Decision: Save TAKG with unresolved references and compiler diagnostics. The editor should preserve draft intent instead of blocking saves until the graph is valid.
Impacts: State model, save behavior, compiler calls, diagnostics panel.
Decision needed before: Editor core implementation.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-003 - What maps React Flow nodes/handles/edges to TAKG semantics?
Status: Resolved
Raised by: React Flow research and visual graph editor spec.
Question: Are React Flow nodes direct wrappers around TAKG entities, or does Studio maintain a view adapter between semantic graph objects and canvas objects?
Why it matters: Canvas libraries have UI concepts like handles and viewport that should not leak into language semantics.
Options:
- One React Flow node per TAKG entity and edge per relationship.
- Adapter layer maps TAKG views to canvas nodes/edges/handles.
- Canvas graph is view-specific and generated from TAKG plus layout metadata.
AI recommendation: Use an adapter layer between TAKG views and React Flow nodes/edges/handles so canvas implementation details never become language semantics.
Decision: Use an adapter layer between TAKG views and React Flow nodes/edges/handles so canvas implementation details never become language semantics.
Impacts: Graph canvas package, layout persistence, compiler cleanliness, future canvas migration.
Decision needed before: Graph canvas implementation.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-004 - Where does layout live?
Status: Resolved
Raised by: TAKG layout requirement and source/compiled separation research.
Question: Does layout live in TAKG, Studio-only metadata, per-view layout files, or a project package?
Why it matters: Users expect layouts to persist, while UAGL must stay semantic and deterministic.
Options:
- TAKG includes layout under explicit `layouts`.
- Studio stores layout separately from TAKG.
- Project/package stores semantic TAKG and layout sidecar files.
AI recommendation: Store layout in explicit TAKG `layouts` metadata for milestone one, scoped by view ID, and keep it excluded from UAGL during compilation.
Decision: Store layout in explicit TAKG `layouts` metadata for milestone one, scoped by view ID, and keep it excluded from UAGL during compilation.
Impacts: TAKG schema, save/load, diff behavior, compiler input.
Decision needed before: First save/load implementation.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-005 - How does Studio call the compiler?
Status: Resolved
Raised by: Tauri command research and Studio engine spec.
Question: Does Studio link the compiler as a Rust library, invoke a CLI binary, call a background service, or support multiple modes?
Why it matters: This affects performance, error handling, packaging, version compatibility, and development workflow.
Options:
- Direct Rust library call from `studio-engine`.
- Spawn `uag` CLI as a child process.
- Use a long-running compiler worker/service.
AI recommendation: Call the compiler as a Rust library from `studio-engine` first. Keep the CLI invocation path as an integration fallback for later debugging and version testing.
Decision: Call the compiler as a Rust library from `studio-engine` first. Keep the CLI invocation path as an integration fallback for later debugging and version testing.
Impacts: Tauri commands, packaging, logs, diagnostics, cross-platform behavior.
Decision needed before: Tauri engine implementation.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-006 - What is the frontend/backend command boundary?
Status: Resolved
Raised by: Tauri command model.
Question: Which operations are Tauri/Rust commands versus pure frontend state mutations?
Why it matters: Filesystem, compiler execution, and project packages belong in Rust, while immediate UI edits need fast frontend state.
Options:
- Rust owns open/save/compile/export; frontend owns editing state.
- Rust owns all graph mutations to preserve type safety.
- Frontend owns all editing and sends snapshots to Rust for persistence/compile.
AI recommendation: Frontend owns immediate graph editing, selection, undo/redo, and viewport; Rust owns open/save/compile/export/package operations through typed commands.
Decision: Frontend owns immediate graph editing, selection, undo/redo, and viewport; Rust owns open/save/compile/export/package operations through typed commands.
Impacts: Performance, testability, undo/redo, IPC schema, error handling.
Decision needed before: Studio engine API.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-007 - What is the first useful node palette?
Status: Resolved
Raised by: Core dialect questions and Studio UI areas.
Question: Which object kinds should users be able to create in the first Studio milestone?
Why it matters: The palette reveals the language model and must align with official dialects.
Options:
- Core-only entities, relationships, boundaries, views.
- Core plus AI-agent, service/API, database, queue, infrastructure starter kinds.
- Palette generated from loaded dialect registry.
AI recommendation: Generate the node palette from the loaded dialect registry, but ship a curated core palette first so the UI can be useful before dialect authoring is complete.
Decision: Generate the node palette from the loaded dialect registry, but ship a curated core palette first so the UI can be useful before dialect authoring is complete.
Impacts: Dialect model, UI design, examples, validation.
Decision needed before: Visual editor implementation.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-008 - How should diagnostics appear on the canvas?
Status: Resolved
Raised by: Studio diagnostics requirements and compiler source-map questions.
Question: How are diagnostics associated with nodes, edges, views, package-level issues, and export losses?
Why it matters: Diagnostics must be actionable, not just text in a panel.
Options:
- Panel-only diagnostics.
- Canvas badges plus details panel.
- Source-map-driven selection, highlighting, and quick fixes.
AI recommendation: Use canvas badges plus a diagnostics panel, backed by compiler source maps. Package-level diagnostics should appear only in the panel.
Decision: Use canvas badges plus a diagnostics panel, backed by compiler source maps. Package-level diagnostics should appear only in the panel.
Impacts: Compiler source map, UI components, accessibility, user workflow.
Decision needed before: Diagnostics UI implementation.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-009 - What does read-only/import UAGL mean?
Status: Resolved
Raised by: Studio specs say UAGL can be opened read-only or imported.
Question: What user actions are allowed when opening UAGL, and how does import reconstruct editable TAKG or layout?
Why it matters: UAGL lacks draft/editor state by design, so import may be lossy or impossible for some graphs.
Options:
- UAGL opens only as read-only inspection.
- UAGL imports into TAKG with generated layout and loss report.
- UAGL import is deferred until compiler round-trip semantics are defined.
AI recommendation: Open UAGL as read-only inspection first. Defer import-to-TAKG until the compiler can emit a trustworthy reverse/loss report.
Decision: Open UAGL as read-only inspection first. Defer import-to-TAKG until the compiler can emit a trustworthy reverse/loss report.
Impacts: File open UI, compiler API, loss reports, layout generation.
Decision needed before: UAGL open/import implementation.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Q-010 - What is the first app target: desktop only or web plus desktop?
Status: Resolved
Raised by: Architecture mentions `apps/desktop` and optional `apps/web`.
Question: Should the first implementation build only Tauri desktop, or maintain a web app target from day one?
Why it matters: Web support constrains filesystem access, compiler execution, package handling, and authentication/security assumptions.
Options:
- Desktop-only first milestone.
- Shared frontend with desktop implementation first and web mocked adapters.
- Full desktop and web parity from the start.
AI recommendation: Build desktop-only first with a clean adapter boundary, then add a web target once project IO and compiler execution abstractions are stable.
Decision: Build desktop-only first with a clean adapter boundary, then add a web target once project IO and compiler execution abstractions are stable.
Impacts: Workspace layout, adapter layer, CI, user docs.
Decision needed before: App scaffold.
Resolution evidence: [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md)

## Resolved Initialization Decisions
- R-001: Repos are `UAG`, `UAG-core`, `UAG-compiler`, and `UAG-studio`.
- R-002: Rust is used for system-level implementation.
- R-003: React + TypeScript are used for Studio frontend.
- R-004: TAKG is editable source; UAGL is compiled IR.
- R-005: All specs follow fixed `TYPE-NNN-name.md` naming and seven-section format.
