# Agent Instructions for opm

You are operating within the openOODA polyrepo. The opm package is the
package manager for openOODA modules. It pulls packages from
`https://catalog.openooda.org` (or the local `seed/` mirror), verifies
the minisig, and lands the payload under the local install. Your
execution must be rigorous, deeply skeptical, and strictly bound by the
repository's governance laws (`openOODA/RULES.oot` and `openOODA/FLOOR.oot`).

## 1. Zero Trust & The Double-Run Law
- **Falsify, never confirm:** A test that always passes provides no proof.
  Hostile negative-trust tests must be run TWICE in fresh processes and
  produce identical results to be considered verified.
- **Resolve refuses extra caps.** The unique move here is `resolve` that
  refuses extra caps (ANCHOR.oo beat 9). Do not grow commands. If a
  capability you want isn't in the published 8 (`FsRead`, `FsWrite`,
  `Process`, `Env`), the answer is no.
- **The 4 stock packages** in `seed/` (echo, hello, caps, sqlite) are the
  only payloads opm install will land without an external catalog fetch.
  See `catalog.oot` for the full surface.

## 2. Services for Speed (No Shortcuts)
- **Do not blindly `grep` the tree.** Use the opm binary directly.
- **You MUST use the live subcommand surface (from `cli/main.oo`):**
  - `opm search` — list packages in the active catalog (seed or remote).
  - `opm add` — install a package by name; verifies `index.minisig` for
    HTTPS adds.
  - `opm remove` — uninstall a previously-added package.
  - `opm update` — refresh a package from its source.
  - `opm outdated` — list packages behind the latest.
  - `opm why` — explain why a package is in the dep graph.
  - `opm bot` — rebuild the local catalog index (CI calls this).
  - `opm pack` — bundle a package for distribution.
  - `opm publish` — push a package to a remote registry.
  - `opm regs` / `opm reg` / `opm registry` — list configured registries.
  - `opm audit` — verify installed packages against their manifests.
  - `opm sbom` — emit a software bill of materials.
  - `opm ingest` — pull a package into the local store.
  - `opm init` — scaffold a new project layout.
  - `opm launch` — run a package's binary.
  - `opm tree` — print the dependency tree.
  - `opm vendor` — copy a package's source into the local repo.
  - `opm clean` — drop the local store and re-fetch.

## 3. Strict Repository Compliance
- **Pure Files:** Only `.oo` and `.oot` files are permitted for logic
  (RULES.oot §1.14). No VERSION file. Version is the git tag (RFC-0006).
- **Line Limits:** Absolute maximum of 256 lines per file.
- **Academy Headers:** All `.oo` files must begin with the exact 4-element
  Academy header.
- **10 public subdirs:** `core/`, `resolve/`, `lock/`, `store/`, `registry/`,
  `policy/`, `sign/`, `launch/`, `qa/`, `cli/`. Plus `docs/`, `examples/`,
  `seed/` as non-public siblings. `std/` is a local compile pointer;
  `OODA_STD` is the contract.
- **api_surface=10.** Per ANCHOR.oo beat 8, do not add a 4th cmd beyond
  the 3 public ones already in `cli/`.

## 4. Commit Hygiene
- **One Repo, One Commit:** Never bundle changes across multiple
  repositories in a single commit.
- **Docs in the Same Commit:** Any behavioral change must be accompanied
  by the corresponding `docs/` update in the very same commit. Bump the
  tag when a subcommand is added.
- **Tag = VERSION:** This repo has no VERSION file. The tag IS the version
  (RFC-0006).
