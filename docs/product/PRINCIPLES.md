# Product Principles — Sagar OS

> **The immutable design, engineering, and user experience tenets that guide every product decision in Sagar OS.**

---

## 1. Predictability Over Novelty

- Systems should behave consistently across reboots, upgrades, and configuration changes.
- Novel UI gimmicks are rejected if they introduce latency, unpredictable window behavior, or cognitive load.
- Hardware state (sleep, lid-close, external displays, audio switching) must work deterministically every single time.

---

## 2. Distraction-Free Focus

- The operating system exists to serve the user's workflow, not to demand attention.
- Notifications are non-modal, quiet by default, and strictly adhere to "Do Not Disturb" focus modes.
- Visual styling is restrained, cohesive, and typography-driven, eliminating visual noise.

---

## 3. Truth Anchoring & Radical Honesty

- **No False Claims:** We clearly state that Sagar OS runs on Debian GNU/Linux 13 today. We never pretend an independent custom kernel is active until it has passed all Phase 5 exit criteria.
- **Clear System State:** When an operation fails (network drop, package conflict, permission denial), the OS presents clear, actionable diagnostics rather than vague error codes or endless loading spinners.

---

## 4. Privacy & Complete User Ownership

- **Zero Telemetry:** No user metrics, crash dumps, or usage analytics are collected or transmitted over the network without explicit, opt-in user request.
- **Local-First Identity:** The user account is fully local, encrypted, and does not require third-party cloud authentication.
- **Default-Drop Firewall:** Unsolicited incoming network connections are blocked by default.

---

## 5. Security by Default & Principle of Least Privilege

- Applications do not receive unconstrained access to the user's home directory or hardware devices.
- Unprivileged user sessions are strictly isolated from system-level hardware daemons via D-Bus and polkit.
- First-party and third-party applications execute under Landlock LSM and seccomp-bpf sandboxing boundaries.

---

## 6. Stateless Reliability & Factory Resilience

- System configurations are divided into vendor defaults (`/usr/lib/sagar/`) and user overrides (`/etc/`, `~/.config/`).
- Deleting or misconfiguring local configuration files must never brick the operating system; the system will boot cleanly back to factory defaults.
- Updates must be transactional, auditable, and easily roll-backable.
