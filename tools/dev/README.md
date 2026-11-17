# Developer & Verification Tools (`tools/dev/`)

This directory will contain developer tools, test harnesses, and automated verification scripts.

## Planned Utilities (Phase 1 & 2)
- `run-qemu.sh`: Launches the generated Sagar OS ISO or disk image inside QEMU with hardware acceleration (KVM) or software emulation.
- `verify-manifest.sh`: Validates package dependencies and conflicts in `distro/manifests/`.
- `lint-docs.sh`: Validates markdown formatting, dead relative links, and Mermaid diagram syntax across `docs/`.

## Execution Protocol
- Developer utilities should provide clear terminal output and adhere to standard exit codes (0 for success, non-zero for failure).
