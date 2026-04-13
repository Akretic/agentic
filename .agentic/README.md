# Agentic Coding Pipeline v1.1

A self-contained template for governed, autonomous AI-assisted development with Google Antigravity.
Copy this structure into any project workspace to get instant project intelligence,
reusable commands, deterministic quality gates, and full-project orchestration.

## Philosophy

> **Architecture requires human approval. Implementation proceeds autonomously inside approved boundaries.**

The system is designed around a simple operating model: humans own the design decisions,
the agent owns the execution. The `/architect` command is conversational and collaborative.
Once architecture is approved, `/build` executes milestone-by-milestone without asking
permission for every screwdriver turn. The agent stops only when it hits a genuine risk
boundary — never for routine implementation steps.

**Stay boring.** This system is optimized for retrieval and consistency, not cleverness.
Concise blueprints, strict naming, predictable command behavior, identical verification
reports every time.

## Structure

```
your-project/
├── GEMINI.md                    # Agent instructions (ONLY pipeline file at root)
├── README.md                    # YOUR project's readme (untouched)
├── package.json                 # YOUR project files (untouched)
├── src/                         # YOUR code (untouched)
│
└── .agentic/                    # Pipeline internals — all contained here
    ├── README.md                # Pipeline documentation
    ├── blueprint.md             # Project identity: stable facts + working assumptions
    ├── context.md               # Context anchor: critical facts re-read before every file write
    │
    ├── commands/                # Reusable commands with defined inputs/outputs
    │   ├── architect.toml       # Design a greenfield project through conversation (guided)
    │   ├── build.toml           # Execute the approved milestone plan (autonomous)
    │   ├── verify.toml          # Run quality gates (full or scoped), produce report
    │   ├── repair.toml          # Fix localized bugs, cleanup, audit follow-up (autonomous)
    │   ├── stabilize.toml       # Bring project to 100% passing state (autonomous)
    │   ├── scaffold-feature.toml # Scaffold a feature following project patterns
    │   ├── audit.toml           # Read-only code quality audit (machine-parseable output)
    │   ├── debug.toml           # Structured reproduce → isolate → diagnose → fix
    │   ├── onboard.toml         # Auto-discover project and populate blueprint + context
    │   ├── sync.toml            # ⚠️ EXPERIMENTAL — Pull framework files from canonical source
    │   └── reset.toml           # Emergency brake — snap agent back to governance
    │
    ├── conventions/             # Language-specific coding standards
    │   ├── typescript.md        # TypeScript/JavaScript conventions
    │   └── rust.md              # Rust conventions
    │
    ├── governance/              # Quality gates, plan templates, escalation rules
    │   ├── quality-gates.md     # G1–G5 mandatory, G6–G10 conditional
    │   ├── plan-template.md     # Standard implementation plan format
    │   ├── milestone-template.md # Master build plan for multi-milestone projects
    │   ├── verification-report.md # Rigid report template (same every time)
    │   └── escalation-protocol.md # 3-attempt retry ladder → escalate
    │
    └── architecture/            # (Created by /architect for greenfield projects)
        ├── design-doc.md        # System architecture, data models, API surface
        └── milestone-ledger.md  # Milestone-by-milestone execution plan
```

## Execution Modes

The pipeline operates in two modes:

| Mode | Behavior | Used By |
|------|----------|---------|
| **Guided** | Conversational, human-interactive, approval required before implementation | `/architect` |
| **Autonomous** | Plan, implement, verify, continue — stops only on hard-stop triggers | `/build`, `/repair`, `/stabilize` |

### Hard-Stop Triggers (Autonomous Mode)

In autonomous mode, the agent must stop and request approval when:

- Architecture rules would change
- A new subsystem or major boundary is introduced
- Dependency installation or toolchain changes
- Secrets, auth, permissions, or security-sensitive work
- Database migrations or destructive data operations
- Destructive file operations
- Repeated gate failure triggers the escalation protocol
- Explicit `[CHECKPOINT]` milestones

## Workflow Recipes

### Bootstrap a New Workspace

```
/onboard → /verify (full) → /stabilize if needed
```

### Small Bug / Cleanup / Maintenance

```
/repair → /verify (scoped)
```

### Diagnosis-First Workflow

```
/debug → optional apply=true → /verify (scoped)
```

### Scoped Feature Inside Existing Architecture

```
/scaffold-feature → /build
```

### Major Subsystem / New Architecture

```
/architect → human approval → /build
```

### Periodic Health Check / Release Prep

```
/audit → /repair (for repairable findings)
```

## Context Anchoring

The biggest failure mode in agentic coding is **context drift** — the agent forgets ports,
paths, and conventions mid-session as the context window fills with code diffs and terminal
output.

`.agentic/context.md` is the defense: a deliberately short (< 30 lines) cheat sheet of critical facts.
The agent is instructed to re-read it before writing every file. This is cheap (25 lines vs
50,000 tokens of context) and eliminates the most common class of drift-caused bugs.

## Adoption

1. Copy this entire directory structure into your project workspace.
2. Open Antigravity in that workspace.
3. Run `/onboard` — the agent will automatically:
   - Scan your project for stack, ports, paths, and conventions
   - Fill in `.agentic/blueprint.md` with discovered stable facts
   - Fill in `.agentic/context.md` with critical constants
   - Report what it found and what needs manual input
4. Review the populated files and fill in any gaps the agent flagged.
5. Run `/verify` to confirm everything builds and passes gates.
6. If not on Windows, update the OS rules section in `GEMINI.md` for your platform.
