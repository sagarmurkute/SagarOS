# General Development Standards & Universal Principles — Sagar OS

> **Universal engineering tenets, naming conventions, code hygiene, Git integration, and AI contribution guardrails for Sagar OS.**

---

## 1. Universal Engineering Tenets

All software components developed for Sagar OS—regardless of programming language or subsystem—must adhere to these universal engineering tenets:

1. **Clarity and Predictability Over Cleverness:** Code must be straightforward, maintainable, and self-documenting. Avoid obscure language features, undocumented macros, or convoluted one-liners.
2. **Defensive Design:** Assume external inputs, files, environment variables, and IPC messages may be malformed or hostile. Validate at system boundaries.
3. **Explicit Failure Handling:** Silent failures, ignored return codes, and unchecked memory allocations are strictly prohibited. Fail early, clean up allocated resources, and return meaningful errors.
4. **Minimal Dependencies:** Avoid external library dependencies unless there is a compelling technical justification approved by an Architectural Decision Record (ADR).
5. **Phase Discipline:** Implementation code must align with the active phase in [ROADMAP.md](../../ROADMAP.md). Never introduce premature components ahead of scheduled milestones.

---

## 2. Global Naming & Identifier Conventions

Unless superseded by a language-specific standard (e.g., Rust idioms in [RUST.md](RUST.md)), the following global conventions apply:

| Scope | Convention | Example |
| :--- | :--- | :--- |
| **Files & Directories** | Lowercase kebab-case or snake_case; no spaces | `session-manager.c`, `sagar_config.h` |
| **Types & Structs** | PascalCase or `sagar_<name>_t` | `SagarSession`, `sagar_config_t` |
| **Functions & Methods** | snake_case with namespace prefix | `sagar_config_load()`, `sagar_session_get_id()` |
| **Variables & Fields** | Lowercase snake_case | `buffer_size`, `display_count` |
| **Constants & Macros** | SCREAMING_SNAKE_CASE with namespace prefix | `SAGAR_MAX_DISPLAYS`, `SAGAR_OK` |
| **IPC Interfaces** | Reversed-domain PascalCase with version | `org.sagaros.Config1` |

---

## 3. Formatting & Code Hygiene

Global formatting standards are anchored in [`.editorconfig`](../../.editorconfig) at the root of the repository:

- **Character Encoding:** UTF-8 strictly without Byte Order Mark (BOM).
- **Line Endings:** UNIX-style `LF` (`\n`). `CRLF` is strictly banned.
- **Indentation:** 
  - Source code (C, Rust, Shell): 4 spaces per indent level. No tab characters (except in `Makefile` recipes).
  - Documentation (`*.md`) & manifests (`*.json`, `*.yaml`): 2 spaces per indent level.
- **Line Length:** Soft limit of 100 characters; hard limit of 120 characters where readability is preserved.
- **Whitespace Hygiene:** Trailing whitespace must be trimmed; all files must terminate with a single trailing newline.

---

## 4. Code Commenting & Documentation

- **Explain Why, Not What:** Comments must explain architectural intent, invariants, non-obvious algorithms, and safety constraints. Do not restate what the code trivially does.
- **Public API Documentation:** Every exported function, public struct, and interface method must have structured documentation comments:
  - Purpose of the function.
  - Parameter definitions and constraints (`[in]`, `[out]`).
  - Return values and error conditions.
  - Ownership semantics of returned pointers or memory.
- **TODO and FIXME Markers:** Must include context and reference an issue or roadmap phase:
  ```c
  /* TODO(phase2): Implement atomic reload via org.sagaros.Config1 */
  ```

---

## 5. Code Review & Pull Request Guidelines

1. **Focused Scope:** Each Pull Request (PR) must address a single coherent feature, fix, or specification. Grab-bag PRs spanning unrelated subsystems will be rejected.
2. **Conventional Commits:** PR titles and commit messages must strictly comply with the Conventional Commits specification mandated in [CONTRIBUTING.md](../../CONTRIBUTING.md):
   ```text
   <type>(<scope>): <lowercase subject description>
   ```
   Allowed types: `feat`, `fix`, `docs`, `spec`, `refactor`, `test`, `chore`.
3. **Automated CI Validation:** PRs must pass all continuous integration checks:
   - Markdown and link validation (`docs-validation.yml`).
   - Semantic PR title linting (`pr-lint.yml`).
   - Language-specific linters and formatters as established in [C.md](C.md), [RUST.md](RUST.md), and [SHELL.md](SHELL.md).
4. **Documentation Accompanying Code:** Any new capability, IPC schema change, or architectural direction must be accompanied by updated documentation and ADR records where applicable.

---

## 6. AI Contributor & Automated Agent Guardrails

AI assistants and code generators working in this repository must operate under the directives codified in [AGENTS.md](../../AGENTS.md):

- **Truth Anchoring:** Never claim or simulate that Sagar OS runs on a custom independent kernel. The active platform foundation is Debian GNU/Linux 13 ("Trixie").
- **No Mockups Presented as Functional:** Never author dummy mockups, stub implementations, or simulated tests presented as functional implementations.
- **Zero Host Tampering:** Never execute commands that install packages or alter files on the host operating system outside the isolated project workspace or containerized build harness.
- **Respect Phase Boundaries:** Do not generate application code, desktop shell implementations, drivers, or kernel code unless an active phase plan specifically authorizes and schedules it.
