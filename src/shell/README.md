# Sagar OS Wayland Compositor & Shell (`src/shell/`)

This directory will contain the native Wayland compositor, window manager, and desktop shell environment.

## Planned Scope (Phase 3)
- `sagar-compositor`: Hardware-accelerated Wayland compositor using DRM/KMS, Mesa, and `libinput`.
- `sagar-panel`: Status bar, system tray, clock, workspace switcher, and hardware indicators.
- `sagar-launcher`: Fast, searchable keyboard-centric application and command launcher.
- `sagar-lock`: Secure Wayland screen lock interface using PAM authentication.
- `sagar-notifications`: Desktop notification daemon implementing the freedesktop notification specification.

## Architectural Constraints
- Pure Wayland-native design (ADR-0004).
- High-efficiency rendering targeting consistent 60+ FPS without screen tearing.
- Strict client isolation: no client sniffing or unauthorized keylogging.
- No implementation code is present during Phase 0.
