# Shell Scripting & Tooling Standards — Sagar OS

> **Scripting conventions, shell interpreter policies, formatting, linting, and defensive programming standards for Sagar OS.**

---

## 1. Scope & Interpreter Policy

Shell scripts in Sagar OS are restricted primarily to build orchestration (`tools/build/`), developer test utilities (`tools/dev/`), packaging hooks (`distro/`), and continuous integration automation.

### 1.1 Default Interpreter: Bash 5.x
- **Standard Shebang:** All Bash scripts must start with:
  ```bash
  #!/usr/bin/env bash
  ```
- **Strict Execution Mode:** Every Bash script must declare strict mode immediately following the shebang:
  ```bash
  set -euo pipefail
  ```
  - `-e`: Exit immediately if any command exits with a non-zero status.
  - `-u`: Treat unset variables as an error and exit immediately.
  - `-o pipefail`: Return value of a pipeline is the status of the last command to exit with a non-zero status.

### 1.2 POSIX `/bin/sh` Portability Policy
- Where required for minimal Debian packaging hooks (`debian/postinst`, `debian/rules`) or early initramfs boot environments, standard POSIX `/bin/sh` is permitted.
- In `/bin/sh` scripts:
  - Shebang must be `#!/bin/sh`.
  - Use `set -eu` (the `-o pipefail` option is a non-POSIX bashism).
  - Banned in `/bin/sh`: arrays, `[[ ... ]]` test expressions, `local` variable declarations (unless supported by target dash/POSIX shell), and Bash-specific string manipulations.

---

## 2. Formatting & Tooling

### 2.1 Automated Formatting (`shfmt`)
All shell scripts must format cleanly using `shfmt`:
- **Indentation:** 4 spaces per indent level (`shfmt -i 4`).
- **Binary Operators:** Place binary operators at the beginning of the next line.
- **Case Indentation:** Indent case statement patterns.

### 2.2 Static Analysis (`shellcheck`)
All shell scripts must pass `shellcheck` in CI with zero warnings:
```bash
shellcheck -x tools/build/*.sh tools/dev/*.sh
```
If a specific warning must be suppressed due to external environment constraints, document the justification with an inline directive:
```bash
# shellcheck disable=SC1091 -- environment file is generated dynamically
source "${BUILD_ENV_FILE}"
```

---

## 3. Defensive Programming Guidelines

1. **Quote All Variable Expansions:** Always quote variables to prevent word splitting and globbing hazards:
   ```bash
   # Correct
   rm -rf "${target_directory:?}/tmp"

   # FORBIDDEN (can cause catastrophic data loss if variable is unset)
   rm -rf $target_directory/tmp
   ```
2. **Safe Temporary Files & Cleanup Traps:** Always generate temporary scratch areas using `mktemp -d` and guarantee their removal upon exit via an explicit signal `trap`:
   ```bash
   scratch_dir="$(mktemp -d)"
   trap 'rm -rf "${scratch_dir}"' EXIT INT TERM
   ```
3. **Explicit Command Checking:** Verify that external dependencies exist before attempting to invoke them:
   ```bash
   command -v mmdebstrap >/dev/null 2>&1 || {
       echo "Error: mmdebstrap is required but not installed." >&2
       exit 1
   }
   ```
4. **Environment Isolation:** Build scripts must never execute commands that alter the host system outside the target build directory or chroot environment.

---

## 4. Policy on Python Tooling

- **Scope:** Python 3 is approved **strictly for optional developer tools, test harnesses, and documentation verification** in `tools/dev/`.
- **Core Restriction:** Python is **not approved** for core operating system daemons, foundation libraries, or desktop shell components.
- **Tooling Standards:** When Python scripts are introduced in developer tooling:
  - Formatted using `ruff format`.
  - Linted using `ruff check --fix`.
  - Must include type annotations (`typing` module) for all public functions.
