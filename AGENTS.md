# AGENTS.md — Agent & Contributor Directives

> **Governing directives, guardrails, and operational protocols for AI agents and human contributors interacting with the Sagar OS repository.**

---

## 1. Core Principles & Truth Anchoring

All agents (automated assistants, code generators, and LLM-driven tools) working within this repository must adhere to the following mandatory principles:

### 1.1 Foundation Truth: Debian 13 Base
- The foundational base of Sagar OS is **Debian GNU/Linux 13 ("Trixie")**.
- The Linux kernel, `systemd`, `glibc`, and base userspace utilities currently originate from upstream Debian.
- **Never claim or fabricate that Sagar OS is already running on a custom independent kernel.**
- Long-term research for an independent kernel exists exclusively in `research/kernel/` and must always be labeled as experimental or theoretical.

### 1.2 Separation of Upstream and Custom Components
- Maintain a strict boundary between Debian upstream components and Sagar OS custom code.
- Custom code belongs under `src/` (e.g., `src/core/`, `src/libraries/`, `src/services/`, `src/graphics/`, `src/desktop/`, `src/apps/`).
- Distribution configurations, package lists, and bootstrap recipes belong under `distro/`.
- Research documentation belongs under `research/`.
- Do not place arbitrary, unstructured scripts in root or pollute upstream packaging namespaces.

### 1.3 Phased Execution & Scope Control
- Work strictly within the current phase defined in [ROADMAP.md](ROADMAP.md).
- **Do not generate application code, desktop implementations, kernel code, or drivers unless an active phase plan specifically authorizes and schedules it.**
- Do not attempt to install dependencies on the host operating system or modify the host system outside the target workspace.

---

## 2. Agent Operational Rules

### Rule 1: Read Before Editing
Always inspect existing documents, specifications, and records in `docs/` and `DECISIONS.md` before proposing changes. Never overwrite or contradict established Architectural Decision Records (ADRs) without explicit user instructions and an accompanying new ADR.

### Rule 2: Keep the Repository Clean & Modular
- Do not create scratch files or temporary build outputs in checked-in folders.
- Avoid large monolithic files. Break complex specifications into modular documents in `docs/` and link them from parent indices.
- Never commit binaries, ISO images, compiled objects (`.o`, `.so`, `.a`), or raw disk images into git.

### Rule 3: Architectural Decision Protocol
Whenever proposing a fundamental technical direction (e.g., choosing an IPC mechanism, selecting a graphics protocol, or defining a package distribution model):
1. Document the context, alternatives considered, decision, and consequences.
2. Record the entry in [DECISIONS.md](DECISIONS.md) and create the corresponding record under `docs/adr/`.
3. Align implementation with the recorded decision.

### Rule 4: Verification & Honesty
- Be rigorous in verifying build scripts and documentation.
- If a dependency, tool, or feature is incomplete, state clearly that it is a placeholder or work-in-progress.
- No dummy mockups presented as working implementations.

---

## 3. Directory Ownership Matrix

Agents should consult this table before creating or modifying files:

| Directory | Scope & Purpose | Agent Restrictions |
| :--- | :--- | :--- |
| `docs/` | Architectural specs, standards, ADRs | Update specs and decisions; follow documentation guidelines |
| `distro/` | Debian 13 manifests, rootfs configs, overlays | Only modify distribution recipes; never include compiled binaries |
| `src/core/` | Low-level Sagar OS foundational libraries | Strictly follow C17 and Rust standards in `docs/standards/` (when Phase 2 opens) |
| `src/libraries/` | Shared domain libraries, client SDKs | Follow modular C17/Rust standards in `docs/standards/` |
| `src/services/` | Custom daemons, session coordinators | System services with clear D-Bus/IPC contracts (`org.sagaros.*`) |
| `src/graphics/` | Wayland display server, compositor, protocols | Pure Wayland-native design only; follow `docs/standards/` |
| `src/desktop/` | Desktop shell components (panel, launcher, UI) | Modular UI design adhering to product specifications |
| `src/apps/` | First-party desktop applications | Modularity, sandboxed execution model |
| `tests/` | Automated unit, integration, security, VM tests | Adhere to testing guidelines in `docs/standards/TESTING.md` |
| `research/kernel/` | Future independent kernel research & specs | Speculative research only; explicitly distinct from the runtime |
| `tools/` | Image generation scripts, CI/CD, linters | Must be host-agnostic or clearly containerized (Bash 5.x / Python) |

---

## 4. Documentation Conventions for Agents

When generating or editing documentation:
1. Use standard Markdown conforming to GitHub Flavored Markdown (GFM).
2. Use Mermaid diagrams for architecture, sequence flows, and component relationships.
3. Ensure all intra-repository links are functional relative markdown links.
4. Keep headings hierarchical and logical (`#`, `##`, `###`).
5. Maintain a table of contents on extensive documents.
