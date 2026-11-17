# Independent Kernel Research (`research/kernel/`)

> **Exploration, Specifications, and Prototypes for a Future Independent Kernel.**

---

## 1. Status & Reality Declaration

> [!IMPORTANT]
> **Sagar OS currently runs on Debian GNU/Linux 13 ("Trixie") with the upstream Linux LTS kernel.**  
> **We do NOT have an active independent kernel in production.**  
> Everything in this directory represents theoretical research, architectural designs, memory models, and long-term prototypes planned for Phase 5 of our roadmap. We explicitly reject simulating or pretending an independent kernel is already functioning.

---

## 2. Research Goals & Motivation

The Linux kernel is a monolithic kernel exceeding 30 million lines of code. While it provides outstanding hardware support today, monolithic architectures present structural challenges:
- Any bug in a third-party device driver in Ring 0 compromises the entire system.
- Ambient Unix authority lacks fine-grained capability delegation.
- Large attack surfaces expose vulnerabilities to local privilege escalation.

Our long-term research investigates:
1. **Capability-Based Security:** Object capabilities where processes hold unforgeable tokens granting specific operations, eliminating ambient authority.
2. **Microkernel Architecture:** Minimizing the Ring 0 kernel to scheduling, memory address space management, and fast IPC.
3. **Memory Safety:** Prototyping kernel components in modern memory-safe languages (such as Rust) with formal verification of critical invariants.
4. **POSIX / Linux ABI Compatibility:** Developing an execution server or personality runtime to execute standard Sagar OS userspace binaries on top of the microkernel without code changes.

---

## 3. Directory Layout (Phase 5 Research)

```text
research/kernel/
├── spec/            # Capability model, syscall interface, and memory specifications
├── prototypes/      # Experimental proof-of-concept code and bootloaders
└── papers/          # Academic studies, IPC benchmark comparisons, and design notes
```

## 4. Verification & Criteria
Before any research prototype can be considered for integration into Sagar OS, it must pass strict verification:
- Microkernel round-trip IPC latency benchmarks under heavy contention.
- Formal proof of memory safety for page-table manipulation.
- High-throughput virtio-blk and virtio-net driver isolation.
