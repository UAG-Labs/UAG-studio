## Summary
<!-- What does this PR change and why? -->

## Changes
- 

## Related Issues
<!-- Closes # -->

## Checklist
- [ ] Generated output remains read-only in Studio — no editable code views introduced
- [ ] All graph mutations go through `editor-core` — no direct TAKG writes from panels
- [ ] Studio calls UAG-compiler for all compilation logic — no compiler code duplicated here
- [ ] Loss reports are surfaced, not hidden
- [ ] Incremental recompilation trigger preserved for graph changes
- [ ] Blockers recorded in `docs/open-questions.md` if applicable
