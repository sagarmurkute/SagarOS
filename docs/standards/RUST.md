# Rust Development Standards — Sagar OS

> **Coding conventions, language edition, safety policies, formatting, and linting standards for Rust in Sagar OS.**

---

## 1. Scope & Language Edition

Rust is an approved systems programming language for Sagar OS, utilized for memory-safe system components, selected background services (`src/services/`), Wayland display server logic (`src/graphics/`), and long-term kernel research (`research/kernel/`).

- **Approved Language Edition:** **Rust 2021 Edition** (configured via `edition = "2021"` in `Cargo.toml`).
- **Toolchain Baseline:** Stable Rust toolchain packaged in or compatible with **Debian GNU/Linux 13 ("Trixie")**.
- **Core Motivation:** Harnessing compile-time memory safety, thread safety, and type systems to eliminate memory-corruption vulnerabilities.

---

## 2. Tooling & Formatting

### 2.1 Automated Formatting (`rustfmt`)
All Rust source files must format cleanly using standard `rustfmt` (`cargo fmt --check`). Key style parameters:
- **Indent Width:** 4 spaces.
- **Max Width:** 100 characters soft limit.
- **Imports:** Grouped and ordered by `std`, external crates, and internal crate modules.

### 2.2 Static Analysis & Linting (`clippy`)
All Rust code must pass Clippy checks in CI with zero warnings:
```bash
cargo clippy --all-targets --all-features -- -D warnings
```

---

## 3. Safety & `unsafe` Code Policy

Memory safety is the primary rationale for adopting Rust in Sagar OS. Unsafe blocks undermine this invariant and must be severely restricted.

1. **Default Deny:** Every library crate must declare `#![deny(unsafe_code)]` at its crate root unless low-level hardware or FFI interaction strictly requires an exception.
2. **Encapsulation of `unsafe`:** Where `unsafe` is unavoidable (e.g., C library FFI, direct DRM/KMS buffer mmap, or POSIX raw syscalls):
   - The unsafe code must be contained inside the smallest possible private function or module.
   - It must expose a strictly safe public interface that guarantees invariants cannot be violated by safe callers.
3. **Mandatory Safety Documentation:** Every `unsafe` block or function must be preceded by a `// SAFETY:` comment explaining why the operation is sound and how invariants are preserved:
   ```rust
   // SAFETY: `fd` is guaranteed to be open and valid for the lifetime of `Device`.
   // The kernel guarantees that `ioctl` with DRM_IOCTL_VERSION does not write out of bounds.
   unsafe {
       ffi::ioctl(self.fd, ffi::DRM_IOCTL_VERSION, &mut version)
   }
   ```

---

## 4. Error Handling & Panic Prevention

1. **No Panics in Production Code:** Functions in shared libraries (`src/libraries/`) and system services (`src/services/`) must never panic.
   - Banned in production paths: `.unwrap()`, `.expect()`, `panic!()`, `unreachable!()` (unless mathematically impossible to reach and documented).
   - Use pattern matching (`if let`, `match`) or the `?` operator to propagate errors gracefully.
2. **Structured Error Types:** Libraries must define explicit, structured domain error enums implementing `std::error::Error`:
   ```rust
   #[derive(Debug, thiserror::Error)]
   pub enum ConfigError {
       #[error("configuration file not found: {path}")]
       NotFound { path: String },
       #[error("failed to parse schema: {reason}")]
       ParseError { reason: String },
       #[error("I/O error encountered: {0}")]
       Io(#[from] std::io::Error),
   }
   ```
3. **Graceful Degradation:** Services must handle external failures (e.g., client disconnection, corrupted config file) without terminating the main process.

---

## 5. Naming & Organization

Adhere strictly to official Rust API guidelines:

| Element | Convention | Example |
| :--- | :--- | :--- |
| **Crates & Packages** | Lowercase kebab-case | `sagar-core`, `sagar-config` |
| **Modules & Files** | Lowercase snake_case | `display_server`, `session_manager.rs` |
| **Types, Structs & Enums** | PascalCase | `SessionCoordinator`, `PowerState` |
| **Functions & Methods** | Lowercase snake_case | `load_configuration()`, `is_active()` |
| **Constants & Statics** | SCREAMING_SNAKE_CASE | `MAX_WORKSPACE_COUNT` |
| **Traits** | PascalCase (adjective or capability) | `Configurable`, `SessionHandler` |

---

## 6. Documentation Comments

- All public structs, enums, functions, and traits must include doc comments (`///` or `//!` for module level).
- Include `# Errors` sections for any function returning a `Result`.
- Include doc tests where feasible to ensure documentation remains synchronized with code.
