# ADR-0003: Long-Term Independent Kernel Research Strategy

- **Status:** Accepted  
- **Date:** 2026-11-17  
- **Authors:** Sagar OS Core Architecture Team  

## Context
A primary long-term ambition for Sagar OS is to explore an independent, high-assurance, capability-based microkernel or custom hybrid kernel architecture. Monolithic kernels (including Linux) expose a massive attack surface in Ring 0 and lack formal isolation between drivers and the core scheduler.

However, developing a production-ready independent kernel requires extensive research, formal verification, and multi-year engineering. Claiming or faking that such a kernel exists prematurely would mislead users, degrade project credibility, and cause architectural confusion.

## Decision
1. We explicitly declare that **Sagar OS currently runs on the Linux kernel provided by Debian 13**.
2. All research, theoretical papers, architectural specifications, memory models, and proof-of-concept code for an independent kernel are quarantined strictly inside [`research/kernel/`](../../research/kernel/).
3. Kernel research will not be included in production rootfs or live ISO builds until Phase 5 exit criteria are formally satisfied.
4. Any future kernel must provide POSIX/Linux ABI compatibility (via an emulation server or runtime layer) to preserve compatibility with Sagar OS userspace components.

## Alternatives Considered
- **Faking a custom kernel by renaming the Linux kernel binary:** Strictly rejected as deceptive and technically dishonest.
- **Abandoning independent kernel research entirely:** Rejected because long-term operating system innovation requires exploring modern capability-based security and memory safety at the kernel level.
- **Starting with a custom microkernel immediately:** Rejected because it would stall all user-facing desktop and application progress for years.

## Consequences
### Positive
- Transparent, honest engineering stance establishing deep technical credibility.
- Safe sandbox for advanced systems research without risking the stability of the production Debian 13 baseline.
- Clear evolutionary target for Phase 5.

### Negative / Trade-offs
- Maintaining two tracks (production Linux base vs. long-term microkernel research) requires disciplined governance and clear documentation boundaries.
