# Project Blueprint

> Fill this in when adopting the agentic pipeline into a project workspace.
> This file is the single source of truth for the project's identity and conventions.

---

## Stable Facts

> Verified, structural facts about this project. These change only during deliberate
> architectural changes. Always trust these.

### Identity

| Key | Value |
|-----|-------|
| Name | <!-- project name --> |
| Root | <!-- absolute path to project root --> |
| Repository | <!-- git remote URL --> |
| Stack | <!-- e.g., NestJS 10 + Next.js 16 + Prisma 5 + PostgreSQL 16 --> |
| Package Manager | <!-- e.g., pnpm 9 / uv / cargo --> |
| Language | <!-- e.g., TypeScript 5.x (strict) / Python 3.12 / Rust 1.78 --> |

### Ports & Services

| Service | Port | Notes |
|---------|------|-------|
| <!-- service name --> | <!-- port --> | <!-- notes --> |

### Architecture Rules

<!-- Non-negotiable structural constraints for this project. Examples: -->
<!-- - Backend modules follow controller → service → repository pattern -->
<!-- - No `any` types, no `console.log` -->
<!-- - API versioned under `/v1/` -->

### Data Layer

| Key | Value |
|-----|-------|
| ORM | <!-- e.g., Prisma 6 --> |
| Schema Path | <!-- e.g., prisma/schema.prisma --> |
| Route Handlers | <!-- e.g., src/app/api/**/route.ts --> |
| Shared Helpers | <!-- e.g., src/lib/** --> |

### Directory Layout

```
project/
├── ...describe key directories...
```

---

## Working Assumptions

> These may drift as the project evolves. **Verify against current code before relying on them.**
> Last verified: <!-- YYYY-MM-DD -->

### Dev Credentials

| Key | Value |
|-----|-------|
| <!-- credential name --> | <!-- value --> |

### Current State

<!-- Active branch? Any known broken features? Recent major changes? -->

### Dependencies of Note

<!-- Non-obvious or pinned dependencies, known version constraints. -->

### Known Gotchas

<!-- Recurring issues, workarounds, things that reliably trip up the agent. -->

#### Boundary Mismatches

<!-- ORM ↔ helper nullability mismatches, API ↔ DB schema drift, etc. -->
<!-- Example: sanitize() returns string | null; Prisma required text fields must never receive null -->
<!-- Tag pre-existing issues with [PRE-EXISTING] -->

#### Pre-Existing Failures

<!-- Gate failures present at adoption time. Do not attempt to fix unless explicitly asked. -->

---

## Verification Sequence

> Ordered list of commands to confirm this project is healthy.
> These are referenced by the `/verify` command and quality gates.

1. <!-- `command` — what it checks -->
2. <!-- `command` — what it checks -->
3. <!-- Browser check: navigate to `http://localhost:XXXX` and verify [specific thing] -->

---

## Contacts & Context

<!-- Owner, stakeholders, deployment targets, external services. -->
