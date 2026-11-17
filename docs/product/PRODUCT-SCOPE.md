# Product Scope & Functional Boundaries — Sagar OS

> **Defining the functional scope, boundaries, evolutionary stages, and explicit non-goals for Sagar OS as a universal desktop operating system.**

---

## 1. Product Scope Overview

Sagar OS is designed as a **universal desktop operating system** intended to serve as a primary daily-driver platform. Its product goal is to combine the broad versatility of general-purpose desktop operating systems with the resource discipline, responsiveness, and visual polish of modern platforms, animated by an independent identity: **Beautiful, Fast, and Capable**.

To maintain engineering discipline and prevent feature bloat, this document establishes clear functional boundaries across all operating system domains, categorizing items by maturity and approval level:
- **Core Product Responsibility:** Foundational deliverables owned, authored, and supported directly by the Sagar OS project.
- **Intended Capabilities:** Planned features targeted for early release milestones.
- **Future Possibilities:** Forward-looking enhancements under architectural consideration.
- **Capabilities Not Yet Approved:** Proposed ideas requiring formal product and architectural review before commitment.

---

## 2. Core Operating System Experience

- **Core Product Responsibility:**
  - Providing a bootable, stable desktop workstation environment built on a Debian GNU/Linux 13 ("Trixie") foundation.
  - Ensuring fast startup, seamless authentication, and reliable session persistence.
- **Intended Capabilities:**
  - Fast boot-to-desktop times with quiet, unbloated startup initialization.
  - Predictable session suspension and immediate resumption on laptop lid-open.
  - Stateless system defaults enabling instant factory-level configuration recovery.
- **Future Possibilities:**
  - Dynamic user-state snapshots and transactional operating system rollback.
- **Capabilities Not Yet Approved:**
  - Immutable root filesystem deployment model (currently under architectural evaluation).

---

## 3. Desktop Environment and User Interface

- **Core Product Responsibility:**
  - Custom Wayland-native display and compositing environment with an integrated desktop shell.
  - Original Sagar OS visual identity, high-contrast typography, and unified light/dark appearance.
- **Intended Capabilities:**
  - Hardware-accelerated window compositing maintaining consistent 60+ FPS without screen tearing.
  - Desktop status panel providing active workspace indicators, clock, and hardware status indicators.
  - Rapid keyboard-driven application launcher with instant fuzzy search.
  - Dynamic floating window management paired with intuitive smart tiling (half-screen and quadrant snapping).
  - Multi-monitor management supporting independent display arrangements and fractional scaling.
  - Actionable, non-intrusive desktop notification toasts with one-click "Do Not Disturb" focus mode.
- **Future Possibilities:**
  - Advanced multi-finger gesture navigation for touchpads and touchscreens.
  - Dynamic wallpaper transition engine with multi-display independence.
- **Capabilities Not Yet Approved:**
  - Dedicated automatic tiling mode (i3/Sway-style auto-tiling) as a native built-in feature.

---

## 4. System Management and Settings

- **Core Product Responsibility:**
  - A unified, centralized graphical settings application providing complete control over system configurations.
  - Elimination of fragmented, duplicate, or legacy control panels.
- **Intended Capabilities:**
  - Display settings: resolution, refresh rates, scaling factor, and monitor alignment.
  - Network and connectivity controls (Wi-Fi scanning, Ethernet, VPN profiles, Bluetooth pairing).
  - Audio device selection, input/output volume balance, and default device routing.
  - User accounts, passwords, and local privilege authentication.
  - Power profiles: adaptive battery-saving, balanced, and performance management.
- **Future Possibilities:**
  - Backup and restore utility for personal user data and application state.
- **Capabilities Not Yet Approved:**
  - Cloud-synced profile settings (conflicts with the zero-telemetry, local-first policy unless purely self-hosted).

---

## 5. Applications and Software Ecosystem

- **Core Product Responsibility:**
  - A focused suite of essential, native first-party applications sharing a consistent design language.
  - Secure application delivery model supporting sandboxed third-party applications.
- **Intended Capabilities:**
  - First-party native applications:
    - Sagar Settings: Centralized system configuration.
    - Sagar Terminal: Fast, GPU-accelerated terminal emulator with tab and split support.
    - Sagar Files: Clean, tabbed file manager with dual-pane viewing and quick preview.
    - Sagar Monitor: Real-time system resource, process, and hardware performance inspector.
  - Isolated sandboxed execution for third-party software (Flatpak / OCI application runtimes).
