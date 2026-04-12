# Agentic Coding Pipeline

A self-contained template for governed AI-assisted development with Google Antigravity.
Copy this structure into any project workspace to get instant project intelligence,
reusable commands, deterministic quality gates, and full-project orchestration.

## Philosophy

Borrowed from the Akretic governance platform:

> **Models may propose, never execute unchecked.**

Every plan requires human approval. Every implementation runs through deterministic gates.
Every result produces a verification report. If something fails, the agent escalates — it
never silently swallows an error.

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
    │   ├── architect.toml       # Design a greenfield project through conversation
    │   ├── orchestrate.toml     # Execute an epic ledger milestone-by-milestone
    │   ├── verify.toml          # Run quality gates, produce verification report
    │   ├── scaffold-feature.toml # Scaffold a feature following project patterns
    │   ├── audit.toml           # Read-only code quality audit
    │   ├── debug.toml           # Structured reproduce → isolate → diagnose → fix
    │   ├── reset.toml           # Emergency brake — snap agent back to governance
    │   └── onboard.toml         # Auto-discover project and populate blueprint + context
    │
    ├── conventions/             # Language-specific coding standards
    │   └── typescript.md        # (add python.md, rust.md as needed)
    │
    ├── governance/              # Quality gates, plan templates, escalation rules
    │   ├── quality-gates.md     # G1–G5 mandatory, G6–G10 conditional
    │   ├── plan-template.md     # Standard implementation plan format
    │   ├── epic-template.md     # Master build plan for multi-milestone projects
    │   ├── verification-report.md # Rigid report template (same every time)
    │   └── escalation-protocol.md # 3-attempt retry ladder → escalate
    │
    └── architecture/            # (Created by /architect for greenfield projects)
        ├── design-doc.md        # System architecture, data models, API surface
        └── epic-ledger.md       # Milestone-by-milestone execution plan
```

## Two Workflows

### Incremental (Existing Projects)
For tasks on established codebases — bug fixes, features, refactors.

1. Agent reads `GEMINI.md` → `.agentic/blueprint.md` → `.agentic/context.md`
2. Produces a plan → you approve → agent implements
3. Quality gates run → verification report produced
4. If gates fail → escalation protocol (3 retries max)

### Greenfield (New Projects)
For building complete applications from a single high-level prompt.

1. Run `/architect` — conversational design phase with clarifying questions
2. Agent produces `.agentic/blueprint.md`, `design-doc.md`, `epic-ledger.md`
3. You review and approve the architecture
4. Run `/orchestrate` — agent executes milestone-by-milestone
5. Pauses at `[CHECKPOINT]` milestones for human review
6. Each milestone runs through quality gates independently

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
