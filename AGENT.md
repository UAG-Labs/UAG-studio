# AGENT.md — Codex Context for `UAG-studio`

## Repository Identity
Repository: `UAG-studio`  
Organization: `UAG-Labs`  
GitHub description: React and Rust visual architecture graph editor for creating, validating, and exporting UAG projects.

## Non-Negotiable Rule
The graph is the source of truth. The diagram is a view. The export is a projection.

## Role
Visual editor application owning React canvas, inspectors, panels, desktop/web shells, and Rust Studio engine integration.

## Technology
React + TypeScript frontend, React Flow canvas, Tauri desktop shell, Rust system-level Studio engine.

## Dependency Boundary
Depends on UAG-core for types and UAG-compiler for compile/validate/export.

## Expected Output
Visual editor that creates/edits TAKG, calls compiler, displays diagnostics, and exports artifacts.

## Working Instructions
1. Read `README.md`, `docs/architecture.md`, `docs/artifact.md`, `docs/REPOSITORY_STRUCTURE.md`, and `docs/specs/README.md` before implementation.
2. Add or update specs using `docs/procedures/add-specification-file.md`.
3. Do not implement undocumented behavior.
4. Do not create unresolved implementation questions. Record blockers in `docs/open-questions.md` and stop.
5. Preserve TAKG as editable source graph and UAGL as compiled IR.
6. Keep generated output deterministic wherever possible.
7. Keep repo responsibilities inside this repo's boundary.
