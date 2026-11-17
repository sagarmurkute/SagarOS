# Security & Sandbox Validation Tests (`tests/security/`)

This directory contains test suites designed to verify system security controls, isolation boundaries, and privilege separation.

## Planned Scope
- AppArmor profile validation and enforcement checks.
- Landlock LSM filesystem boundary tests for sandboxed applications.
- `seccomp-bpf` syscall filter violation tests.
- Privilege escalation regression tests (verifying unprivileged daemons cannot write to system state).
