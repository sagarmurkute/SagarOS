# C Development Standards — Sagar OS

> **Coding conventions, language version, memory management, formatting, and safety standards for C in Sagar OS.**

---

## 1. Scope & Standard Version

C is the foundational systems programming language for Sagar OS core foundation libraries (`src/core/`), low-level utilities, and standard POSIX runtime interfaces.

- **Approved Language Standard:** **ISO C17** (`-std=c17` or `-std=gnu17` where POSIX/Linux extensions are required).
- **Target Compiler Baseline:** GCC 13+ / Clang 16+ as supplied by **Debian GNU/Linux 13 ("Trixie")**.
- **Standard Library:** Upstream GNU C Library (`glibc`).

---

## 2. Formatting & Tooling

### 2.1 Automated Formatting (`clang-format`)
All C source (`*.c`) and header (`*.h`) files must format cleanly using `clang-format`. The authoritative style parameters:
- **Indent Width:** 4 spaces.
- **Tabs:** Never use tab characters for indentation.
- **Brace Style:** Allman style or K&R style with 1TBS (one true brace style) for functions and control blocks. Braces are mandatory for all control blocks, even single-line `if`/`for`/`while` statements:
  ```c
  /* Correct */
  if (condition) {
      handle_success();
  } else {
      handle_failure();
  }

  /* FORBIDDEN */
  if (condition) handle_success();
  ```
- **Column Limit:** 100 characters soft limit, 120 characters hard limit.
- **Pointer Alignment:** Left-aligned or right-aligned consistently across libraries (standardized as `type *ptr`).

### 2.2 Compiler Warnings & Quality Gates
C code must compile cleanly with zero warnings under standard development flags:
```text
-Wall -Wextra -Wpedantic -Werror -Wformat=2 -Wconversion -Wshadow -Wundef
```
Static analysis with `clang-tidy` must be run as part of the integration test harness.

---

## 3. Header Files & File Organization

### 3.1 Header Guards
All header files must use unique, fully qualified preprocessor include guards based on the file's repository path:
```c
#ifndef SAGAR_CORE_CONFIG_H
#define SAGAR_CORE_CONFIG_H

/* Declarations */

#endif /* SAGAR_CORE_CONFIG_H */
```

### 3.2 Include Ordering
Include statements must be grouped logically with an empty line separating each group:
1. Associated primary header (e.g., `sagar_config.h` in `sagar_config.c`).
2. System / C standard library headers (`<stdio.h>`, `<stdlib.h>`, `<stdint.h>`).
3. POSIX and Linux platform headers (`<unistd.h>`, `<sys/types.h>`).
4. External library headers (`<systemd/sd-bus.h>`).
5. Sagar OS internal project headers (`"sagar_core.h"`, `"sagar_log.h"`).

### 3.3 Encapsulation & Opaque Pointers
Public headers must expose opaque struct pointers where internal state should be hidden from external consumers:
```c
/* Public header: sagar_session.h */
typedef struct sagar_session sagar_session_t;

sagar_session_t *sagar_session_create(const char *user);
void sagar_session_destroy(sagar_session_t *session);
```

---

## 4. Naming Conventions

All public symbols in C must carry the project namespace prefix `sagar_` to prevent collision with third-party libraries or POSIX namespaces:

| Element | Format | Example |
| :--- | :--- | :--- |
| **Types & Typedefs** | `sagar_<module>_<name>_t` | `sagar_config_t`, `sagar_result_t` |
| **Public Functions** | `sagar_<module>_<action>()` | `sagar_config_load()`, `sagar_log_info()` |
| **Static Functions** | `<action>_<noun>()` or `sagar_<module>_<action>()` | `parse_line()`, `sagar_config_parse()` |
| **Constants & Enums** | `SAGAR_<MODULE>_<NAME>` | `SAGAR_CONFIG_MAX_PATH`, `SAGAR_OK` |
| **Macros** | `SAGAR_<NAME>()` | `SAGAR_ARRAY_SIZE(arr)` |

---

## 5. Memory Management & Safety

1. **Explicit Allocation Checking:** Every memory allocation (`malloc`, `calloc`, `realloc`) must be checked immediately for `NULL`:
   ```c
   char *buffer = malloc(size);
   if (buffer == NULL) {
       return SAGAR_ERROR_OUT_OF_MEMORY;
   }
   ```
2. **Clear Ownership Semantics:** Functions that allocate memory returned to the caller must document transfer of ownership explicitly. Pair every `_create()` / `_alloc()` function with a corresponding `_destroy()` / `_free()` function.
3. **Buffer Safety:** Never use unbounded string functions (`strcpy`, `strcat`, `sprintf`, `gets`). Always use bounded alternatives (`snprintf`, `strlcpy` or explicit bounds validation).
4. **Cleanup Patterns:** Use standardized cleanup patterns or GCC/Clang cleanup attributes (`__attribute__((cleanup(sagar_free_wrapper)))`) to guarantee resources (file descriptors, allocated buffers) are freed along error return paths.
5. **Zeroing Sensitive Memory:** Buffers containing sensitive data (passwords, encryption keys) must be cleared using `explicit_bzero()` or `memset_s()` prior to deallocation.

---

## 6. Error Handling Strategy

1. **Return Codes:** Functions must return an integer status code (`sagar_result_t` or standard `int` where `0` indicates success and negative values indicate errors):
   ```c
   typedef enum sagar_result {
       SAGAR_OK                   =  0,
       SAGAR_ERROR_GENERIC        = -1,
       SAGAR_ERROR_INVALID_ARGS   = -2,
       SAGAR_ERROR_OUT_OF_MEMORY  = -3,
       SAGAR_ERROR_NOT_FOUND      = -4,
       SAGAR_ERROR_ACCESS_DENIED  = -5,
   } sagar_result_t;
   ```
2. **Output Parameters:** When a function returns a computed value or allocated object, pass it via an output pointer:
   ```c
   sagar_result_t sagar_config_get_int(const sagar_config_t *config, const char *key, int *out_val);
   ```
3. **No Unchecked Errors:** Callers must inspect and handle error returns. Discarding error codes without handling requires an explicit cast to `(void)`.
