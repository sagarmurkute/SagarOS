# Sagar OS

> **A modern, modular, and resilient operating system project.**

Welcome to the foundational repository of **Sagar OS**. This project is a long-term operating system initiative aimed at delivering a coherent, robust, and distraction-free computing experience with strict architectural discipline, high security, and performance.

---

## 1. Architectural Philosophy & Strategy

Building a resilient, production-ready operating system requires a pragmatic, staged engineering roadmap rather than rebuilding the entire universe on day one.

### Initial Foundation: Debian GNU/Linux 13 (Trixie)
The primary and immediate foundation of Sagar OS is **Debian GNU/Linux 13 ("Trixie")**. Leveraging Debian provides:
- Uncompromising stability, rock-solid package reliability, and rigorous security updates.
- Battle-tested hardware enablement across contemporary x86_64 and AArch64 systems.
- A mature ecosystem of developer tools, system utilities, and POSIX compliance.

### Long-Term Ambition: Independent Kernel Research
While Sagar OS is powered by Debian GNU/Linux today, our long-term vision includes research into an independent, purpose-built kernel (such as a verified capability-based microkernel). 

> **Important Reality Check:**
> **Sagar OS does NOT currently possess a custom kernel.** We explicitly do not pretend or simulate an existing independent kernel. The current kernel is the upstream Linux kernel supplied and supported by Debian 13. Research, specifications, and academic explorations for a future independent kernel live strictly in the [`research/kernel/`](research/kernel/) directory and will not be conflated with the production distribution runtime.

---

## 2. Component Boundary: Upstream Debian vs. Sagar OS

A foundational rule of this repository is maintaining a crystal-clear distinction between what is inherited from Debian upstream and what is designed and authored by the Sagar OS team.

| Component Layer | Upstream Debian GNU/Linux 13 | Sagar OS Custom Engineering |
| :--- | :--- | :--- |
| **Kernel & Hardware Drivers** | Linux LTS Kernel, DRM/KMS, firmware | None (Upstream driver & kernel enablement) |
| **Base Userspace & Init** | `systemd`, `glibc`, `coreutils`, `util-linux` | Custom systemd unit presets, security profiles |
| **Package Management** | `apt`, `dpkg`, Debian official repos | Sagar OS package repositories & overlay channels |
| **Display & Compositor** | Wayland protocols, `mesa`, `seatd` / `libinput` | Sagar OS custom compositor & display shell |
| **Desktop & Session** | Base freedesktop specifications | Sagar OS Desktop Environment, notification & panel daemon |
| **System Services** | `NetworkManager`, `PipeWire`, `PAM` | Sagar OS identity daemon, unified settings service, telemetry-free analytics |
| **Core Applications** | Standard open-source utilities (optional) | Sagar OS suite of native, focused first-party apps |
| **Kernel Research (Future)** | N/A (Standard monolithic Linux) | Academic exploration, microkernel specs, IPC prototypes in `research/kernel/` |

---

## 3. Repository Structure

This repository is organized to maintain modularity, clean boundaries, and reproducibility:

```text
SagarOS/
├── AGENTS.md                  # Collaboration rules for AI assistants and contributors
├── ARCHITECTURE.md            # Comprehensive layered architectural specification
├── CONTRIBUTING.md            # Contribution workflow, code formatting, and review rules
├── DECISIONS.md               # Architectural Decision Records (ADR) index
├── LICENSE                    # Apache 2.0 license
├── MASTER_SPEC.md             # Master technical specification of Sagar OS
├── README.md                  # Project overview, boundaries, and introduction
├── ROADMAP.md                 # Phased engineering milestones and validation criteria
│
├── distro/                    # Distribution engineering, Debian manifests, and rootfs builders
│   ├── manifests/             # Package lists, bootstrap recipes, and seed profiles
│   └── overlays/              # Distribution filesystem overlays, configurations, and branding
│
├── docs/                      # Central project documentation
│   ├── adr/                   # Detailed Architectural Decision Records (ADR-0001+)
│   ├── architecture/          # Subsystem design documents and diagrams
│   ├── specs/                 # Subsystem technical specifications
│   └── standards/             # Documentation and engineering conventions
│
├── research/                  # Long-term academic and architectural exploration
│   └── kernel/                # Specifications, memory models, and prototypes for future kernel
│
├── src/                       # Custom Sagar OS software source code (staged for implementation)
│   ├── core/                  # Shared system libraries and foundation abstractions
│   ├── services/              # Custom daemons, session coordinators, and background services
│   ├── shell/                 # Wayland compositor, window manager, and desktop shell
│   └── apps/                  # First-party Sagar OS native user applications
│
└── tools/                     # Developer, build, and CI orchestration tools
    ├── build/                 # Rootfs builders, image creators, and ISO assembly scripts
    └── dev/                   # Linting, validation, test harnesses, and local tooling
```

---

## 4. Key Documentation Index

- **[Master Specification](MASTER_SPEC.md)**: Authoritative technical definition and functional goals of the operating system.
- **[Architecture Specification](ARCHITECTURE.md)**: Layered architectural diagram, subsystem interactions, and isolation guarantees.
- **[Roadmap](ROADMAP.md)**: Six-phase engineering trajectory from repository inception to kernel research.
- **[Architectural Decisions (ADRs)](DECISIONS.md)**: Historical log and rationale behind fundamental system decisions.
- **[Agent & Contributor Protocols](AGENTS.md)**: Mandatory guidelines for AI agents and human contributors.
- **[Contribution Guidelines](CONTRIBUTING.md)**: Git conventions, branch management, and review processes.
- **[Documentation Standards](docs/standards/DOCUMENTATION.md)**: Style guides, markdown format, and documentation maintenance rules.

---

## 5. Current Project Status

We are in **Phase 0: Repository Inception, Architectural Specification, and Governance**.
- **No executable code, drivers, or kernel implementations are present in this phase.**
- Focus is entirely on architectural integrity, specifications, build tooling design, and boundary definitions.
- For development milestones, see [ROADMAP.md](ROADMAP.md).
