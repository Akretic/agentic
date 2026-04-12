# Quality Gates

Every implementation must pass through a defined set of quality gates before completion.
Gates are classified as **mandatory** (run on every task) or **conditional** (run when the task type warrants it).

---

## Gate Definitions

### Mandatory Gates (Every Task)

These gates run on every task, regardless of scope or risk.

| ID | Gate | Check | Command |
|----|------|-------|---------|
| G1 | **Build** | Code compiles without errors | `pnpm build` / `cargo build` |
| G2 | **Type Safety** | No type errors | `pnpm typecheck` / `cargo check` |
| G3 | **Lint** | No lint violations introduced | `pnpm lint` / `cargo clippy` |
| G4 | **Existing Tests** | All pre-existing tests still pass | `pnpm test` / `cargo test` |
| G5 | **Documentation** | Changes summarized in walkthrough artifact | Artifact creation |

### Conditional Gates

These gates run only when the task matches their trigger condition.

| ID | Gate | Trigger | Check | Command |
|----|------|---------|-------|---------|
| G6 | **New Tests** | Adding a feature or fixing a bug | New code has test coverage for the change | Manual verification |
| G7 | **Visual Verification** | UI changes (components, pages, styles) | UI renders correctly, no layout breakage | Browser subagent |
| G8 | **Security Scan** | Auth, API, secrets, or permission changes | No hardcoded secrets, safe auth patterns | `grep` scan for patterns |
| G9 | **Migration Safety** | Database schema changes | Migration runs cleanly, rollback is possible | `prisma migrate dev` + review |
| G10 | **Performance** | Changes to queries, loops, or data-heavy paths | No obvious N+1 queries or unbounded loops | Manual review |

---

## Gate Verdicts

Each gate produces one of three verdicts:

| Verdict | Meaning | Action |
|---------|---------|--------|
| ✅ PASS | Gate requirement satisfied | Continue to next gate |
| ⚠️ WARN | Minor issue, non-blocking | Note in verification report, continue |
| ❌ FAIL | Blocking issue | Fix and re-run gate (see escalation protocol) |

---

## Applying Gates to a Task

1. **Always run G1–G5.**
2. **Check if any conditional gates apply** based on the task description.
3. **Run applicable conditional gates.**
4. **Produce a verification report** listing all gates run and their verdicts.

If a gate is not applicable, mark it as `⬚ N/A` in the report — do not skip it silently.
