# openOODA/opm — OODA Package Manager

The OODA Package Manager (opm) is the tactical library for managing third-party OODA packages. It handles content-addressable storage, dependency resolution (pubgrub), lockfiles, cryptographic signing, and the E-M telemetry audit trail.

## Part of the openOODA ecosystem

This repo is one of six in the [openOODA](https://github.com/openOODA) polyrepo:

- [openOODA/openOODA](https://github.com/openOODA/openOODA) — governance, process boards, RFCs
- [openOODA/ooda](https://github.com/openOODA/ooda) — the compiler, runtime, standard library, LSP
- **openOODA/opm** — this repo, the OODA package manager library
- **openOODA/lsp** — the openOODA native LSP server
- [openOODA/.github](https://github.com/openOODA/.github) — shared GitHub meta
- [openOODA/openOODA.github.io](https://github.com/openOODA/openOODA.github.io) — website

## Quick start

```sh
# Build
ooda run ooda/opm/scripts/build.oo

# Test (runs the 8 break-test drivers)
ooda run ooda/opm/scripts/test.oo

# Verify VERSION + api_surface
ooda run ooda/opm/scripts/verify.oo

# Release (build + test + verify + tarball)
ooda run ooda/opm/scripts/release.oo
```

## Repo layout

```
opm/
  ANCHOR.oo          front door; Academy header + import registration
  VERSION            compat contract (opm version, ooda range, api_surface)
  core/              identity, name, recipe, pin
  resolve/           pubgrub, resolve, graph
  lock/              lockfile format
  store/             CAS, archive
  registry/          catalog, registry protocol, git ingest
  policy/            cap gates, yank, license
  sign/              HMAC, index
  launch/            pre-exec re-verify
  qa/                self-tests (8 break-test drivers)
  scripts/           build, test, verify, release
  docs/              per-package docs
  examples/          sample manifests, recipes, lockfiles
```

Every dir has an `ANCHOR.oo` at the top (per the openOODA tactical-subsystem template). The pattern is uniform across the project.

## Compatibility

`opm` requires `ooda >= 2.10.0`. See `VERSION` for the full contract. The `api_surface` field is a structural check: the loader asserts the mod.oo exposes exactly 9 public subdirs.

## License

Dual-licensed under Apache 2.0 or MIT, at your option. See `LICENSE`.
