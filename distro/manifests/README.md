# Distribution Manifests (`distro/manifests/`)

This directory houses package lists and bootstrap profiles used to assemble the Sagar OS Debian 13 root filesystem.

## Purpose & Files (Scheduled for Phase 1)
- `base.list`: Minimal bootable Debian 13 system packages (`systemd`, `linux-image-amd64`, `glibc`, `coreutils`, `iproute2`, `apt`).
- `hardware.list`: Essential firmware, DRM graphics drivers (Mesa), wireless utilities, and audio support (`PipeWire`).
- `desktop.list`: Sagar OS runtime dependencies (Wayland libraries, font renderers, PAM modules).

## Rules
- Every package included must have a justified role in the minimal footprint.
- Bloatware and redundant packages are strictly prohibited.
