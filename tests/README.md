# Sagar OS Test Suite (`tests/`)

This directory houses the comprehensive test and automated validation suite for **Sagar OS**.

## Directory Structure

```text
tests/
├── unit/            # Isolated unit tests for libraries, services, and utilities
├── integration/     # Subsystem, IPC, and cross-daemon communication tests
├── security/        # Sandboxing (Landlock, seccomp), privilege isolation, and AppArmor tests
└── vm/              # Automated headless QEMU boot and end-to-end OS image validation
```

## Testing Principles
- **Hermetic Execution:** Tests must run without modifying the host machine.
- **Fail Fast:** Verification harnesses should report unambiguous error codes and logs.
- **Continuous Integration:** Integrated with GitHub Actions workflows.
