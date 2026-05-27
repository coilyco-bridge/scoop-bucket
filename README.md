# coilysiren/scoop-bucket

Scoop bucket for Windows binaries published from `coilysiren/*` repos. Sibling to [`coilysiren/homebrew-tap`](https://github.com/coilysiren/homebrew-tap) - same purpose, different OS.

## Install

```powershell
scoop bucket add coilysiren https://forgejo.coilysiren.me/coilysiren/scoop-bucket
scoop install coily
```

## Update

```powershell
scoop update coily
```

## Manifests

- **`coily`** - [coilysiren/coily](https://forgejo.coilysiren.me/coilysiren/coily). Operator CLI. Pulls prebuilt `coily-windows-<arch>.exe` from each Forgejo release. Both the bucket and the binaries it points at are hosted on Forgejo (coily releases moved there in coily#80).

## How autoupdate works

Each manifest's `autoupdate` block points at `https://forgejo.coilysiren.me/coilysiren/<repo>/releases/download/v$version/<asset>#/<rename>` and reads the SHA256 from the `.sha256` sidecar uploaded alongside the binary. `scoop bucket update` walks the bucket and bumps any manifest whose upstream `checkver` matches the Forgejo `releases.atom` feed.

Upstream side of the contract:

- The producing repo's `.forgejo/workflows/release.yml` must attach `<asset>` and `<asset>.sha256` to the release.
- The release tag must be `v<semver>`.

For `coily` that wiring lives at [`coilysiren/coily/.forgejo/workflows/release.yml`](https://forgejo.coilysiren.me/coilysiren/coily/src/branch/main/.forgejo/workflows/release.yml) (`windows-assets` job).

## See also

- [AGENTS.md](AGENTS.md) - agent-facing operating rules.
- [docs/FEATURES.md](docs/FEATURES.md) - inventory of what ships today.
- [.coily/coily.yaml](.coily/coily.yaml) - allowlisted commands.

Cross-reference convention from [coilysiren/agentic-os-kai#313](https://github.com/coilysiren/agentic-os-kai/issues/313).
