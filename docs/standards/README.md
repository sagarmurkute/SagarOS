# Sagar OS Engineering & Development Standards (`docs/standards/`)

> **Authoritative coding conventions, language standards, IPC protocols, security guardrails, and testing frameworks for Sagar OS.**

---

## 1. Overview

The documents in this directory govern how software, specifications, build tooling, and documentation are authored, verified, and maintained across the Sagar OS project. All human developers and automated AI contributors must adhere strictly to these normative standards.

---

## 2. Standards Navigation Hub

```text
docs/standards/
├── README.md               # Standards index, governance, and navigation hub (this file)
├── GENERAL.md              # Universal engineering tenets, naming, Git, and AI agent guardrails
├── C.md                    # ISO C17 standards, memory management, clang-format, and error handling
├── RUST.md                 # Rust 2021 standards, unsafe policies, clippy, and panic prevention
├── SHELL.md                # Bash 5.x standards, strict mode, shellcheck, shfmt, and POSIX portability
├── IPC-API.md              # D-Bus (org.sagaros.*) and Varlink schemas, versioning, and error models
├── TESTING.md              # Testing pyramid (unit, integration, security, VM) and quality verification
├── SECURITY.md             # Least privilege, compiler hardening, input sanitization, and sandboxing
└── DOCUMENTATION.md        # Technical documentation conventions, GFM, ADR formats, and Mermaid rules
```

---

## 3. Approved Languages & Tooling Summary

| Domain | Standard Language | Approved Tooling | Policy Reference |
| :--- | :--- | :--- | :--- |
| **Core Libraries & Low-Level** | **ISO C17** (`-std=c17`) | `clang-format`, `clang-tidy`, GCC/Clang warnings | [C.md](C.md) |
| **Memory-Safe Services & Shell** | **Rust 2021 Edition** | `rustfmt`, `clippy` (`-D warnings`), `cargo` | [RUST.md](RUST.md) |
| **Build & Tooling Automation** | **Bash 5.x** (`set -euo pipefail`) | `shfmt`, `shellcheck` | [SHELL.md](SHELL.md) |
| **Optional Developer Tools** | **Python 3** (Optional tooling only) | `ruff format`, `ruff check` | [SHELL.md](SHELL.md) |
| **IPC Bus & Transports** | **D-Bus (`org.sagaros.*`) & Varlink** | XML Introspection schemas, Varlink IDL | [IPC-API.md](IPC-API.md) |
| **Documentation & Specs** | **Markdown (GFM)** | `lychee` link checker, `editorconfig-checker` | [DOCUMENTATION.md](DOCUMENTATION.md) |

---

## 4. Relationship to Authoritative Architecture Documents

- **[AGENTS.md](../../AGENTS.md):** Mandatory agent directives, scope boundaries, and truth-anchoring rules.
- **[CONTRIBUTING.md](../../CONTRIBUTING.md):** Git workflow, branch management, Conventional Commits, and PR rules.
- **[MASTER_SPEC.md](../../MASTER_SPEC.md):** Authoritative system specifications, platform baselines, and Debian 13 upstream contracts.
- **[ARCHITECTURE.md](../../ARCHITECTURE.md):** Layered architectural blueprints and subsystem boundary specifications.
