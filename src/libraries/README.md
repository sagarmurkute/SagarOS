# Sagar OS Shared Libraries (`src/libraries/`)

This directory houses reusable, non-core domain libraries and client SDKs developed for Sagar OS components and applications.

## Planned Scope
- Client libraries for interacting with Sagar OS system daemons (`sagar-configd`, `sagar-sessiond`).
- Wayland client helper abstractions and IPC wrappers.
- Theming and visual asset integration helpers.

## Distinction from `src/core/`
- `src/core/`: Foundation system abstractions, low-level POSIX utilities, and essential system-level primitives (`libsagar-core`).
- `src/libraries/`: Higher-level modular shared libraries, client SDKs, and reusable component toolkits.

## Guidelines
- Strict modularity and minimal external dependencies.
- No implementation code is present during Phase 0.
