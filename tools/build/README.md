# Image & Rootfs Build Tools (`tools/build/`)

This directory will contain scripts and tooling for building Sagar OS installation and live images.

## Planned Tools (Phase 1)
- `build-rootfs.sh`: Uses `mmdebstrap` inside an isolated container to generate a minimal Debian 13 root filesystem according to `distro/manifests/`.
- `build-image.sh`: Takes the rootfs output and builds a bootable hybrid UEFI/BIOS ISO or QCOW2 virtual machine image.
- `package-deb.sh`: Packages Sagar OS custom services and shell into valid Debian packages.

## Guidelines
- Must run cleanly in CI environments without requiring root privileges on the host (e.g., using user namespaces).
- Output artifacts are strictly git-ignored.