- **Future Possibilities:**
  - Curated, graphical software discovery catalog emphasizing verified, sandboxed applications.
- **Capabilities Not Yet Approved:**
  - First-party creative apps (photo editor, audio workstation) or specialized office suites authored by the core team.

---

## 6. Gaming and Entertainment

- **Core Product Responsibility:**
  - Providing an unencumbered, low-overhead graphics pipeline that allows games and multimedia to utilize full hardware power.
- **Intended Capabilities:**
  - Low-latency Wayland graphics throughput with variable refresh rate (VRR / Adaptive Sync) support.
  - Isolated Xwayland compatibility environment for legacy games and windowed titles.
  - Automatic performance prioritization that allocates full GPU/CPU power to the foreground game window.
  - Plug-and-play support for standard USB and Bluetooth game controllers.
- **Future Possibilities:**
  - Integration with cross-platform gaming runtimes and compatibility layers.
- **Capabilities Not Yet Approved:**
  - Proprietary anti-cheat kernel module emulation (fundamentally out-of-scope for the base OS).

---

## 7. Development and Productivity

- **Core Product Responsibility:**
  - A first-class environment for software engineering, research, and technical productivity.
- **Intended Capabilities:**
  - Native POSIX standard compliance and access to Debian 13 development packages and toolchains.
  - High RAM availability at idle, reserving maximum memory for compiling, local containers, and IDEs.
  - Keyboard-first interaction model minimizing friction between editor, terminal, and browser.
- **Future Possibilities:**
  - Integrated containerized developer environments (isolated dev containers).
- **Capabilities Not Yet Approved:**
  - Proprietary developer IDE authored by the core operating system team.

---

## 8. Security, Privacy and Reliability

- **Core Product Responsibility:**
  - An operating system that places user privacy, hardware control, and system stability above commercial data collection.
- **Intended Capabilities:**
  - Strict privacy by default: complete absence of commercial telemetry, behavioral tracking, or unsolicited data transmission.
  - Default-drop inbound network firewall blocking unsolicited inbound connections (technical architecture detailed in [MASTER_SPEC.md](../../MASTER_SPEC.md)).
  - Application process sandboxing restricting access to the user home directory and sensitive peripheral devices.
  - Clear privilege separation: system hardware daemons run isolated from unprivileged desktop user sessions.
  - User-controlled updates: zero forced reboots during active sessions.
- **Future Possibilities:**
  - Hardware-backed full-disk encryption with automated TPM2 unlock.
- **Capabilities Not Yet Approved:**
  - Mandatory remote attestation or locked boot chains restricting user root access.

---

## 9. Hardware and Device Support

- **Core Product Responsibility:**
  - Tier-1 hardware enablement on contemporary 64-bit platforms utilizing Debian 13 upstream drivers.
- **Intended Capabilities:**
  - Primary architectures: `x86_64` (AMD64) and `aarch64` (64-bit ARM with UEFI/ACPI).
  - Complete support for modern Intel, AMD, and mobile GPU hardware via upstream graphics acceleration drivers (see [MASTER_SPEC.md](../../MASTER_SPEC.md)).
  - Plug-and-play peripheral support: external storage, USB-C docks, keyboards, mice, audio DACs.
  - Predictable battery management and power conservation for laptops.
- **Future Possibilities:**
  - Specialized performance tuning profiles for handheld gaming PCs and compact mini-PCs.
- **Capabilities Not Yet Approved:**
  - Proprietary legacy hardware support requiring obsolete kernel drivers.
  - Formal support for legacy 32-bit (x86) architectures.

---

## 10. Networking and Connectivity

- **Core Product Responsibility:**
  - Reliable, low-friction network connection management for home, campus, and enterprise environments.
- **Intended Capabilities:**
  - Seamless Wi-Fi scanning, connection, and captive portal detection.
  - Wired Gigabit/10G Ethernet auto-negotiation.
  - Bluetooth audio and input device pairing with automatic reconnection.
  - VPN profile configuration directly from the system settings interface.
- **Future Possibilities:**
  - Native local peer-to-peer file transfer protocol between Sagar OS devices on the same local network.
- **Capabilities Not Yet Approved:**
  - Cloud-routed mesh networking managed by external commercial servers.

---

## 11. Accessibility and Internationalization

