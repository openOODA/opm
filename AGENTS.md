# opm: Agent Engineering Standards (v1)

This repository houses the cryptographic package manager for openOODA.
All work in this repository strictly defers to the organization standards in [`openOODA/AGENTS.md`](file:///home/ubermetroid/Projects/openOODA/openOODA/AGENTS.md).

---

## 1. Package Manager Architecture & Invariants
- **Reproducible Resolution**: Validates `ooda.pkg` manifests and lockfiles deterministically.
- **Cryptographic Signatures**: Minisign and SHA-256 integrity verification ahead of extraction.
- **Capability Auditing**: Statically checks and declares capability requirements before dependency compilation.

---

## 2. Invariants & Quality Standards
- **The Page Rule**: Every `.oo` page must be between 16 and 256 lines.
- **Directory Density**: At most 8 `.oo` pages per directory.
- **4-Element Academy Header**: Mandatory on every `.oo` page.
- **Double-Run Determinism**: All `qa/*.oo` verification probes must pass in sequential fresh processes.

---

## 3. Local Verification Commands
```bash
cli build cli/main.oo -o dist/opm
cli qa
```
