# CONTRIBUTING.md — Sagar OS Contribution Guidelines

> **Thank you for your interest in contributing to Sagar OS.**  
> We welcome contributions from human developers, architects, and automated AI agents. To maintain architectural purity, code quality, and project integrity, please read and adhere to these guidelines.

---

## 1. Architectural Code of Conduct

1. **Respect Component Separation:** Do not blend custom code directly into upstream Debian packages or root folders. Custom code belongs strictly in `src/`. Upstream configurations and package profiles belong in `distro/`.
2. **Honesty & Transparency:** Do not fabricate or pretend that features exist if they are not yet implemented. In particular, custom kernel work is strictly future research quarantined in `research/kernel/`.
3. **Phase Discipline:** Contributions must align with the active phase in [ROADMAP.md](ROADMAP.md). We do not accept application or desktop code ahead of Phase 2/3.
4. **No Host Alterations:** Build scripts and tools must be isolated (chroot/containers/VMs). Under no circumstances should any script install global packages onto the contributor's or user's host OS.

---

## 2. Development Workflow

### 2.1 Branching Strategy
- `main`: Protected production branch. Every commit on `main` must represent a coherent, tested, and documented state.
- Feature branches: Use descriptive branch names with appropriate prefixes:
  - `feat/<short-description>`: New architectural features or tools.
  - `fix/<short-description>`: Bug fixes or corrections.
  - `docs/<short-description>`: Documentation additions or updates.
  - `research/<short-description>`: Research papers, microkernel specs.

### 2.2 Commit Message Standard (Conventional Commits)
All commit messages must follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```text
<type>(<scope>): <short description in imperative mood>

[optional body explaining context, rationale, and consequences]

[optional footer, e.g., Closes #12, References ADR-0002]
```

**Allowed types:**
- `feat`: A new feature or capability.
- `fix`: A bug fix.
- `docs`: Documentation changes only.
- `spec`: Architectural or technical specification changes.
- `refactor`: Code or file restructuring without functional changes.
- `test`: Adding or correcting tests.
- `chore`: Repository maintenance, tooling, or CI updates.

**Examples:**
- `docs(adr): record ADR-0001 for debian 13 foundation`
- `spec(security): define landlock sandboxing criteria`
- `chore(repo): initialize base folder layout`

---

## 3. Pull Request Guidelines

1. **Keep Pull Requests Focused:** An individual PR should solve one problem or introduce one coherent specification/feature. Avoid multi-megabyte grab-bag PRs.
2. **Documentation Accompaniment:** Any architectural change or new subsystem must be accompanied by relevant documentation in `docs/` and, if applicable, an entry in `DECISIONS.md`.
3. **No Unversioned Artifacts:** Ensure binaries, ISOs, `.o`, `.so`, temporary files, and log files are excluded via `.gitignore`.
4. **Testing & Verification:** Provide instructions on how changes were verified (e.g., Markdown linting, QEMU boot test, shell syntax check).

---

## 4. Documentation Conventions

Please review [docs/standards/DOCUMENTATION.md](docs/standards/DOCUMENTATION.md) for full formatting rules, markdown conventions, and Mermaid diagram requirements.
