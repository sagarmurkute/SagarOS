# Feature Catalogue — Sagar OS

> **Detailed catalogue of planned user-facing, system, and platform features for Sagar OS, aligned with product scope maturity classifications.**

---

## Maturity Classification Guide

Every feature in this catalogue is mapped to an explicit maturity tier defined in [PRODUCT-SCOPE.md](PRODUCT-SCOPE.md):
- **Core Responsibility:** Essential foundational deliverable owned and maintained directly by the Sagar OS project.
- **Intended Capability:** Planned feature committed for design and implementation in target milestones.
- **Future Possibility:** Forward-looking capability under architectural consideration.
- **Not Yet Approved:** Proposed concept requiring formal review before engineering scheduling.

---

## 1. Graphics & Display Management

### GFX-01: Hardware-Accelerated Display Compositor
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 3
- **Description:** A dedicated Wayland-native display server and compositor engineered for smooth, tear-free window rendering, direct scanout, and optimal graphical throughput. Technical architecture is defined in [MASTER_SPEC.md](../../MASTER_SPEC.md).
- **User Story:** As a daily-driver user, I want windows, video playback, and animations to render smoothly without screen tearing or stutter so that interactions feel immediate and fluid.
- **Acceptance Criteria:**
  - Sustained 60+ FPS window management on standard refresh displays.
  - Zero visible screen tearing across full-screen and windowed surfaces.
  - Direct hardware rendering for foreground interactive surfaces.
- **Unresolved Details:** TBD (Exact compositor toolkit/protocol implementation under engineering review).

### GFX-02: Multi-Monitor Display Management
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 3
- **Description:** Dynamic display arrangement, independent refresh rate management, and seamless hot-plugging for external monitors and projectors.
- **User Story:** As a workstation user connecting multiple displays of varying refresh rates, I want each display to run at its native refresh rate without degrading other screens.
- **Acceptance Criteria:**
  - Independent refresh rate support across connected monitors.
  - Automatic desktop surface repositioning upon display disconnect without application crashes.
- **Unresolved Details:** TBD (VRR/Adaptive Sync across mixed-vendor multi-monitor setups).

### GFX-03: Fractional Display Scaling
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 3
- **Description:** High-DPI and mixed-DPI display scaling supporting fractional multipliers with crisp font rendering and unblurred window surfaces.
- **User Story:** As a laptop user on a high-density screen, I want the interface and text to scale cleanly without blurring or tiny unreadable UI elements.
- **Acceptance Criteria:**
  - Crisp typography and vector iconography at 125%, 150%, and 175% scaling steps.
  - Correct window coordinate mapping across boundaries between standard and HiDPI displays.
- **Unresolved Details:** TBD (Legacy X11 application scaling behavior under fractional Wayland scales).

### GFX-04: Isolated Legacy Application Compatibility
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 3
- **Description:** A secure, rootless compatibility layer allowing legacy X11 applications to execute without granting them access to sniff keystrokes or record adjacent Wayland windows.
- **User Story:** As a user running legacy software, I want older applications to launch and function seamlessly while remaining sandboxed from my modern sessions.
- **Acceptance Criteria:**
  - Legacy applications open and render within standard desktop window frames.
  - X11 processes cannot inspect global keyboard input outside their focused window.
- **Unresolved Details:** TBD.

---

## 2. Desktop Environment & Shell

### DSK-01: System Status Panel
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 3
- **Description:** An unobtrusive, persistent system panel displaying active workspaces, system indicators (network, audio volume, battery, power profile), and clock.
- **User Story:** As an everyday user, I want quick, glanceable visibility into my active workspaces, connectivity, and battery state from a clean panel.
- **Acceptance Criteria:**
  - Panel updates hardware indicators in real-time with negligible CPU usage.
  - Visual styling matches the unified light/dark design language.
- **Unresolved Details:** TBD (Final default panel placement: top bar vs. bottom taskbar pending UX review).

### DSK-02: Rapid Central Launcher
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 3
- **Description:** A keyboard-driven central command and application launcher featuring instant fuzzy search, application execution, and system command shortcuts.
- **User Story:** As a productivity user, I want to press a single key, type two characters, and hit Enter to launch any application in milliseconds.
- **Acceptance Criteria:**
  - Launcher opens instantly upon invocation.
  - Fuzzy-search indexes installed applications and system settings.
  - Fully navigable via keyboard arrow keys and Enter.
