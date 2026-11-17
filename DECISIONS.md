# DECISIONS.md — Architectural Decision Log

> **Index of Architectural Decision Records (ADRs) governing the design, engineering, and lifecycle of Sagar OS.**

---

## What is an Architectural Decision Record (ADR)?

An Architectural Decision Record (ADR) is a lightweight document capturing an important architectural decision made along with its context, considered alternatives, and consequences.

All formal ADRs reside in the [`docs/adr/`](docs/adr/) directory and follow the format specified in [docs/standards/DOCUMENTATION.md](docs/standards/DOCUMENTATION.md).

---

## Decision Log Index

| ID | Title | Status | Date | Summary | Full Document |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ADR-0001** | Adoption of Debian GNU/Linux 13 (Trixie) as Base | **Accepted** | 2026-11-17 | Establish Debian 13 as the rock-solid upstream foundation for userspace, kernel, and driver enablement. | [0001-debian-13-foundation.md](docs/adr/0001-debian-13-foundation.md) |
| **ADR-0002** | Strict Separation of Custom and Upstream Components | **Accepted** | 2026-11-17 | Enforce strict boundaries between Debian upstream packages and custom Sagar OS code to preserve maintainability. | [0002-upstream-separation.md](docs/adr/0002-upstream-separation.md) |
| **ADR-0003** | Independent Kernel Research Strategy | **Accepted** | 2026-11-17 | Isolate future microkernel research to `research/kernel/` without claiming active implementation. | [0003-independent-kernel-research.md](docs/adr/0003-independent-kernel-research.md) |
| **ADR-0004** | Wayland-Native Display & Compositor Stack | **Accepted** | 2026-11-17 | Adopt Wayland as the exclusive display protocol; reject legacy X11 monolithic display server design. | [0004-wayland-display-stack.md](docs/adr/0004-wayland-display-stack.md) |
| **ADR-0005** | Documentation Standards & AI Agent Protocols | **Accepted** | 2026-11-17 | Mandate rigorous documentation standards and enforce guardrails for autonomous AI agent contributions. | [0005-documentation-and-agent-protocols.md](docs/adr/0005-documentation-and-agent-protocols.md) |

---

## How to Propose a New Decision

1. Copy the template from [docs/adr/README.md](docs/adr/README.md).
2. Assign the next sequential number (e.g., `0006-<slug>.md`).
3. Set status to `Proposed` and open a discussion or pull request.
4. Once consensus is reached, update status to `Accepted` and link the ADR in this index.
