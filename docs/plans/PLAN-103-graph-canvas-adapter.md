# Plan: PLAN-103 - Graph Canvas Adapter

**Status:** Draft
**Repo Scope:** `UAG-studio`

## Goal
Render and interact with TAKG views without leaking canvas details into language semantics.

## Tasks
1. Implement TAKG view to React Flow adapter.
2. Map entities to nodes and relationships to edges.
3. Map handles/ports as UI affordances, not language facts unless backed by semantic fields.
4. Implement view filters and layout application.
5. Add adapter tests proving node movement changes layout only.

## Success Criteria
1. Canonical fixture view renders.
2. Layout changes do not alter semantic entities or relationships.
3. Hidden diagnostics can still be surfaced in panels.
4. Adapter is isolated enough to replace canvas library later.
