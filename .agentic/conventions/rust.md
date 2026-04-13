# Rust Conventions

> Applies to all Rust projects managed by this pipeline.

---

## Imports

Order `use` statements in this sequence, separated by blank lines:

1. Standard library (`std::*`)
2. External crates (`serde`, `tokio`, `axum`, etc.)
3. Internal crate modules (`crate::*`, `super::*`)

```rust
use std::collections::HashMap;
use std::sync::Arc;

use serde::{Deserialize, Serialize};
use tokio::sync::RwLock;

use crate::domain::Project;
use crate::errors::AppError;
```

## Error Handling

- **Library crates:** use `thiserror` for typed, domain-specific errors.
- **Application/binary crates:** use `anyhow` for ergonomic error propagation.
- **No `.unwrap()` in non-test code.** Use `.expect("reason")` only when the invariant is truly guaranteed and documented.
- **No `panic!` in library code.** Return `Result` instead.

```rust
// ✅ Library error
#[derive(Debug, thiserror::Error)]
pub enum DomainError {
    #[error("Project not found: {0}")]
    NotFound(String),
    #[error("Validation failed: {0}")]
    Validation(String),
}

// ✅ Application error propagation
async fn handle_request() -> anyhow::Result<Response> {
    let project = repo.find(id).await?;
    Ok(project.into())
}

// ❌ Never in non-test code
let value = map.get("key").unwrap();
```

## Types

- **Prefer newtype wrappers** for domain identifiers: `struct ProjectId(Uuid)` over raw `Uuid`.
- **Derive common traits** on data types: `Debug, Clone, Serialize, Deserialize` at minimum.
- **Avoid `Box<dyn Any>`** — prefer concrete types or bounded trait objects.
- **Use `impl Trait`** in function signatures for simple polymorphism.
- **Lifetime annotations** only when the compiler requires them — don't over-annotate.

```rust
#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct ProjectId(pub Uuid);

#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct Project {
    pub id: ProjectId,
    pub name: String,
    pub created_at: DateTime<Utc>,
}
```

## Naming

| Thing | Convention | Example |
|-------|-----------|---------|
| Modules | `snake_case` | `project_service.rs` |
| Types / Structs / Enums | `PascalCase` | `ProjectStatus` |
| Functions / Methods | `snake_case` | `find_by_id` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_RETRIES` |
| Enum variants | `PascalCase` | `Status::Active` |
| Trait names | `PascalCase` | `Repository` |
| Feature flags | `kebab-case` | `feature = "async-runtime"` |

## Module Structure

- One primary type per file when the type is substantial.
- `mod.rs` or inline `pub mod` declarations — be consistent within a project.
- Group related functionality:

```
src/
├── main.rs / lib.rs
├── domain/           # Core types and business logic
│   ├── mod.rs
│   └── project.rs
├── handlers/         # HTTP/API handlers
├── services/         # Business logic orchestration
├── repository/       # Data access
└── errors.rs         # Error types
```

## Workspace Patterns

- Shared types go in a `-common` or `-shared` crate.
- Binary vs library separation: `my-app` (binary) depends on `my-app-core` (library).
- Workspace-level dependencies in `[workspace.dependencies]` to keep versions aligned.

## Clippy & Formatting

- Enforce all default Clippy lints: `#![deny(clippy::all)]` in `lib.rs` / `main.rs`.
- Use `rustfmt` with default settings unless the project has a `rustfmt.toml`.
- Run `cargo clippy --workspace --all-targets` for workspace-wide lint checks.
- Run `cargo fmt --all -- --check` in CI.

## Testing

- Unit tests in `#[cfg(test)] mod tests` at the bottom of each file.
- Integration tests in the `tests/` directory.
- Use `#[tokio::test]` for async tests.
- Mock external dependencies with trait-based injection, not concrete type patching.
- Test file naming mirrors source: `src/domain/project.rs` → tests in the same file or `tests/domain_project.rs`.

## Documentation

- Public API items must have `///` doc comments.
- Use `//!` module-level docs for crate and module overviews.
- Include examples in doc comments for non-obvious APIs: ` ```rust ... ``` `
