# Sagar OS Engineering & Tooling (`tools/`)

This directory contains build automation, image creation harnesses, developer utilities, and testing tools.

## Directory Structure

```text
tools/
├── build/           # Rootfs generation, live ISO mastering, and packaging scripts
└── dev/             # Local test runners, QEMU boot test harnesses, and linters
```

## Tooling Requirements
- **No Host Mutation:** Tools must never install system-wide packages or mutate host files.
- **Containerization / Chroot:** Build steps must execute inside isolated environments (Docker/Podman or unprivileged `mmdebstrap`).
- **Reproducibility:** Build tools must produce deterministic, reproducible output hashes.
