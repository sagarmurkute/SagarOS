# Distribution Filesystem Overlays (`distro/overlays/`)

This directory contains static filesystem overlays that are layered on top of the Debian 13 base rootfs during image generation.

## Purpose & Organization (Scheduled for Phase 1 & 2)
- `base/`: Baseline OS configurations, default OS release identity (`/etc/os-release`), and systemd preset policies.
- `branding/`: Wallpapers, logos, Plymouth boot themes, and icons.
- `desktop/`: Default environment variables, Wayland session desktop files, and terminal themes.

## Rules
- Never commit binary blobs or compiled programs here.
- Maintain stateless configuration rules: prefer `/usr/lib/sagar/` and `/usr/share/sagar/` over dirty `/etc/` edits.
