# Inter-Process Communication (IPC) Standards — Sagar OS

> **D-Bus namespace policies, interface versioning, naming conventions, error models, and Varlink standards for Sagar OS.**

---

## 1. Scope & Architectural Role

Inter-Process Communication (IPC) in Sagar OS coordinates interactions between unprivileged user sessions (`src/desktop/`, `src/apps/`) and system-level background services (`src/services/`).

Two primary IPC transports are established:
1. **D-Bus:** The standard message bus for desktop session coordination, system state broadcasts, and polkit-mediated privileged operations.
2. **Varlink:** Point-to-point, stateless JSON-over-socket IPC for high-throughput service-to-service communication.

---

## 2. Official D-Bus Namespace & Versioning

### 2.1 Namespace Hierarchy
All Sagar OS D-Bus services, objects, and interfaces must reside within the official reversed-domain hierarchy:
```text
org.sagaros.<Subsystem><Version>
```

### 2.2 Versioned Interface Names
Every D-Bus interface must append a numerical major version suffix directly to the subsystem name:
- `org.sagaros.Config1`: Unified Configuration Service interface, Version 1.
- `org.sagaros.Session1`: Session Management Service interface, Version 1.
- `org.sagaros.Power1`: Adaptive Power Management Service interface, Version 1.

### 2.3 Compatibility & Evolution Rules
- **Backwards Compatibility:** Within a major version (e.g., `Config1`), existing methods, signals, and argument signatures must remain backwards-compatible. New optional methods or signals may be added.
- **Breaking Changes:** If an interface method signature is removed or altered incompatibly, a new versioned interface must be introduced (e.g., `org.sagaros.Config2`). Both interfaces should be supported concurrently during transition periods where practical.

---

## 3. D-Bus Naming & Data Type Conventions

| Element | Convention | Example |
| :--- | :--- | :--- |
| **Well-Known Bus Name** | `org.sagaros.<Subsystem>` | `org.sagaros.Config`, `org.sagaros.Session` |
| **Object Paths** | `/org/sagaros/<Subsystem>` | `/org/sagaros/Config`, `/org/sagaros/Power` |
| **Interface Names** | `org.sagaros.<Subsystem><Version>` | `org.sagaros.Config1` |
| **Methods** | PascalCase (Verb + Noun) | `GetProperty()`, `ApplyConfiguration()` |
| **Signals** | PascalCase (Event descriptor) | `ConfigurationChanged`, `PowerStateChanged` |
| **Parameters & Arguments** | camelCase or snake_case | `configPath`, `newPowerState` |

---

## 4. Error Reporting Standards

All D-Bus error returns must use the standardized error namespace `org.sagaros.Error.*`:

```text
org.sagaros.Error.InvalidArgument
org.sagaros.Error.NotFound
org.sagaros.Error.PermissionDenied
org.sagaros.Error.ServiceUnavailable
org.sagaros.Error.Timeout
org.sagaros.Error.InternalError
```

Every error reply must include a human-readable description in plain language explaining why the operation failed.

---

## 5. Interface Introspection & Documentation

1. **XML Introspection Contracts:** Every published D-Bus interface must provide an authoritative XML introspection specification file stored in `docs/specs/` (e.g., `docs/specs/dbus/org.sagaros.Config1.xml`).
2. **Annotation:** Methods requiring administrative privileges must be clearly annotated in the introspection XML:
   ```xml
   <annotation name="org.freedesktop.DBus.GLib.Async" value="true"/>
   <annotation name="org.sagaros.Security.RequiresPolkit" value="org.sagaros.config.modify"/>
   ```

---

## 6. Varlink Protocol Standards

For point-to-point daemon communication:
1. **Interface URI:** Must use `org.sagaros.<subsystem>`.
2. **Schema Definition:** Must define strict Varlink interface files (`*.varlink`) specifying inputs, outputs, and errors.
3. **Payload Encoding:** Valid UTF-8 JSON strictly conforming to the interface schema.
