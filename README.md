<p align="center">
  <img src="./public/banners/uag-labs-readme-banner.svg" alt="UAG-studio banner" />
</p>

# UAG-studio

**The human trust and inspection layer for the UAG graph-native architecture compiler platform.**

Studio is not a diagramming tool. It is the interface through which humans read, understand, and approve architecture graphs. AI systems and the compiler operate on the graph directly — Studio is what makes that legible and trustworthy for humans.

## Role in the System

```text
Human intent
→ Studio (create / inspect / approve graph)
→ TAKG saved to disk
→ UAG-compiler (policy engine → validate → lower → emit)
→ Generated output (code, diagrams, contracts, CI/CD)
→ Studio displays output read-only
→ Developer intent flows back through the graph, never through editing generated output
```

The compiled output is read-only in Studio. All changes flow back through the graph.

## Stack

- React + TypeScript — canvas, inspectors, panels
- React Flow — graph canvas interaction
- Vite — dev build
- Tauri — desktop app shell
- Rust — Studio engine (project IO, compiler calls, graph queries)
- UAG-core — canonical graph types
- UAG-compiler — compile, validate, emit, diff, query

## What Studio Owns

- **Graph canvas** — visual editing of TAKG: nodes, edges, events, capabilities, resources, constraints, goals
- **Behavior layer editors** — per-capability state machine editor, predicate builder, effect/transformation editors, hole contract viewer
- **Property inspector** — per-node type-aware property editing
- **Policy config panel** — review and edit the active policy file (naming conventions, adapter bindings)
- **Compiler panel** — trigger compilation, view active targets, see compilation readiness status
- **Diagnostics panel** — errors, warnings, loss reports per emitter
- **Loss report panel** — per-node loss report showing what semantics each target could not express
- **Output viewer** — read-only display of generated code, diagrams, and configs
- **Validation panel** — architectural validity check results
- **Hole registry** — list of all Hole nodes, their contracts, and their adapter bindings
- **Project explorer** — file/package management for multi-file TAKG projects
- **Search panel** — query graph by node type, capability, constraint, gap

## Native Editing Format

Studio edits TAKG. UAGL is compiled output — Studio may display it read-only. Studio never writes UAGL directly.

## Trust Model

Humans approve architecture through Studio. AI agents may modify the TAKG graph programmatically, but Studio is the required checkpoint for human review before compilation drives generated output. Studio surfaces:

- What the graph encodes (structural view)
- What the compiler will emit (compilation readiness, target status)
- What was dropped (loss reports)
- What is missing (holes, gaps, unbound adapters)

## Event-Driven Compilation

Studio supports live, reactive compilation. When a graph node changes, Studio triggers incremental recompilation via UAG-compiler. Only affected output files are regenerated. On a 50-node graph with one changed node, this completes in under one second.
