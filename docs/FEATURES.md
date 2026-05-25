# Features

Baseline inventory of what `coilysiren/scoop-bucket` ships today. Update when a manifest is added, removed, or materially reshaped.

## Manifests

Bucket installed via `scoop bucket add coilysiren https://github.com/coilysiren/scoop-bucket`. Individual manifests installed with `scoop install coilysiren/<name>`.

- **[bucket/coily.json](../bucket/coily.json)** - tracks `coilysiren/coily` releases. Pulls the prebuilt `coily-windows-<arch>.exe` from each tag. Operator CLI for the homelab.

## Autoupdate

Each manifest's `autoupdate` block points at `https://github.com/coilysiren/<repo>/releases/download/v$version/<asset>#/<rename>` and reads the SHA256 from the `.sha256` sidecar uploaded alongside the binary. `scoop bucket update` walks the bucket and bumps any manifest whose upstream `checkver` matches.

Upstream-side contract:

- The producing repo's `release.yml` attaches `<asset>` and `<asset>.sha256` to the release.
- The release tag is `v<semver>`.

## See also

- [README.md](../README.md) - human-facing intro and install steps.
- [AGENTS.md](../AGENTS.md) - agent-facing operating rules.
- [.coily/coily.yaml](../.coily/coily.yaml) - allowlisted commands.

Cross-reference convention from [coilysiren/agentic-os-kai#313](https://github.com/coilysiren/agentic-os-kai/issues/313).
