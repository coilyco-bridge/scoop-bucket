# coilysiren/scoop-bucket

Scoop bucket for Windows binaries published from `coilysiren/*` repos. Sibling to [`coilysiren/homebrew-tap`](https://github.com/coilysiren/homebrew-tap) - same purpose, different OS.

## Install

```powershell
scoop bucket add coilysiren https://github.com/coilysiren/scoop-bucket
scoop install coily
```

## Update

```powershell
scoop update coily
```

## Manifests

- **`coily`** - [coilysiren/coily](https://github.com/coilysiren/coily). Operator CLI. Pulls prebuilt `coily-windows-<arch>.exe` from each release.

## How autoupdate works

Each manifest's `autoupdate` block points at `https://github.com/coilysiren/<repo>/releases/download/v$version/<asset>#/<rename>` and reads the SHA256 from the `.sha256` sidecar uploaded alongside the binary. `scoop bucket update` walks the bucket and bumps any manifest whose upstream `checkver` matches.

Upstream side of the contract:

- The producing repo's `release.yml` must attach `<asset>` and `<asset>.sha256` to the release.
- The release tag must be `v<semver>` (the same shape `mathieudutour/github-tag-action` already produces).

For `coily` that wiring lives at [`coilysiren/coily/.github/workflows/release.yml`](https://github.com/coilysiren/coily/blob/main/.github/workflows/release.yml) (windows-build job).

## See also

- [AGENTS.md](AGENTS.md) - agent-facing operating rules.
- [docs/FEATURES.md](docs/FEATURES.md) - inventory of what ships today.
- [.coily/coily.yaml](.coily/coily.yaml) - allowlisted commands.

Cross-reference convention from [coilysiren/agentic-os-kai#313](https://github.com/coilysiren/agentic-os-kai/issues/313).
