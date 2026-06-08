# Plan: PLAN-101 - Workspace and App Shell

**Status:** Draft
**Repo Scope:** `UAG-studio`

## Goal
Create the Studio workspace and runnable desktop shell.

## Tasks
1. Create `apps/desktop`.
2. Create packages for `editor-core`, `graph-canvas`, `ui`, `bindings`, `inspectors`, and `panels`.
3. Create `rust/studio-engine`.
4. Wire Vite, Tauri, TypeScript, lint, test, and build commands.
5. Add empty app layout with main work area, side panels, and status area.

## Success Criteria
1. `pnpm install`, `pnpm test`, and `pnpm build` run.
2. Desktop dev command launches the shell.
3. Package boundaries match architecture docs.
4. No semantic graph implementation is hidden in UI-only packages.
