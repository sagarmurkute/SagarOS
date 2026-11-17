# MASTER_SPEC.md — Sagar OS Master Technical Specification

> **Status:** Active / Inception  
> **Version:** 0.1.0  
> **Target Release:** Sagar OS 1.0 (Debian 13 Baseline)

---

## 1. Executive Summary

**Sagar OS** is a modern, modular operating system designed to deliver high performance, predictable system behavior, uncompromising stability, and clean architectural boundaries. 

The project follows a two-horizon architectural approach:
1. **Horizon 1 (Current & Production Baseline):** A meticulously engineered, highly refined distribution built atop **Debian GNU/Linux 13 ("Trixie")**, featuring a custom Wayland-native desktop shell, bespoke system services, and clean component isolation.
2. **Horizon 2 (Long-Term Research):** A dedicated, multi-year exploration of an independent, memory-safe, capability-based microkernel architecture, designed to eventually replace the monolithic Linux kernel while preserving userspace ABI compatibility.

---

## 2. Platform & Hardware Baseline

### 2.1 Target Architectures
- **Primary Tier 1 Target:** `x86_64` (AMD64, modern UEFI systems).
- **Secondary Tier 1 Target:** `aarch64` (ARM64, standard UEFI/ACPI or DeviceTree platforms).

### 2.2 Boot & Firmware Environment
- **Firmware Support:** UEFI 2.x+ (64-bit). Legacy BIOS/CSM is considered non-essential and will not be prioritized.
- **Bootloader:** GRUB 2 / systemd-boot with secure boot chain capability.
- **Kernel Image:** Debian-signed Linux kernel LTS image with initramfs generated via `dracut` or `initramfs-tools`.

---

## 3. Foundational Base: Debian GNU/Linux 13 (Trixie)

### 3.1 Base Userspace
- **Upstream Distribution:** Debian GNU/Linux 13 ("Trixie").
- **Init & Service Manager:** `systemd` (standardized service supervision, cgroup v2 resource management, journal logging).
- **C Standard Library:** `glibc` (upstream Debian).
- **Core Utilities:** GNU `coreutils`, `util-linux`, `findutils`, `bash`.
- **Hardware Abstraction & Devices:** `udev`, `kmod`, standard Linux sysfs/procfs interfaces.

### 3.2 Upstream Dependency Rationale
Using Debian 13 as the base foundation guarantees:
- High security response standards from the Debian Security Team.
- Broad hardware driver compatibility via upstream Linux kernel and Mesa graphics stack.
- Stability and predictability across all core POSIX subsystems.

---

## 4. Component Separation & Architecture Layers

Sagar OS enforces strict layering to prevent architectural degradation.

```text
+-------------------------------------------------------------+
|                Sagar OS First-Party Apps                    |
|             (Native, Focused, Sandboxed Apps)               |
+-------------------------------------------------------------+
|               Sagar OS Shell & Desktop Stack                |
|      (Wayland Compositor, Session UI, Panel, Launcher)       |
+-------------------------------------------------------------+
|               Sagar OS Services & Middleware                |
|     (Identity, System Configuration Daemon, Audio/PipeWire) |
+=============================================================+  <-- Architectural Boundary
|                Debian GNU/Linux 13 Userspace                |
|       (systemd, glibc, GNU coreutils, apt, PAM, D-Bus)      |
+-------------------------------------------------------------+
|            Monolithic Linux Kernel & Device Drivers         |
|         (Debian Upstream Linux LTS, DRM/KMS, Evdev)         |
+-------------------------------------------------------------+
|                      Target Hardware                        |
|                  (x86_64 / AArch64 Platforms)               |
+-------------------------------------------------------------+
```

### Component Ownership Rules:
1. **Debian Base Layer (`distro/`):** Pure Debian 13 packages pulled without invasive source patching. Configuration overlays and package manifests define the exact base footprint.
2. **Sagar OS Custom Layer (`src/`):** All custom software developed by the Sagar OS team resides here, building on top of standard POSIX/Linux APIs.
3. **Research Layer (`research/`):** Independent kernel and microkernel design papers, specifications, and prototypes. Completely decoupled from the current runtime.

---

## 5. Subsystem Specifications

### 5.1 Display & Compositing Stack
- **Protocol:** Pure Wayland. X11 is not supported natively in the core desktop; Xwayland will be available strictly as an isolated compatibility fallback.
- **Graphics Pipeline:** Direct Rendering Manager (DRM) / Kernel Mode Setting (KMS) with Mesa (Vulkan / OpenGL).
- **Input Stack:** `libinput` integrated directly into the custom Sagar Wayland compositor (`src/shell/`).
- **Audio Stack:** `PipeWire` with `WirePlumber` session management.

### 5.2 Storage & File System Hierarchy
- **Standard:** Strict adherence to Filesystem Hierarchy Standard (FHS 3.0).
- **Root Filesystem:** Read-only / immutable root support as a primary design target (e.g., Btrfs with snapshots or OSTree-compatible model).
- **User State Separation:** All persistent user data strictly contained in `/home/$USER`, adhering to XDG Base Directory Specification.
- **System Configuration:** `/etc` reserved for local host state; default system configurations packaged in `/usr/lib/sagar/` or `/usr/share/sagar/`.

### 5.3 Security Model
- **Process Isolation:** cgroups v2 resource accounting and limits for all system units and user sessions.
- **Mandatory Access Control (MAC):** AppArmor profiles for custom Sagar OS services and untrusted applications.
- **Sandboxing:** Unprivileged user namespaces, `seccomp-bpf` filtering, and Landlock LSM for application sandboxing.
- **Privilege Elevation:** `polkit` for graphical authentication; minimal `sudo` configuration for administrative tasks.

### 5.4 Networking & Connectivity
- **Backend:** `NetworkManager` or `systemd-networkd` with standard D-Bus management APIs.
- **Firewall:** `nftables` with a default-drop policy for unsolicited incoming connections.

---

## 6. Long-Term Independent Kernel Vision

### 6.1 Purpose & Motivation
While the monolithic Linux kernel provides immediate hardware compatibility and a mature ecosystem, a future custom kernel for Sagar OS aims to explore:
- **Capability-Based Security:** Object capabilities replacing ambient Unix permissions at the kernel level.
- **Microkernel Reliability:** Drivers, filesystems, and network stacks running in isolated user address spaces to eliminate kernel panics from driver faults.
- **Memory Safety:** Implementation in a memory-safe systems programming language (e.g., Rust) with formal verification of core scheduling and IPC primitives.

### 6.2 Reality Declaration & Constraints
- **Current State:** Research, formal modeling, and conceptual prototyping only.
- **Location:** All work on this initiative is restricted to `research/kernel/`.
- **Userspace Compatibility Goal:** Any future independent kernel must maintain a high-performance Linux/POSIX ABI emulation layer (either via personality servers or microkernel IPC gateways) to guarantee continuity with the Sagar OS userspace.

---

## 7. Build System & Reproducibility Requirements

1. **Hermetic Builds:** All build scripts under `tools/build/` must be containerized or run inside clean chroot environments (`mmdebstrap` / `debootstrap`).
2. **Determinism:** Build outputs (rootfs images, ISOs, Debian packages) must aim for bit-for-bit reproducibility.
3. **No Host Pollution:** The build system must never modify the host operating system's files or install global dependencies without explicit sandboxing.
