# ADR-0002: Strict Separation of Custom and Upstream Components

- **Status:** Accepted  
- **Date:** 2026-11-17  
- **Authors:** Sagar OS Core Architecture Team  

## Context
Many derivative Linux distributions fail over time because they indiscriminately patch upstream packages, mix custom scripts into root directories, and make it impossible to cleanly update or audit the system. Over time, "dependency hell" and upstream divergence make maintenance unsustainable.

## Decision
We enforce a strict physical and logical boundary between **Debian Upstream Components** and **Sagar OS Custom Components**:
1. Upstream packages must not be modified with proprietary, unversioned patches unless managed via explicit Debian source packaging (`distro/manifests/`).
2. All Sagar OS custom software lives in `src/` (`src/core/`, `src/services/`, `src/shell/`, `src/apps/`).
3. Distribution configs, filesystem overlays, and branding reside cleanly in `distro/overlays/`.
4. Sagar default configurations install into `/usr/lib/sagar/` or `/usr/share/sagar/`, leaving `/etc` pristine for local user overrides.

## Alternatives Considered
- **In-place patching of Debian packages:** Rejected due to high maintenance overhead and recurring merge conflicts during security updates.
- **Monolithic single repository mix:** Rejected because it obscures ownership and prevents independent testing of custom subsystems.

## Consequences
### Positive
- Standard Debian security updates can be applied without breaking custom Sagar OS software.
- Custom components can be compiled, tested, and packaged independently.
- Clean architectural layers improve code readability and onboarding for contributors and AI agents.

### Negative / Trade-offs
- Requires careful packaging and overlay tooling in `tools/build/`.
- Requires designing Sagar OS services to interact via standard interfaces (D-Bus, sockets, file configs) rather than monkey-patching existing system scripts.
