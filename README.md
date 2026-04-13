# Agentic — Governed AI Coding Pipeline for Google Antigravity

A drop-in template that gives any project structured, governed, autonomous AI-assisted development.

> **Architecture requires human approval. Implementation proceeds autonomously inside approved boundaries.**

## What This Is

A self-contained `.agentic/` directory and `GEMINI.md` configuration that you copy into any project workspace. It provides:

- **11 reusable commands** — `/architect`, `/build`, `/repair`, `/verify`, `/audit`, `/debug`, `/scaffold-feature`, `/stabilize`, `/onboard`, `/sync`, `/reset`
- **Deterministic quality gates** — G1–G5 mandatory on every task, G6–G10 conditional
- **Context anchoring** — prevents the agent from drifting on ports, paths, and conventions during long sessions
- **Milestone-based execution** — multi-step builds with automatic verification between milestones
- **Governed autonomy** — the agent works independently but stops at clearly defined risk boundaries

## Quick Start

```
# 1. Copy the pipeline into your project
cp -r .agentic/ /path/to/your-project/.agentic/
cp GEMINI.md /path/to/your-project/GEMINI.md
cp .gitattributes /path/to/your-project/.gitattributes

# 2. Open the project in Antigravity and run:
/onboard

# 3. The agent scans your project, populates blueprint.md and context.md.
#    Review the output, fill any gaps, then verify:
/verify
```

## How It Works

### Two Execution Modes

| Mode | Behavior | Commands |
|------|----------|----------|
| **Guided** | Conversational, interactive, requires human approval | `/architect` |
| **Autonomous** | Plans, implements, verifies, continues without approval | `/build`, `/repair`, `/stabilize` |

### Hard-Stop Triggers

In autonomous mode, the agent stops and asks when:

- Architecture rules would change
- New subsystem or major boundary introduced
- Dependencies or toolchain changes needed
- Security-sensitive work (secrets, auth, permissions)
- Database migrations or destructive operations
- Repeated gate failures

### Command Overview

| Command | Purpose | Mode |
|---------|---------|------|
| `/architect` | Design a system through conversation, produce architecture artifacts | Guided |
| `/build` | Execute the milestone ledger milestone-by-milestone | Autonomous |
| `/repair` | Fix localized bugs, cleanup, audit follow-up (≤5 files) | Autonomous |
| `/verify` | Run quality gates (full or scoped), produce report | — |
| `/audit` | Read-only code quality audit with machine-parseable output | — |
| `/debug` | Structured reproduce → isolate → diagnose → fix | Guided (or autonomous with `apply=true`) |
| `/scaffold-feature` | Scaffold a feature following project patterns | Autonomous |
| `/stabilize` | Bring project to 100% passing state | Autonomous |
| `/onboard` | Auto-discover project and populate pipeline config | — |
| `/sync` | Pull framework updates from this repo (tag-pinned) | — |
| `/reset` | Emergency brake — snap agent back to governance | — |

## Supported Languages

| Language | Compile | Lint | Test | Format |
|----------|---------|------|------|--------|
| TypeScript | `pnpm build` | `pnpm lint` | `pnpm test` | `pnpm format` |
| Rust | `cargo build` | `cargo clippy` | `cargo test` | `cargo fmt` |
| Python | — | `ruff check` | `pytest` | `ruff format` |

Conventions files are included for TypeScript and Rust. Additional languages can be added per-project via `/onboard`.

## Keeping Updated

```bash
# Check your current version
cat .agentic/version.txt

# Preview what would change
/sync dry_run=true

# Apply the update
/sync
```

The sync command overwrites framework files, preserves project-specific files (`blueprint.md`, `context.md`, `architecture/*`), and merges `GEMINI.md` using protected block markers to keep your project customizations intact.

## Platform Support

Ships configured for **Windows (PowerShell)**. For Linux/macOS, swap the OS Rules section in `GEMINI.md` — a commented-out Bash variant is included in the file.

## Structure

```
your-project/
├── GEMINI.md              # Agent instructions (synced framework + project overrides)
├── .gitattributes         # Line ending normalization
│
└── .agentic/
    ├── README.md           # Detailed pipeline documentation
    ├── blueprint.md        # Project identity (populated by /onboard)
    ├── context.md          # Critical facts re-read before every file write
    ├── version.txt         # Framework version (semver)
    ├── sync-source.txt     # Canonical repo URL for /sync
    ├── commands/           # 11 command definitions
    ├── conventions/        # Language-specific coding standards
    ├── governance/         # Quality gates, templates, escalation rules
    └── architecture/       # Design docs + milestone ledger (per-project)
```

## License

MIT
