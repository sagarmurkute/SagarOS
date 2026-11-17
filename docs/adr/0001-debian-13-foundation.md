# ADR-0001: Adoption of Debian GNU/Linux 13 (Trixie) as Foundational Base

- **Status:** Accepted  
- **Date:** 2026-11-17  
- **Authors:** Sagar OS Core Architecture Team  

## Context
When building a modern, dependable operating system, engineering teams face a fundamental trade-off: build every subsystem (kernel, toolchain, drivers, standard library, networking, package manager) from scratch, or build atop an existing, battle-tested, high-assurance open-source base.

Starting completely from scratch on day one leads to immense maintenance burdens, poor hardware driver support, and years of stalled development before reaching user-facing utility. Conversely, building on a fragile or rapidly churning upstream base creates constant breakage.

## Decision
We adopt **Debian GNU/Linux 13 ("Trixie")** as the foundational base for Sagar OS.
Specifically:
- Upstream Linux LTS kernel and Debian hardware drivers provide device enablement.
- Debian standard userspace (`systemd`, `glibc`, GNU coreutils) provides the core runtime foundation.
- Debian package repositories (`deb`) serve as the baseline package ecosystem.

## Alternatives Considered
1. **Linux From Scratch (LFS) / Custom Source Build:**
   - *Rejected:* Enormous maintenance overhead; security patching every package would consume all project resources.
2. **Arch Linux Base:**
   - *Rejected:* Rolling-release model introduces frequent breaking changes that conflict with long-term stability and predictable system service development.
3. **Alpine Linux (musl + BusyBox):**
   - *Rejected:* While lightweight, musl presents compatibility challenges with many proprietary drivers, gaming runtimes, and desktop ecosystems.
4. **Immediate Custom Microkernel:**
   - *Rejected:* Developing a functional microkernel, SMP scheduler, memory manager, and complete driver ecosystem before having a working desktop environment would delay usable releases by many years.

## Consequences
### Positive
- Exceptional stability, security patching, and package availability from the Debian ecosystem.
- Immediate Tier-1 hardware support across x86_64 and AArch64 platforms.
- Development focus can be dedicated entirely to Sagar OS custom value: shell, services, applications, and architecture.

### Negative / Trade-offs
- Bound to Debian's package versions and release cadence.
- Monolithic Linux kernel architecture must be accepted in the immediate term, deferring microkernel aspirations to long-term research.