- **Unresolved Details:** TBD (Inclusion of basic math evaluation and file search in v1.0).

### DSK-03: Distraction-Free Notification Service
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 3
- **Description:** An actionable notification toast system that groups alerts by application, respects focus modes, and never steals active keyboard focus.
- **User Story:** As a writer or programmer in deep focus, I want non-critical notifications silenced automatically during focus sessions so my flow is uninterrupted.
- **Acceptance Criteria:**
  - Banners appear in a designated corner without stealing input focus.
  - One-click "Do Not Disturb" suppresses all non-critical notifications.
- **Unresolved Details:** TBD.

### DSK-04: Secure Screen Lock & Session Authentication
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 3
- **Description:** A hardware-accelerated lock screen backed by local authentication services, securing the active session during absence.
- **User Story:** As a security-conscious user, I want to lock my screen with a shortcut and know my session is inaccessible without authentication.
- **Acceptance Criteria:**
  - Screen locks immediately with zero frame leakage.
  - Session resumes cleanly upon successful password entry.
- **Unresolved Details:** TBD (Biometric / fingerprint unlock integration timeline).

### DSK-05: Virtual Workspace Management
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 3
- **Description:** Spatial virtual workspaces enabling clean separation between distinct project contexts, navigable via keyboard shortcuts and multi-touch gestures.
- **User Story:** As a multitasker, I want distinct workspaces for communication, development, and research so my screen remains uncluttered.
- **Acceptance Criteria:**
  - Workspaces switch smoothly without visual flicker.
  - Windows remain reliably pinned to their assigned workspace across sleep and wake cycles.
- **Unresolved Details:** TBD (Fixed vs. dynamic workspace allocation model).

---

## 3. Core System Services

### SRV-01: Unified Configuration Service
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 2
- **Description:** A centralized system service providing atomic, stateless configuration APIs across display, network, sound, and user preferences.
- **User Story:** As a system administrator or desktop app, I want a single, documented API to inspect and modify system settings without manually editing fragmented configuration files.
- **Acceptance Criteria:**
  - Exposes standardized IPC interfaces for all system settings.
  - Enforces vendor defaults when user configuration overrides are absent.
- **Unresolved Details:** TBD (D-Bus vs. Varlink protocol schemas under specification).

### SRV-02: Session Management Service
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 2
- **Description:** Coordinates user login, session lifecycle, unprivileged seat management, and graphical authentication prompts.
- **User Story:** As a desktop user, I want my graphical session to launch securely with proper permission boundaries and unprivileged process isolation.
- **Acceptance Criteria:**
  - Manages session lifecycle from login to logout.
  - Enforces authorization prompts for administrative actions.
- **Unresolved Details:** TBD.

### SRV-03: Adaptive Power Management Service
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 2
- **Description:** Manages device power policies, laptop lid-close behavior, display blanking, and dynamic performance/efficiency profile transitions.
- **User Story:** As a laptop user, I want my system to consume minimal power while reading or typing, and scale performance when running heavy builds.
- **Acceptance Criteria:**
  - Enters deep low-power sleep states when the lid is closed.
  - Switches between power profiles without requiring a system reboot.
- **Unresolved Details:** TBD (Automated heuristic power scaling vs. manual user profile toggles).

### SRV-04: Dynamic Audio Routing Service
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 2
- **Description:** Low-latency multimedia audio routing providing automatic input/output stream switching upon peripheral connect/disconnect.
- **User Story:** As a user plugging in headphones, I want audio output to switch immediately and smoothly without stuttering or manual reconfiguration.
- **Acceptance Criteria:**
  - Auto-switches default sink/source upon audio device connection.
  - Independent volume balance memory per output device.
- **Unresolved Details:** TBD.

---

## 4. First-Party Native Applications

### APP-01: Sagar Settings
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 4
- **Description:** A centralized graphical control center for displays, networks, audio, Bluetooth, power profiles, and user accounts.
- **User Story:** As an everyday user, I want one single settings app to configure my entire machine without navigating legacy control panels.
- **Acceptance Criteria:**
  - Single-window interface with clean sidebar navigation.
  - Changes apply immediately without modal confirmation dialogs.
- **Unresolved Details:** TBD.

