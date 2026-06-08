# Plan: PLAN-105 - Visual Editing and Inspectors

**Status:** Draft
**Repo Scope:** `UAG-studio`

## Goal
Complete graph editing workflows and property inspectors.

## Tasks
1. Add node creation, relationship creation, deletion, duplication, and ref cleanup.
2. Add inspectors for entity, relationship, boundary, surface, operation, contract, flow, view, policy, and layout metadata.
3. Support relationship fields for mode, protocol, cardinality, data, auth, and failure behavior.
4. Support classification and secret-reference warnings.
5. Add keyboard, command palette, and basic accessibility behavior.

## Success Criteria
1. Users can author a complete canonical-style graph without editing YAML.
2. Invalid relationships are diagnosed without crashing.
3. Inspectors write TAKG semantics, not canvas internals.
4. Basic keyboard and accessibility checks pass.
