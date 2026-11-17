# Sagar OS System Services & Daemons (`src/services/`)

This directory will contain custom system daemons and background coordinators that integrate with Debian's `systemd` supervisor.

## Planned Scope (Phase 2)
- `sagar-sessiond`: User session manager and display manager coordinator.
- `sagar-configd`: Unified system configuration daemon providing D-Bus/Varlink endpoints.
- `sagar-powerd`: Device power policy daemon (lid switch, battery conservation, dynamic CPU scaling profiles).
- `sagar-polkit-agent`: Authentication agent for privileged desktop operations.

## Boundaries
- Clear privilege separation: root services handle hardware mutations; session daemons run strictly unprivileged.
- All IPC contracts must be documented in `docs/specs/` before implementation begins.
- No implementation code is present during Phase 0.
