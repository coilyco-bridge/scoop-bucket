# Features

Baseline inventory of what `coilysiren/scoop-bucket` ships today. Update when a manifest is added, removed, or materially reshaped.

## Manifests

Bucket installed via `scoop bucket add coilysiren https://github.com/coilyco-bridge/scoop-bucket`. Individual manifests installed with `scoop install coilysiren/<name>`.

- **[bucket/repo-recall.json](../bucket/repo-recall.json)** - tracks `coilysiren/repo-recall` Forgejo releases. Pulls `repo-recall-windows-amd64.exe`, then `post_install` registers a per-user `AtLogOn` scheduled task that runs the binary in Kai's session on `127.0.0.1:7887` (default 7777 left free for WSL). `pre_uninstall` unregisters it. No admin or password (per-user task, not a Windows service).

## Autoupdate

Each manifest's `autoupdate` block points at `https://github.com/coilysiren/<repo>/releases/download/v$version/<asset>#/<rename>` and reads the SHA256 from the `.sha256` sidecar uploaded alongside the binary. `scoop bucket update` walks the bucket and bumps any manifest whose upstream `checkver` matches.

Upstream-side contract:

- The producing repo's `release.yml` attaches `<asset>` and `<asset>.sha256` to the release.
- The release tag is `v<semver>`.

## See also

- [README.md](../README.md) - human-facing intro and install steps.
- [AGENTS.md](../AGENTS.md) - agent-facing operating rules.
- [.coily/coily.yaml](../.coily/coily.yaml) - allowlisted commands.

Cross-reference convention from [coilysiren/agentic-os-kai#313](https://github.com/coilyco-bridge/agentic-os-kai/issues/313).
