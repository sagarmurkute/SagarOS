# Sagar OS Custom Source Tree (`src/`)

This directory is the dedicated home for all custom software authored specifically for **Sagar OS**.

## Directory Structure

```text
src/
├── core/            # Foundation system abstractions, low-level utilities (libsagar-core)
├── libraries/       # Shared domain libraries, client SDKs, and component toolkits
├── services/        # System daemons, background services, D-Bus coordinators
├── graphics/        # Wayland compositor, display server, and protocols/
├── desktop/         # Desktop shell components (panel, launcher, notifications, session UI)
├── shell/           # Integrated shell environment reference
└── apps/            # Native first-party Sagar OS desktop applications
```

## Status & Governance Notice
> [!IMPORTANT]
> **We are currently in Phase 0.**  
> In accordance with project requirements and [ROADMAP.md](../ROADMAP.md), **no application code, desktop implementations, drivers, or kernel code are authored yet.**
> 
> Implementation will commence systematically when Phase 2 and Phase 3 are formally opened.
