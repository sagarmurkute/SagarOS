# Sagar OS Distribution Engineering (`distro/`)

This directory contains the distribution configuration, upstream package manifests, bootstrap profiles, and filesystem overlays that define the **Debian GNU/Linux 13 ("Trixie")** base for Sagar OS.

## Directory Structure

```text
distro/
├── manifests/       # Package selection lists, bootstrap seeds, and dependency definitions
└── overlays/        # Filesystem overlays, default configurations, artwork, and branding
```

## Guiding Principles
- **Clean Upstream Baseline:** All packages defined in manifests must resolve cleanly against official Debian 13 repositories.
- **Stateless Defaults:** System configuration overlays must place defaults in `/usr/lib/sagar/` or `/usr/share/sagar/`, avoiding unnecessary mutation of `/etc/`.
- **Modular Profiles:** Manifests are split into minimal, core, hardware, and desktop profiles.
