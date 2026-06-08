# Artifact Definition — `UAG-studio`

## Purpose
Defines what a successful first implementation artifact looks like.

## Success Conditions
- The repository can be understood without prior conversation context.
- Root README, docs architecture, roadmap, structure, and specs are present.
- No unresolved open questions exist in this initialization package.
- Implementation can begin from specs without architecture clarification.
- Acceptance criteria remain unchecked until tests or manual evidence exist.

## Done for Bootstrap
- README explains the repo.
- `specs/README.md` indexes all specs.
- `REPOSITORY_STRUCTURE.md` defines expected file/folder layout.
- `plans/PLAN-001-bootstrap.md` defines first execution plan.

## Implementation Readiness Decisions
The initial open-question audit has been answered for planning purposes. The accepted baseline decisions are recorded in [ADR-0002 Implementation Readiness Decisions](./adr/ADR-0002-implementation-readiness-decisions.md) and reflected in [open-questions.md](./open-questions.md).

Answered questions:
- Q-001: What is the first supported Studio project format?
- Q-002: How should Studio represent invalid or partial TAKG?
- Q-003: What maps React Flow nodes/handles/edges to TAKG semantics?
- Q-004: Where does layout live?
- Q-005: How does Studio call the compiler?
- Q-006: What is the frontend/backend command boundary?
- Q-007: What is the first useful node palette?
- Q-008: How should diagnostics appear on the canvas?
- Q-009: What does read-only/import UAGL mean?
- Q-010: What is the first app target: desktop only or web plus desktop?

