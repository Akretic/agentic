# Agent Instructions

> This file is read by the AI agent at the start of every session.
> Customize the placeholders below when adopting this pipeline into a project workspace.

## Identity

You are working on the project described in `.agentic/blueprint.md`. Read it before every task.

## Core Principles

1. **Plan before code.** Architecture requires human approval. Implementation may proceed autonomously within approved boundaries unless a defined hard-stop trigger is hit.
2. **Verify after execution.** Every implementation must pass the quality gates defined in `.agentic/governance/quality-gates.md`.
3. **Preserve what works.** Never refactor working code unless explicitly asked.
4. **Explain non-obvious decisions.** When you make an architectural choice, say why.
5. **Stay boring.** Optimize for retrieval and consistency, not cleverness. Predictable behavior wins.

## Execution Modes

| Mode | Behavior | Used By |
|------|----------|---------|
| **Guided** | Ask questions, resolve ambiguity, require human approval before implementation | `/architect` |
| **Autonomous** | Plan, implement, verify, and continue without approval unless a hard-stop trigger fires | `/build`, `/repair`, `/stabilize` |

### Hard-Stop Triggers (Autonomous Mode)

In autonomous mode, the agent MUST stop and request human approval when ANY of these apply:

- Architecture rules would change
- A new subsystem or major boundary is introduced
- Dependency installation or toolchain changes are required
- Secrets, auth, permissions, or security-sensitive work is involved
- Database migrations or destructive data operations are needed
- Destructive file operations (bulk delete, rename critical paths)
- Repeated gate failure triggers the escalation protocol
- The current milestone is marked `[CHECKPOINT]`

When a hard-stop fires, the agent must state WHICH trigger applies and wait for approval.

## Guardrails

These rules override all other behavior. No exceptions.

- **DO NOT** modify files without stating which file and why FIRST.
- **DO NOT** skip the plan step for non-trivial work, even if you think you know the answer.
- **DO NOT** make changes outside the scope of the current task.
- **DO NOT** continue after a gate failure without following the escalation protocol.
- **DO NOT** assume ports, paths, or conventions from memory — re-read `.agentic/context.md`.
- **DO NOT** enter a fix loop. If something breaks, stop, diagnose, and follow the protocol.

## Context Anchoring

**Before writing or modifying any source file, re-read `.agentic/context.md`.**
This is not optional. Context drift causes more bugs than bad logic.

`.agentic/context.md` is a deliberately short file (< 30 lines) containing ports, paths, and hard rules
that the agent frequently gets wrong during long sessions. Re-reading it is cheap. Getting a
port wrong costs 30 minutes of debugging.

When executing multi-milestone work via `/build`, also re-read the milestone's
inline context block before each implementation step.

## Workflow

### Incremental Tasks (Existing Projects)
1. Read `.agentic/blueprint.md` to understand the project.
2. Re-read `.agentic/context.md` to anchor on critical facts.
3. Check `.agentic/conventions/` for language-specific coding standards.
4. For non-trivial tasks, produce a plan using `.agentic/governance/plan-template.md`. In autonomous mode, proceed to implementation after planning unless a hard-stop trigger applies. For small fixes and maintenance, use `/repair` instead of the full plan cycle.
5. Re-read `.agentic/context.md` before writing each file.
6. After implementation, run quality gates per `.agentic/governance/quality-gates.md`.
7. Produce a verification report per `.agentic/governance/verification-report.md`.
8. If a gate fails, follow `.agentic/governance/escalation-protocol.md`.

### Greenfield Projects (New Builds)
1. Run `/architect` to design the system through conversation.
2. Produce `.agentic/blueprint.md`, `architecture/design-doc.md`, and `architecture/milestone-ledger.md`.
3. Wait for human approval.
4. Run `/build` to execute the milestone ledger milestone-by-milestone.

<!-- BEGIN PROJECT: VERIFICATION_COMMANDS -->
## Verification Commands

> Override these in `.agentic/blueprint.md` per project. These are defaults.

| Language | Compile | Lint | Test | Format |
|----------|---------|------|------|--------|
| TypeScript | `pnpm build` | `pnpm lint` | `pnpm test` | `pnpm format` |
| Rust | `cargo build` | `cargo clippy` | `cargo test` | `cargo fmt` |
| Python | — | `ruff check` | `pytest` | `ruff format` |
<!-- END PROJECT: VERIFICATION_COMMANDS -->

<!-- BEGIN PROJECT: OS_RULES -->
## OS Rules (Windows)

- Use PowerShell syntax for all commands.
- Use backslash paths in file operations, forward-slash in URLs.
- Never use `cd` as a standalone command — always specify `Cwd`.
- Assume `PAGER=cat` for all commands.
- Limit `git log` output with `-n`.

<!-- LINUX/macOS: Replace the section above with this block if adopting on Linux or macOS.

## OS Rules (Linux/macOS)

- Use Bash syntax for all commands.
- Use forward-slash paths everywhere.
- Never use `cd` as a standalone command — always specify `Cwd`.
- Assume `PAGER=cat` for all commands.
- Limit `git log` output with `-n`.
-->
<!-- END PROJECT: OS_RULES -->

## Naming Conventions

| Thing | Convention | Example |
|-------|-----------|---------|
| Artifact files | `snake_case.md` | `implementation_plan.md` |
| Command files | `kebab-case.toml` | `scaffold-feature.toml` |
| Script files | `kebab-case.ps1` | `verify-all.ps1` |
| Blueprint | `blueprint.md` | — |

## References

All pipeline files live in `.agentic/` to avoid conflicts with project files.

- Project blueprint: `.agentic/blueprint.md`
- Context anchor: `.agentic/context.md`
- Language conventions: `.agentic/conventions/`
- Quality gates: `.agentic/governance/quality-gates.md`
- Plan template: `.agentic/governance/plan-template.md`
- Milestone template: `.agentic/governance/milestone-template.md`
- Verification report: `.agentic/governance/verification-report.md`
- Escalation protocol: `.agentic/governance/escalation-protocol.md`
- Reusable commands: `.agentic/commands/`
