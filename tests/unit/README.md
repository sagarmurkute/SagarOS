# Unit Tests (`tests/unit/`)

This directory contains standalone, isolated unit tests for Sagar OS code components.

## Planned Scope
- Unit tests for foundation abstractions (`src/core/`).
- Unit tests for domain shared libraries (`src/libraries/`).
- Unit tests for parsing, state machines, and configuration engines.

## Guidelines
- Must execute quickly in memory without requiring hardware access or root privileges.
- Standardized assertion reporting.
- No implementation code is present during Phase 0.
