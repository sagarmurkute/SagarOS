# Feature Catalogue — Sagar OS

> **Exhaustive breakdown of planned user-facing, system, and platform features for Sagar OS.**

---

## 1. Display, Graphics & Window Management (`src/graphics/`)

| Feature ID | Feature Name | Description | Target Phase |
| :--- | :--- | :--- | :--- |
| **GFX-01** | Wayland Native Compositing | Tear-free, hardware-accelerated rendering utilizing DRM/KMS and Mesa. | Phase 3 |
| **GFX-02** | Multi-Monitor Management | Independent display refresh rates, display arrangement, and hot-plugging. | Phase 3 |
| **GFX-03** | Fractional Scaling | HiDPI and mixed-DPI display scaling with crisp font and surface rendering. | Phase 3 |
| **GFX-04** | Isolated Xwayland Sandbox | Run legacy X11 applications without allowing them to spy on Wayland windows. | Phase 3 |
| **GFX-05** | Custom Protocol Extensions | Low-overhead protocols for shell integration (`src/graphics/protocols/`). | Phase 3 |

---

## 2. Desktop Shell & Environment (`src/desktop/`)

| Feature ID | Feature Name | Description | Target Phase |
| :--- | :--- | :--- | :--- |
| **DSK-01** | Sagar Status Panel | Top/bottom panel displaying active workspaces, system indicators, and clock. | Phase 3 |
| **DSK-02** | Rapid Keyboard Launcher | Instant fuzzy-search application launcher, file search, and math calculations. | Phase 3 |
| **DSK-03** | Distraction-Free Notifications | Grouped, action-oriented notifications with "Do Not Disturb" focus mode. | Phase 3 |
| **DSK-04** | Secure Screen Lock | Hardware-accelerated lock screen backed by PAM authentication. | Phase 3 |
| **DSK-05** | Workspace Navigation | Virtual workspaces with smooth swipe gestures and keyboard switching. | Phase 3 |
| **DSK-06** | Multi-Monitor Wallpapers | Individual monitor wallpaper configuration with smooth transitions. | Phase 3 |

---

## 3. System Services & Middleware (`src/services/`)

| Feature ID | Feature Name | Description | Target Phase |
| :--- | :--- | :--- | :--- |
| **SRV-01** | Unified Config Daemon | `sagar-configd` providing atomic, stateless system configuration APIs. | Phase 2 |
| **SRV-02** | Session Coordinator | `sagar-sessiond` managing user login, seat allocation, and polkit dialogs. | Phase 2 |
| **SRV-03** | Intelligent Power Daemon | `sagar-powerd` handling lid-close actions, battery profiles, and CPU governors. | Phase 2 |
| **SRV-04** | Audio Routing Integration | PipeWire and WirePlumber automatic sink/source switching. | Phase 2 |

---

## 4. First-Party Native Applications (`src/apps/`)

| Feature ID | Feature Name | Description | Target Phase |
| :--- | :--- | :--- | :--- |
| **APP-01** | Sagar Settings | Clean, single-window control panel for displays, network, audio, and accounts. | Phase 4 |
| **APP-02** | Sagar Terminal | GPU-accelerated terminal with tabs, split panes, and modern font rendering. | Phase 4 |
| **APP-03** | Sagar Files | Fast, tabbed file manager with clean dual-pane view and archive preview. | Phase 4 |
| **APP-04** | Sagar Monitor | Real-time CPU, GPU, memory, process hierarchy, and disk I/O inspector. | Phase 4 |

---

## 5. Security, Packaging & System Resilience

| Feature ID | Feature Name | Description | Target Phase |
| :--- | :--- | :--- | :--- |
| **SEC-01** | Landlock Sandboxing | Filesystem sandboxing restricting desktop apps to designated paths. | Phase 4 |
| **SEC-02** | Stateless System Defaults | Factory defaults in `/usr/lib/sagar/` enabling instant factory reset. | Phase 2 |
| **SEC-03** | Flatpak / OCI App Delivery | Safe, sandboxed distribution for third-party software. | Phase 4 |
| **SEC-04** | Default-Drop Firewall | Pre-configured `nftables` policy blocking unsolicited inbound traffic. | Phase 1 |
| **SEC-05** | Hermetic Build Harness | Bit-for-bit reproducible Debian 13 rootfs and live ISO image builder. | Phase 1 |