### APP-02: Sagar Terminal
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 4
- **Description:** A fast, GPU-accelerated terminal emulator designed for high throughput, tabbed sessions, split panes, and clean font rendering.
- **User Story:** As a developer, I want a lightweight, instant-launch terminal that renders large compiler outputs smoothly without lagging.
- **Acceptance Criteria:**
  - GPU-accelerated text rendering with sub-frame latency.
  - Native split-pane and tab navigation via keyboard shortcuts.
- **Unresolved Details:** TBD (Configurable keymap bindings format).

### APP-03: Sagar Files
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 4
- **Description:** A clean, responsive file manager supporting tabbed browsing, optional dual-pane navigation, and quick document preview.
- **User Story:** As a knowledge worker, I want to quickly organize, preview, and move files across directories without UI delays.
- **Acceptance Criteria:**
  - Instant directory loading with asynchronous metadata indexing.
  - Safe file operations with non-punitive undo support for accidental deletions.
- **Unresolved Details:** TBD.

### APP-04: Sagar Monitor
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 4
- **Description:** A real-time system resource inspector displaying CPU, GPU, memory allocation, process hierarchies, and network/disk activity.
- **User Story:** As a power user, I want to see which processes are consuming RAM or CPU and easily terminate runaway tasks.
- **Acceptance Criteria:**
  - Real-time performance graphs with low monitoring overhead.
  - Detailed per-process tree view with search filtering.
- **Unresolved Details:** TBD.

---

## 5. Security, Packaging & System Resilience

### SEC-01: Application Process Sandboxing
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 4
- **Description:** Filesystem and syscall sandboxing restricting desktop applications to authorized file paths and isolated device nodes (technical details in [MASTER_SPEC.md](../../MASTER_SPEC.md)).
- **User Story:** As a user downloading third-party software, I want confidence that untrusted apps cannot read my private documents or access my webcam without permission.
- **Acceptance Criteria:**
  - Sandboxed applications run in restricted namespaces without arbitrary home-directory access.
- **Unresolved Details:** TBD (Fine-grained portal permission prompt design).

### SEC-02: Stateless System Defaults
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 2
- **Description:** Vendor default configurations are stored in dedicated distribution directories, keeping host configuration directories pristine and enabling instant factory reset.
- **User Story:** As a user who misconfigured system files, I want to reset to factory defaults without re-installing the operating system.
- **Acceptance Criteria:**
  - Removing custom configuration overrides restores default working state on next boot.
- **Unresolved Details:** TBD.

### SEC-03: Sandboxed Application Delivery Support
- **Maturity Tier:** Intended Capability
- **Target Phase:** Phase 4
- **Description:** Built-in runtime support for third-party sandboxed desktop applications (formal selection of primary packaging standard pending evaluation).
- **User Story:** As a user, I want to install modern desktop applications cleanly without risking system package dependency conflicts.
- **Acceptance Criteria:**
  - Supports installing and running isolated third-party desktop applications.
- **Unresolved Details:** TBD (Evaluation of Flatpak as the primary graphical runtime pending approval).

### SEC-04: Default-Drop Inbound Network Firewall
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 1
- **Description:** A pre-configured inbound network firewall that rejects unsolicited incoming connections out of the box (technical architecture in [MASTER_SPEC.md](../../MASTER_SPEC.md)).
- **User Story:** As a user connecting to public coffee-shop Wi-Fi, I want my machine protected against unauthorized incoming connection attempts automatically.
- **Acceptance Criteria:**
  - Default-drop policy for all unsolicited inbound network packets.
  - Established outbound connections function normally without manual rule configuration.
- **Unresolved Details:** TBD.

### SEC-05: Reproducible Rootfs & Live Image Builder
- **Maturity Tier:** Core Responsibility
- **Target Phase:** Phase 1
- **Description:** An isolated, containerized build harness capable of generating a minimal, bootable Debian 13 rootfs and hybrid UEFI installation image.
- **User Story:** As a distribution maintainer, I want deterministic, bit-for-bit reproducible image builds directly from package manifests.
- **Acceptance Criteria:**
  - Clean build execution without modifying the host operating system.
  - Generates bootable ISO and disk images verified via automated QEMU smoke tests.
- **Unresolved Details:** TBD (Final selection of live installation framework pending evaluation).
