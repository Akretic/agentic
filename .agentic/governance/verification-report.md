# Verification Report Template

> Produced at the end of every completed task. Keep it short and consistent.

---

```markdown
# Verification Report

**Task:** [one-line description]
**Project:** [project name]
**Date:** [YYYY-MM-DD HH:MM]
**Status:** ✅ ALL GATES PASSED / ❌ BLOCKED (see below)

## Gate Results

| Gate | Verdict | Notes |
|------|---------|-------|
| G1 Build | ✅ / ❌ | |
| G2 Types | ✅ / ❌ | |
| G3 Lint | ✅ / ❌ | |
| G4 Tests | ✅ / ❌ | |
| G5 Docs | ✅ / ❌ | |
| G6 New Tests | ✅ / ⬚ N/A | |
| G7 Visual | ✅ / ⬚ N/A | |
| G8 Security | ✅ / ⬚ N/A | |
| G9 Migration | ✅ / ⬚ N/A | |
| G10 Perf | ✅ / ⬚ N/A | |

## Changes

- Files modified: X
- Files created: Y
- Files deleted: Z

## Failures (if any)

| Gate | Error | Fix Applied |
|------|-------|-------------|
| — | — | — |
```

---

## Rules

1. **Always produce this report.** No exceptions.
2. **Same structure every time.** Do not add extra sections or commentary.
3. **Mark N/A gates explicitly.** Never silently skip a gate.
4. **If a gate failed and was fixed**, record both the error and the fix in the Failures table.
