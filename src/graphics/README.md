# Sagar OS Graphics & Display Server (`src/graphics/`)

This directory contains the display server, compositor architecture, and rendering pipeline for **Sagar OS**.

## Purpose & Scope
- **Compositor Engine:** Low-level Wayland compositor interacting directly with Linux DRM/KMS, Mesa (Vulkan/OpenGL), and `libinput`.
- **Display Server Pipeline:** Mode-setting, output management, hardware-accelerated surface composition, and frame scheduling.
- **Protocol Definitions:** Wayland protocol interfaces and custom extension XML definitions in [`protocols/`](protocols/).

## Architectural Boundaries
- Strictly separated from desktop shell user interface components (`src/desktop/`).
- Operates as a pure Wayland display server; legacy X11 support is delegated to sandboxed Xwayland.
- Adheres to Phase discipline: no implementation code is generated during Phase 0.
