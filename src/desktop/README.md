# Sagar OS Desktop Shell & Environment (`src/desktop/`)

This directory contains the desktop shell user interface components, workspace management, and visual system environment for **Sagar OS**.

## Planned Desktop Components (Phase 3)
- `panel/`: System status bar, clock, system tray, workspace indicator, and hardware monitors.
- `launcher/`: Keyboard-driven application launcher and system command palette.
- `notifications/`: Desktop notification server conforming to the freedesktop notification specification.
- `session-ui/`: Session management dialogs (logout, restart, suspend, power off) and lock screen interface.
- `wallpaper/`: Background rendering and multi-monitor wallpaper daemon.

## Architectural Boundaries
- Interacts with the display server (`src/graphics/`) strictly via standard Wayland protocols (`xdg-shell`, `wlr-layer-shell`).
- Communicates with system services (`src/services/`) via standard D-Bus / Varlink IPC interfaces.
- Completely decoupled from the low-level compositor engine.
- No implementation code is present during Phase 0.
