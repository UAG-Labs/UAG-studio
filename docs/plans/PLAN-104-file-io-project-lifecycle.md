# Plan: PLAN-104 - File IO and Project Lifecycle

**Status:** Draft
**Repo Scope:** `UAG-studio`

## Goal
Implement reliable project open/save lifecycle.

## Tasks
1. Open `.takg.yaml` editable.
2. Save deterministic TAKG.
3. Open `.uagl.yaml` read-only.
4. Preserve partial-invalid TAKG and diagnostics.
5. Track dirty state, recent projects, save-as, overwrite warnings, and read/write errors.
6. Validate package/import metadata when schemas are available.

## Success Criteria
1. Fixture open/save round trip preserves semantics.
2. UAGL cannot be edited directly.
3. Write failure keeps dirty state.
4. Unknown compatible fields are preserved or diagnosed.
