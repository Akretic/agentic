# Plan Template

> Standard structure for implementation plans. Follow this format exactly.

---

```markdown
# [Goal — One Line]

Brief description of the problem and what the change accomplishes. 2-3 sentences max.

## User Review Required

> [!IMPORTANT]
> List anything that requires explicit user decision before proceeding.

## Proposed Changes

### [Component Name]

#### [MODIFY/NEW/DELETE] [filename](file:///absolute/path)
- What changes and why

## Verification Plan

Which quality gates apply (reference by ID from quality-gates.md):
- Mandatory: G1, G2, G3, G4, G5
- Conditional: [list applicable gates with justification]

## Open Questions

Anything that blocks or could alter the plan.
```

---

## Rules

1. **Do not pad the plan.** If the change is small, the plan is small.
2. **Group changes by component**, not by file type.
3. **Reference quality gates by ID.** Do not re-describe what the gates check.
4. **Only ask open questions that would change the plan.** Do not ask "should I proceed?"
