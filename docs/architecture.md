# Architecture — UAG-studio

## Boundary
Studio owns UI and local app integration. It does not define language semantics or compiler internals.

## App Shells
- `apps/desktop`: Tauri desktop app.
- `apps/web`: optional web app.

## Packages
- `ui`: shared components.
- `graph-canvas`: React Flow canvas.
- `editor-core`: state and mutations.
- `inspectors`: property editors.
- `panels`: UI panels.
- `bindings`: compiler/Tauri/type wrappers.

## Rust Engine
`rust/studio-engine` handles local project IO, compiler calls, graph queries, and package file handling.
