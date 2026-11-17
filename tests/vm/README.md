# Virtual Machine & Image Boot Tests (`tests/vm/`)

This directory contains automated end-to-end boot tests executed inside virtualized QEMU environments.

## Planned Scope
- Headless QEMU boot verification testing generated ISO and disk images.
- Verification of clean systemd target activation (`multi-user.target`, `graphical.target`).
- Boot-time regression testing (verifying boot-to-prompt times under 5 seconds).
