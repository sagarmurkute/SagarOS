# Sagar OS Core Foundation Libraries (`src/core/`)

This directory will contain the fundamental libraries (`libsagar-core`) shared across all Sagar OS services, the compositor, and applications.

## Planned Scope (Phase 2)
- Configuration file parsing (stateless fallback engine).
- IPC protocol helpers (D-Bus and Varlink wrapper abstractions).
- System introspection utilities (hardware detection, battery, thermal, and network state queries).
- Logging and telemetry-free diagnostics facade.

## Boundaries
- Must not depend on any graphical toolkit or display server.
- Must remain lightweight, highly modular, and memory-safe (written in C or Rust).
- No implementation code is present during Phase 0.
