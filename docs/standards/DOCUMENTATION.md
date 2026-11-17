# DOCUMENTATION.md — Sagar OS Documentation Standards

> **Conventions, Structure, and Formatting Rules for Sagar OS Technical Documentation.**

---

## 1. Documentation Philosophy

Documentation in Sagar OS is treated as a first-class engineering artifact. Clear, accurate, and structured documentation is essential for:
- Maintaining architectural integrity over years of development.
- Enabling seamless collaboration between human contributors and AI agents.
- Ensuring that design decisions are reasoned, recorded, and verifiable.

---

## 2. Document Hierarchy & Locations

All documentation is stored in the `docs/` tree or the project root:

| Location | Content Type | Audience |
| :--- | :--- | :--- |
| `README.md` | Project elevator pitch, overview, high-level matrix | Public, all contributors |
| `AGENTS.md` | Agent operating rules and guardrails | AI models, contributors |
| `MASTER_SPEC.md` | Authoritative system specifications | Architects, engineers |
| `ARCHITECTURE.md` | High-level layered architecture & blueprints | System designers, engineers |
| `ROADMAP.md` | Phased development plan and exit criteria | Project managers, contributors |
| `DECISIONS.md` | Index of Architectural Decision Records | All engineers |
| `docs/adr/` | Individual ADR markdown documents (`0001-*.md`) | Systems architects |
| `docs/architecture/` | Deep-dive architectural blueprints for subsystems | Subsystem owners |
| `docs/specs/` | Granular subsystem technical specifications | Implementers |
| `docs/standards/` | Engineering standards, coding style, doc conventions | All contributors |

---

## 3. Formatting & Markdown Rules

### 3.1 Standard Markdown & GFM
- Use standard GitHub Flavored Markdown (GFM).
- Ensure consistent line endings (`LF`).
- Use two spaces for list indents or block indentation.
- Always include an empty line before and after lists, code blocks, and blockquotes.

### 3.2 File and Line Links
- Use relative markdown links for intra-repository references (e.g., `[MASTER_SPEC.md](../../MASTER_SPEC.md)`).
- When linking to source files, use readable basenames rather than full paths.

### 3.3 Mermaid Diagrams
- Use Mermaid diagrams to visualize architecture, sequence flows, and state machines.
- Supported diagram types:
  - `flowchart TD` / `flowchart LR`
  - `sequenceDiagram`
  - `stateDiagram-v2`
- Always quote labels containing special characters, brackets, or parentheses (e.g., `id["Label (Info)"]`).

### 3.4 Alerts & Callouts
Use standard GitHub-style alerts sparingly for critical notes:
```markdown
> [!NOTE]
> Relevant context or explanation.

> [!WARNING]
> Important hazard or constraint.
```

---

## 4. Architectural Decision Record (ADR) Standard

Every ADR must follow this standardized template:

```markdown
# ADR-XXXX: Title of Decision

- **Status:** Proposed | Accepted | Deprecated | Superseded
- **Date:** YYYY-MM-DD
- **Authors:** Name / Agent

## Context
What is the problem or technical challenge being addressed?

## Decision
What is the specific architectural decision taken?

## Alternatives Considered
- Option A: Why it was rejected.
- Option B: Why it was rejected.

## Consequences
### Positive
- Advantage 1
- Advantage 2

### Negative / Trade-offs
- Trade-off 1
- Trade-off 2
```
