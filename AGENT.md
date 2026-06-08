# AGENT.md — Context for `UAG-studio`

## Repository Identity
Repository: `UAG-studio`
Organization: `UAG-Labs`
Role: Human trust and inspection layer — visual graph editor, compiler panel, diagnostics display, read-only output viewer.

## Non-Negotiable Rules
- The architecture graph is the source of truth.
- The diagram is a view.
- The export is a projection.
- The code is a compilation target.
- Studio is NOT a diagramming tool. It is the human trust layer for a graph-native architecture compiler.
- Generated output is read-only in Studio. All developer intent flows through the graph, never through editing generated code.
- Studio edits TAKG. Studio never writes UAGL directly.
- Hole contracts, constraint nodes, and goal nodes are visible in Studio but their implementation is in adapters — Studio shows the contract, not the implementation.
- Studio surfaces loss reports for every emitter. Hiding loss is not an option.
- Event-driven incremental recompilation must be supported. Graph changes trigger targeted re-emit, not full recompilation.

## Technology
React + TypeScript frontend, React Flow canvas, Tauri desktop shell, Rust Studio engine.

## Dependency Boundary
Depends on UAG-core for types. Depends on UAG-compiler for compile, validate, emit, diff, query. Does not depend on any other sibling repo.

## Expected Output
- Visual canvas for editing all 7 TAKG primitives: nodes, edges, events, capabilities, resources, constraints, goals
- Behavior layer editors: state machine editor, predicate builder, effect/transformation editors, hole contract viewer
- Policy config panel for reviewing and editing naming conventions and adapter bindings
- Compiler panel: trigger compilation, view target status, compilation readiness gaps
- Diagnostics panel: errors, warnings, loss reports
- Loss report panel: per-node per-emitter loss detail
- Output viewer: read-only display of generated code, diagrams, CI/CD configs
- Hole registry: all Hole nodes with contract details and adapter routing
- Event-driven incremental recompilation integration

## Working Instructions
1. Read `README.md`, `docs/architecture.md`, `docs/artifact.md`, `docs/REPOSITORY_STRUCTURE.md`, and `docs/specs/README.md` before any work.
2. Add or update specs using `docs/procedures/add-specification-file.md`.
3. Do not implement undocumented behavior.
4. Do not create unresolved questions. Record blockers in `docs/open-questions.md` and stop.
5. Preserve the trust model: Studio is for human inspection and approval. Generated output is always read-only in Studio.
6. Keep compiler integration clean — Studio calls UAG-compiler, it does not duplicate compiler logic.
7. Keep repo responsibilities inside this repo's boundary.
