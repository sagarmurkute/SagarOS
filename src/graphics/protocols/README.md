# Sagar OS Wayland Protocols (`src/graphics/protocols/`)

This directory houses the protocol specifications and XML interface definitions for Wayland extensions used by the Sagar OS graphics stack and desktop components.

## Planned Scope
- Upstream Wayland protocol XML imports (e.g., `xdg-shell`, `wlr-layer-shell`, `linux-dmabuf`).
- Custom Sagar OS protocol extensions for secure session coordination, output configuration, and shell integration.

## Guidelines
- Protocol files must use standard Wayland XML protocol definitions.
- Custom extensions must be documented in `docs/specs/` prior to standardization.
- No implementation code is present during Phase 0.
