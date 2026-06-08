# Plan: PLAN-001 - Bootstrap `UAG-studio`

**Status:** Draft
**Derived From:** ../specs/README.md
**Derivation Status:** Current

## Objective
Create the initial implementation skeleton exactly as defined in `../REPOSITORY_STRUCTURE.md`.

## Required Reading
- ../../README.md
- ../../AGENT.md
- ../artifact.md
- ../architecture.md
- ../REPOSITORY_STRUCTURE.md
- ../specs/README.md

## Architecture Graph Hardening
Before Studio becomes the primary authoring surface, it must protect the graph contract:

1. Use an adapter between TAKG and React Flow so canvas state never becomes language semantics.
2. Preserve partial-invalid TAKG and display compiler diagnostics instead of blocking save.
3. Keep view filters separate from layout coordinates and editor-only state.
4. Open UAGL read-only until reverse import and import loss reports are trustworthy.
5. Display diagnostics and loss reports with source-map navigation to canvas objects, source paths, package issues, or export artifacts.
6. Apply classification/redaction warnings before AI context or public exports.
7. Treat runtime observations as overlays/drift diagnostics, not editable design intent.

## Steps
1. Create the root files and folders defined in `../REPOSITORY_STRUCTURE.md`.
2. Implement only the first milestone in `ROADMAP.md`.
3. Add tests corresponding to acceptance criteria.
4. Do not mark criteria verified until evidence exists.
5. Stop if an unresolved design question appears.
