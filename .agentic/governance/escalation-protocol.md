# Escalation Protocol

When a quality gate fails, follow this deterministic retry sequence.

---

## Retry Ladder

| Attempt | Action | Scope |
|---------|--------|-------|
| **1st failure** | Analyze error output, apply targeted fix, re-run the failed gate | Fix only the failing code |
| **2nd failure** | Broaden analysis — check for upstream causes, dependency issues, or incorrect assumptions | May touch adjacent files |
| **3rd failure** | **Stop and escalate to user** | No further code changes |

## Escalation Report

When escalating after 3 failed attempts, produce this exact structure:

```markdown
## Escalation: [Gate ID] Failed

**Gate:** [gate name]
**Attempts:** 3

### What Was Tried
1. [Attempt 1 — what was changed and why]
2. [Attempt 2 — what was changed and why]
3. [Attempt 3 — what was changed and why]

### Root Cause Assessment
[Best understanding of why the gate keeps failing]

### Options
1. [Option A — highest confidence] — [tradeoff]
2. [Option B] — [tradeoff]
3. [Abandon and revert] — [what gets lost]
```

## Rules

1. **Never silently swallow a failure.** Every failed gate attempt is reported.
2. **Never apply unrelated changes during a retry.** Fix only what the gate is checking.
3. **Never skip the escalation.** If 3 attempts fail, stop.
4. **Revert on escalation.** If the user chooses to abandon, revert all changes from the failed task.
