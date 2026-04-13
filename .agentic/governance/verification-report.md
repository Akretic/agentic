# Verification Report Template

> Produced at the end of every completed task. Keep it short and consistent.

---

```markdown
# Verification Report

**Task:** [one-line description]
**Project:** [project name]
**Date:** [YYYY-MM-DD HH:MM]
**Scope:** [full / scoped (list affected paths)]
**Status:** ✅ ALL GATES PASSED / ❌ BLOCKED (see below)

## Gate Results

| Gate | Verdict | Notes |
|------|---------|-------|
| G1 Compile | ✅ / ❌ | |
| G2 Types | ✅ / ❌ | |
| G3 Lint | ✅ / ❌ | |
| G4 Tests | ✅ / ❌ | |
| G5 Docs | ✅ / ❌ | [artifact path or walkthrough reference] |
| G6 New Tests | ✅ / ⬚ N/A | [test file path or waiver justification] |
| G7 Visual | ✅ / ⬚ N/A | |
| G8 Security | ✅ / ⬚ N/A | [checklist: secrets ✓, auth guards ✓, CORS ✓] |
| G9 Migration | ✅ / ⬚ N/A | |
| G10 Perf | ✅ / ⬚ N/A | [performance note if triggered] |

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
5. **Include scope.** Always record whether full or scoped verification was run, and which paths were in scope.
6. **Deterministic gate evidence.** For G5, G6, G8, and G10, include the required evidence (artifact path, test file path, checklist, or performance note) in the Notes column. Empty notes for these gates is a FAIL.
