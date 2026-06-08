# Architecture — UAG-studio

## Identity
UAG-studio is the human trust and inspection layer of the UAG compiler platform. It is the only place humans directly read and modify the architecture graph. AI agents and the compiler operate on the graph programmatically; Studio makes that legible, inspectable, and trustworthy for humans.

Studio is not a diagramming tool. It is a graph editor backed by a compiler.

## Boundary
Studio owns the UI, desktop/web shells, and the Rust Studio engine. It does not define language semantics, compiler internals, or policy rules. It calls UAG-compiler for everything compilation-related and reads UAG-core types for everything graph-related.

## Trust Model

```text
Human reads/approves → Studio (graph canvas + property inspector + diagnostics)
Human edits → TAKG modified via Studio
TAKG changes → Studio triggers incremental recompilation via UAG-compiler
Compiler output → displayed read-only in Studio
Loss reports → displayed per node per emitter
Holes → visible with full contract; adapter routing visible but implementation is in adapter
```

The generated output is always read-only in Studio. A developer who wants to change what the compiler generates must change the graph. There is no escape hatch to edit generated code.

## App Shells

```text
apps/desktop    Tauri desktop app — full native integration, local file access
apps/web        Optional web app — remote project access, reduced local IO
```

## Package Structure

```text
packages/
  ui/             shared React components (buttons, panels, overlays, etc.)
  graph-canvas/   React Flow canvas — node rendering, edge routing, selection, pan/zoom
  editor-core/    graph state, TAKG mutations, undo/redo, validation triggers
  inspectors/     per-node-type property editors — one inspector per primitive type
  panels/         UI panels: compiler, diagnostics, loss report, holes, output, search
  bindings/       UAG-compiler Tauri command wrappers, UAG-core TypeScript type bindings
```

## Rust Studio Engine (`rust/studio-engine`)

The studio-engine is the Rust layer that Studio's frontend talks to via Tauri commands. It handles:

- Local project IO — reading and writing `.takg.yaml` files and packages
- Compiler calls — invoking UAG-compiler and streaming results back to the frontend
- Graph queries — `uag query` commands for holes, gaps, node lookup
- Graph diff — `uag diff` between versions
- Incremental recompilation triggers — watching for graph file changes and firing targeted re-emit

The studio-engine does not implement any compiler or policy logic. It is a thin, fast integration layer.

## UI Panels

**Graph canvas** — visual editing of all 7 TAKG primitives. Each primitive type has a distinct visual representation. Edges carry type labels (call, event, data flow). Constraint and Goal nodes are visually distinct and annotated with enforcement level.

**Property inspector** — type-aware editor for the focused node. For a `Capability`, shows state machine summary. For a `Constraint`, shows enforcement mode. For a `Hole`, shows full typed contract (inputs, outputs, invariants) and adapter binding status.

**Behavior layer editors:**
- State machine editor — per-capability state/transition diagram with guard and effect editing
- Predicate builder — visual tree editor for typed boolean expressions
- Effect/transformation editors — typed resource operation and dataflow pipeline editors
- Hole contract viewer — read-only contract display; adapter binding status

**Policy config panel** — displays the active policy file. Allows editing naming conventions and adapter bindings. Changes here affect compilation targets without changing the graph structure.

**Compiler panel** — active targets, compilation readiness status per target, trigger full or incremental recompilation. Shows which nodes have changed since last compile. Shows the exact missing information for each compilation readiness failure.

**Diagnostics panel** — all compiler errors, warnings, and loss entries. Filterable by level, emitter, and node.

**Loss report panel** — per-node per-emitter view of what graph semantics each target could not express. No semantic is silently dropped.

**Hole registry** — all `Hole` nodes in the active graph. For each: name, typed contract, invariants, adapter binding (or missing). Unbound holes are highlighted as compilation blockers.

**Output viewer** — read-only file tree and viewer for all generated output (code, diagrams, CI/CD configs). Syntax-highlighted, non-editable.

**Search panel** — full graph search by node type, name, capability, constraint, gap. Surfaces all compilation readiness gaps with direct navigation to the relevant nodes.

## Event-Driven Incremental Recompilation

When any TAKG node is saved, Studio triggers incremental recompilation via UAG-compiler. The compiler uses its node hash manifest to identify which nodes changed and re-emits only their affected outputs. On a 50-node graph, one changed node recompiles in under one second. Studio streams the result back to the relevant panels without a full UI reload.

This enables a live editing loop: change a node → see updated diagnostics and output in real time.