- **Core Product Responsibility:**
  - An operating system that is fundamentally usable by diverse users regardless of ability or language.
- **Intended Capabilities:**
  - High-contrast visual modes designed to promote high legibility and contrast across core typography as general design goals, while formal accessibility standards and compliance certifications remain open and unresolved.
  - Scalable system fonts and cursor sizes without layout breakage.
  - Complete keyboard navigability across the desktop shell, panel, launcher, and first-party apps.
  - UTF-8 standard encoding across all filesystem, terminal, and UI surfaces.
- **Future Possibilities:**
  - Integration with modern screen readers and assistive technology APIs.
  - Community localization infrastructure for multi-language translations.
- **Capabilities Not Yet Approved:**
  - AI-driven real-time speech-to-text transcription built directly into the base OS offline.

---

## 12. Out-of-Scope Areas (Explicit Non-Goals)

To preserve focus and maintain software quality, the following areas are **explicitly out-of-scope**:

1. **Monetized Telemetry & Tracking:** No advertising networks, usage tracking, or commercial telemetry will ever be included.
2. **Bundled Bloatware:** No third-party commercial software, sponsored games, or trialware will be pre-installed.
3. **Mandatory Cloud Accounts:** The operating system will never require an online account or cloud registration to install, boot, or operate.
4. **Native X11 Display Server:** X11 is not supported as a native host display server. X11 compatibility is strictly confined to an isolated Xwayland sandbox.
5. **Premature Custom Kernel in Production:** Sagar OS will not attempt to ship or fake an independent kernel in production releases. Production runs on the Debian-supported Linux LTS kernel.
6. **Server & Headless Infrastructure Specialization:** Sagar OS is fundamentally designed as an interactive desktop workstation; cloud virtualization host or headless server profiles are not primary product targets.

---

## 13. Current Limitations and Dependencies

1. **Debian 13 Baseline Cadence:** Release versions of upstream base libraries and Linux LTS kernels are bound to Debian 13 ("Trixie") package timelines and security updates.
2. **Third-Party Application Compatibility:** Proprietary applications built exclusively for Windows or macOS are not guaranteed to run natively; compatibility relies on standard web runtimes, containerization, or community emulation layers.
3. **Phase 0 Status:** The project is in Phase 0 (Specification & Architecture). No application binaries, desktop shell executables, or drivers are implemented yet.

---

## 14. Scope Evolution Across Phases

```mermaid
flowchart LR
    P1["Phase 1: Minimal Bootable Base"] --> P2["Phase 2: System Services & Middleware"]
    P2 --> P3["Phase 3: Wayland Compositor & Shell"]
    P3 --> P4["Phase 4: First-Party Apps & Daily Driver"]
    P4 --> P5["Phase 5: Kernel Research (Quarantined)"]
```

- **Phase 1 (v0.1):** Minimal bootable Debian 13 rootfs, UEFI ISO image, console verification in QEMU.
- **Phase 2 (v0.2):** Core middleware, system services (Unified Configuration Service, Session Management Service), stateless configuration defaults.
- **Phase 3 (v0.3):** Custom Wayland compositor (`src/graphics/`), desktop shell (`src/desktop/`), multi-monitor support, status panel, launcher.
- **Phase 4 (v0.8 – v1.0):** Native first-party apps (`src/apps/`), sandboxing, installer integration, daily-driver hardware polish.
- **Phase 5 (Long-Term):** Capability-based microkernel research strictly in `research/kernel/`.

---

## 15. Unresolved Product-Scope Decisions Requiring Approval

The following scope boundaries remain open for formal product owner ratification:

1. **Immutable Root Filesystem Architecture:** Formally decide whether Sagar OS v1.0 should enforce a read-only immutable root filesystem (e.g., using Btrfs snapshots / OSTree-like model), or standard writable root with stateless `/usr/lib/sagar` defaults.
2. **Default Third-Party Application Delivery:** Formally approve whether Flatpak is the primary recommended third-party desktop application delivery mechanism out-of-the-box.
3. **Scope of Native Accessibility Services for v1.0:** Define whether full screen-reader integration is a mandatory gate for v1.0 GA or scheduled as an immediate post-1.0 milestone.
4. **Scope of First-Party Software Store:** Confirm whether v1.0 will include a graphical application store GUI, or if initial application management will be handled via verified CLI tools and Flatpak portals.
