# Testing Standards & Quality Verification — Sagar OS

> **Testing standards, framework-neutral requirements, and verification protocols across unit, integration, security, and virtual machine tiers for Sagar OS.**

---

## 1. Testing Pyramid & Verification Tiers

To ensure system reliability, Sagar OS enforces a multi-tiered testing strategy structured into four distinct test domains:

```text
tests/
├── unit/            # Fast, isolated in-memory unit tests
├── integration/     # Inter-Process Communication & multi-daemon contract tests
├── security/        # Sandboxing, Landlock boundary, and privilege isolation tests
└── vm/              # Automated headless QEMU boot and live ISO validation
```

---

## 2. Unit Testing Standards (`tests/unit/`)

### 2.1 Scope & Execution Requirements
- **Isolation:** Unit tests must execute entirely in user space without requiring hardware access, root privileges, or running background daemons.
- **Speed:** The entire unit test suite must complete execution in under 30 seconds in CI.
- **Determinism:** Tests must be deterministic; tests relying on wall-clock timing or external network connections are strictly prohibited.

### 2.2 Language-Specific Test Standards
- **Rust Components:** 
  - Executed via `cargo test --all`.
  - Unit tests live in the same file within a dedicated `#[cfg(test)] mod tests` block.
- **C Components:**
  - Must adhere to framework-neutral test requirements: clear test runner execution, exit code 0 for success, non-zero for failure, andTAP (Test Anything Protocol) or standard test output.
  - *Framework Selection:* `cmocka` is the recommended lightweight test harness candidate (available in Debian 13 without complex runtimes), pending formal benchmark approval.

---

## 3. Integration Testing Standards (`tests/integration/`)

### 3.1 Scope
Integration tests validate the interaction between two or more subsystems (e.g., verifying that a client request over D-Bus correctly triggers a state update in the configuration service).

### 3.2 Guidelines
- Use an isolated session or private test D-Bus instance (`dbus-run-session`) to prevent pollution of the host or developer session.
- Verify D-Bus interface XML schemas against active daemon introspection.
- Validate that service crashes or client disconnects trigger proper cleanup without memory leaks or zombie processes.

---

## 4. Security & Sandbox Testing Standards (`tests/security/`)

### 4.1 Scope
Security tests proactively verify that privilege boundaries, namespaces, and sandboxes cannot be breached.

### 4.2 Test Scenarios
1. **Filesystem Sandbox Boundary:** Assert that an application restricted by Landlock cannot read or write to unauthorized directories (e.g., attempting to read `~/.ssh` or `/etc/shadow` must return `EACCES`).
2. **Syscall Filtering:** Assert that forbidden system calls filtered by `seccomp-bpf` terminate the offending thread or return `EPERM`.
3. **Privilege Elevation:** Assert that unprivileged user sessions cannot trigger administrative actions without valid polkit authorization.

---

## 5. Virtual Machine & Boot Testing Standards (`tests/vm/`)

### 5.1 Scope
Automated end-to-end boot tests executed in headless QEMU/KVM virtualized environments to validate the generated rootfs and live installation media.

### 5.2 Verification Gates
1. **Boot-to-Prompt Target:** The minimal rootfs image must boot to a clean login prompt within 5 seconds under virtualized hardware.
2. **Zero Failed System Units:** Upon reaching `multi-user.target`, `systemctl --failed` must return zero failed systemd services.
3. **Automated Exit Code:** The QEMU test harness must execute automatically via `tools/dev/run-qemu.sh`, capture serial console output, and exit with status `0` on clean prompt detection or non-zero on timeout.
