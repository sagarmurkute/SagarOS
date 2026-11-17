# Sagar OS Architecture Documentation

This directory contains in-depth subsystem architectural blueprints, data flow diagrams, and design records.

## Core Documents
- Main Architecture Blueprint: [ARCHITECTURE.md](../../ARCHITECTURE.md)
- Subsystem designs will be documented here as development proceeds through each phase:
  - `display-stack.md`: Wayland compositor and rendering pipeline design.
  - `services-ipc.md`: System daemon IPC protocols and D-Bus interfaces.
  - `security-model.md`: Process sandboxing, Landlock, and namespace policies.
  - `storage-stateless.md`: Stateless root filesystem and state isolation design.
