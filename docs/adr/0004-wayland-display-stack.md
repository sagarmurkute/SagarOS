# ADR-0004: Wayland-Native Display and Compositor Stack

- **Status:** Accepted  
- **Date:** 2026-11-17  
- **Authors:** Sagar OS Core Architecture Team  

## Context
Display servers in modern Unix-like operating systems have undergone a generational shift. The legacy X11 protocol suffers from fundamental design flaws: lack of security isolation between clients, screen tearing, complex archaic extensions, and inability to properly isolate clipboard, keystrokes, and window captures.

Wayland has emerged as the modern, secure, and performant standard for Linux graphics and window management.

## Decision
1. Sagar OS adopts **Wayland as the sole native display protocol** for its desktop environment and shell (`src/shell/`).
2. The display pipeline relies directly on Linux DRM/KMS, Mesa (Vulkan/OpenGL), and `libinput`.
3. X11 will not be supported as a host display server. Legacy X11 application compatibility will be provided strictly through rootless Xwayland inside an isolated sandbox.

## Alternatives Considered
- **X11 Display Server:** Rejected due to inherent security vulnerabilities (any client can sniff keystrokes of another client) and architectural obsolescence.
- **Mir / Custom Display Protocol:** Rejected due to lack of broad toolkits and hardware ecosystem adoption compared to Wayland.

## Consequences
### Positive
- Strict security isolation between application surfaces and windows.
- Hardware-accelerated, tear-free rendering with modern refresh rate and HDR capabilities.
- Direct alignment with the modern Linux graphics stack and future Wayland protocols.

### Negative / Trade-offs
- Legacy X11 applications require Xwayland compatibility overhead.
- Requires building or tailoring a Wayland compositor stack (`wlroots` or Rust equivalent) for the Sagar OS desktop shell.
