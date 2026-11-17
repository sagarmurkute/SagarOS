# ROADMAP.md — Sagar OS Long-Term Engineering Roadmap

> **Strategic Phasing, Milestones, and Verification Criteria.**

---

## Roadmap Overview

The development of Sagar OS is divided into structured, sequential phases. Advancement from one phase to the next requires satisfying explicit exit criteria.

```mermaid
flowchart LR
    P0["Phase 0: Inception & Specs (Current)"] --> P1["Phase 1: Debian 13 Base & Image Harness"]
    P1 --> P2["Phase 2: Core Middleware & System Services"]
    P2 --> P3["Phase 3: Wayland Compositor & Shell"]
    P3 --> P4["Phase 4: Applications & Security Sandboxing"]
    P4 --> P5["Phase 5: Kernel Research & Prototyping"]
```

---

## Phase 0: Inception, Architecture & Governance (CURRENT PHASE)

- **Objective:** Establish the foundational repository, architectural invariants, governance, and contributor guidelines without premature implementation.
- **Deliverables:**
  - [x] Repository directory layout (`distro/`, `docs/`, `src/`, `research/`, `tools/`).
  - [x] Foundational documentation (`README.md`, `AGENTS.md`, `MASTER_SPEC.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `DECISIONS.md`).
  - [x] Architecture Decision Records baseline (ADR-0001 through ADR-0005).
  - [x] Documentation and contribution standards (`CONTRIBUTING.md`, `docs/standards/DOCUMENTATION.md`).
  - [x] Clear demarcation between Debian upstream and Sagar custom components.
- **Exit Criteria:**
  - Repository structure fully established and verified.
  - Zero premature driver, kernel, or desktop code introduced.
  - Contributor and AI agent protocols documented and committed.

---

## Phase 1: Debian 13 Base Rootfs & Bootable Image Harness

- **Objective:** Construct a containerized, hermetic build pipeline capable of producing a minimal bootable Debian GNU/Linux 13 ("Trixie") root filesystem and UEFI ISO image.
- **Key Tasks:**
  - Define Debian 13 package manifests (`distro/manifests/base.list`, `distro/manifests/hardware.list`).
  - Implement a reproducible debootstrap/mmdebstrap build script in `tools/build/build-rootfs.sh`.
  - Implement a UEFI-bootable live ISO/QCOW2 disk generator in `tools/build/build-image.sh`.
  - Establish automated headless boot testing via QEMU (`tools/dev/run-qemu.sh`).
- **Deliverables:**
  - Fully reproducible bootable base image running Debian 13 LTS kernel.
  - Automated CI test passing QEMU boot verification into console shell.
- **Exit Criteria:**
  - System boots to a clean login prompt in QEMU (UEFI) within 5 seconds.
  - Base footprint adheres strictly to the minimal package manifest.

---

## Phase 2: Core Middleware & System Services Integration

- **Objective:** Establish Sagar OS branding, configuration infrastructure, session supervisor, and system daemons.
- **Key Tasks:**
  - Setup Sagar OS package repository structure and release signing keys.
  - Author Sagar OS core library (`src/core/`) for system introspection and configuration management.
  - Implement system daemons (`src/services/`):
    - Session coordinator and display manager integration.
    - Power management, device policy, and audio (`PipeWire`) integration.
  - Create base filesystem overlay (`distro/overlays/base/`) with default `/usr/lib/sagar` configurations.
- **Deliverables:**
  - `libsagar-core` shared library.
  - `sagar-session-daemon` and `sagar-configd` services running under systemd.
- **Exit Criteria:**
  - System boots into Sagar session coordinator with D-Bus services active and zero systemd unit failures.

---

## Phase 3: Sagar Wayland Compositor & Shell Environment

- **Objective:** Develop a modern, hardware-accelerated Wayland compositor and desktop user interface.
- **Key Tasks:**
  - Implement Wayland compositor in `src/shell/` utilizing `wlroots` or modern Rust Wayland bindings.
  - Implement the desktop shell: status panel, app launcher, notification server, and lock screen.
  - Integrate DRM/KMS graphics pipeline with Mesa acceleration (Vulkan/OpenGL).
  - Integrate `libinput` gesture and input processing.
- **Deliverables:**
  - Functional Wayland compositor binary (`sagar-shell`).
  - Integrated status bar, launcher, and workspace manager.
- **Exit Criteria:**
  - Compositor renders at consistent 60+ FPS on Intel, AMD, and VirtIO-GPU targets.
  - Wayland compliance tests (xdg-shell, layer-shell protocols) pass cleanly.

---

## Phase 4: Application Ecosystem, Sandboxing & Polish

- **Objective:** Build native Sagar OS first-party applications and integrate robust sandboxing for third-party software.
- **Key Tasks:**
  - Implement first-party applications in `src/apps/` (Settings, Terminal, File Manager).
  - Enforce application sandboxing using Landlock, seccomp-bpf, and unprivileged user namespaces.
  - Provide seamless Flatpak / OCI integration for third-party desktop applications.
  - End-to-end security audit and performance profiling.
- **Deliverables:**
  - First-party application suite with cohesive visual design and keybinding language.
  - Hardened default security profiles.
- **Exit Criteria:**
  - Daily-driver viability: full hardware support (Wi-Fi, Bluetooth, Audio, Multi-monitor, Suspend/Resume).

---

## Phase 5: Long-Term Independent Kernel Research & Prototyping

- **Objective:** Explore an independent, capability-based microkernel designed to eventually replace the monolithic Linux kernel.
- **Key Tasks:**
  - Formal specification of capability-based microkernel primitives in `research/kernel/spec/`.
  - Prototype microkernel IPC performance benchmarks in virtualized environments.
  - Investigate POSIX/Linux system call emulation architecture (ABI personality server).
  - Memory-safe implementation prototypes (Rust/seL4 integration studies).
- **Deliverables:**
  - Academic whitepaper and architectural evaluation report.
  - Proof-of-concept microkernel booting in QEMU with basic IPC and memory paging.
- **Exit Criteria:**
  - Formal evaluation of whether custom kernel IPC throughput satisfies Sagar OS userspace requirements.
