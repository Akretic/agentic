# Epic Ledger Template

> Master build plan produced by the `/architect` command.
> Executed by the `/orchestrate` command.
> Each milestone is a self-contained vertical slice with its own context block.

---

## Project: <!-- project name -->
## Created: <!-- date -->
## Status: <!-- X of Y milestones verified -->

---

<!-- Copy this block for each milestone -->

## M1: <!-- Milestone Name -->                [ ] PLANNED

<!-- Add [CHECKPOINT] after the state marker for milestones requiring human review -->
<!-- Example: [ ] PLANNED [CHECKPOINT] -->

**Context:**
<!-- Inline the critical facts this milestone needs. Ports, paths, conventions. -->
<!-- This is intentionally redundant with context.md — redundancy prevents drift. -->

**Depends on:** <!-- M0 (none) / M1 / M2, etc. -->

**Scope:**
<!-- 2-3 sentence description of what this milestone delivers -->

### Tasks
- [ ] <!-- specific, implementable task -->
- [ ] <!-- specific, implementable task -->
- [ ] <!-- specific, implementable task -->

### Files Created/Modified
<!-- Filled in by the orchestrator after verification -->
<!-- - path/to/file.ts (created) -->
<!-- - path/to/other.ts (modified) -->

### Verification Notes
<!-- Filled in by the orchestrator after gate execution -->
<!-- Gate results, any warnings, fixes applied -->

---

## Milestone State Reference

| State | Marker | Meaning |
|-------|--------|---------|
| Planned | `[ ] PLANNED` | Not yet started |
| In Progress | `[>] IN_PROGRESS` | Agent is currently executing |
| Awaiting Review | `[?] AWAITING_REVIEW` | Checkpoint — waiting for human |
| Verified | `[x] VERIFIED` | All quality gates passed |
| Blocked | `[!] BLOCKED` | Escalation triggered, needs human decision |
