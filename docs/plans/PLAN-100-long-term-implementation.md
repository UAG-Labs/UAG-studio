# Plan: PLAN-100 - Long-Term Implementation

**Status:** Draft
**Handoff Target:** Haiku 4.5, Composer, GPT-5.2, or equivalent implementation agent
**Repo Scope:** `UAG-studio` only

## End State
`UAG-studio` is the production desktop authoring environment for Universal Architecture Graphs. It opens and saves TAKG, inspects UAGL read-only, edits semantic graph objects through a canvas adapter, preserves layout separately, calls the compiler, displays diagnostics/source maps/loss reports, supports policy-aware exports, shows runtime observations as overlays, manages project lifecycle, and provides a polished user experience for large architecture graphs.

## Non-Negotiable Boundaries
1. Do not define language semantics here.
2. Do not implement compiler internals or exporters here.
3. Do own user workflows, app state, Tauri integration, canvas adapters, file IO, diagnostics display, and export UX.
4. Keep canvas state out of TAKG semantics.

## Phases
| Phase | Plan | Exit State |
|---|---|---|
| 1 | [PLAN-101](./PLAN-101-workspace-app-shell.md) | App workspace and shell run. |
| 2 | [PLAN-102](./PLAN-102-project-state-bindings.md) | Project state and bindings are testable. |
| 3 | [PLAN-103](./PLAN-103-graph-canvas-adapter.md) | TAKG views render through adapter without semantic leakage. |
| 4 | [PLAN-104](./PLAN-104-file-io-project-lifecycle.md) | Open/save/recent/dirty/read-only lifecycle works. |
| 5 | [PLAN-105](./PLAN-105-visual-editing-inspectors.md) | Full graph editing and inspectors work. |
| 6 | [PLAN-106](./PLAN-106-compiler-diagnostics-exports.md) | Compiler, diagnostics, loss reports, and export UX work. |
| 7 | [PLAN-107](./PLAN-107-runtime-overlays-advanced-ux.md) | Runtime overlays and large-graph UX are complete. |
| 8 | [PLAN-108](./PLAN-108-release-hardening.md) | Desktop app is release-ready. |

## Final Success Criteria
1. Users can create, open, edit, validate, compile, export, and save architecture projects.
2. TAKG is editable and UAGL is read-only unless explicit import support with loss reporting exists.
3. Diagnostics and loss reports navigate to canvas objects, hidden objects, source paths, package issues, or artifacts.
4. Layout, selection, viewport, collapsed state, and UI state never become language semantics.
5. Large graphs are usable through views, search, filters, and panels.
6. App builds, tests, packages, and documents release behavior.

## Very Last Task
After all phases and final success criteria are complete, perform a full `docs/` folder audit as the final task in this repo. Update the documentation folder so it fully reflects the finished system, including specs, inherited procedures, plans, ADRs, skills, app workflows, UI architecture, compiler integration behavior, diagnostics/export behavior, compatibility records, and any repo-specific implementation knowledge. This documentation audit must be the final closeout action and should not be skipped or moved earlier.
