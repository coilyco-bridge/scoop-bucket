# Agent instructions for `coilysiren/scoop-bucket`

Orientation for fresh Claude / mobile sessions. Keep this short.

## Scope

The Scoop bucket for `coilysiren/*` tools on Windows. Sibling to [`coilysiren/homebrew-tap`](https://github.com/coilysiren/homebrew-tap). Each `bucket/*.json` manifest points at a release asset published from its upstream repo.

## Project shape

- `bucket/*.json` - Scoop manifests, one per published tool.
- `README.md` - install steps and the upstream-side contract for autoupdate.

## Repo boundaries

This repo only hosts manifests. Source code for each tool lives in its own `coilysiren/*` repo. Releases are produced upstream and consumed here.

## Commands

Route every dev command through coily, which reads [`.coily/coily.yaml`](.coily/coily.yaml). No local dev verbs today.

## Validation

Pre-commit suite shipped from `coilysiren/agentic-os` enforces catalog and documentation discipline. Run with `pre-commit run --all-files`.

## Safety

- Do not hand-edit `version` or `hash` to race the release pipeline.
- Do not bypass commit hooks (`--no-verify`).
- Privileged ops route through `coily ops gh` etc., never bare `gh` / `aws` / `kubectl`.

## Cross-repo contracts

The producing repo's `release.yml` must attach `<asset>` and `<asset>.sha256` to the release. The release tag must be `v<semver>`. Without those, `scoop update` cannot bump the manifest.

## Release

Upstream repos cut a tag. `scoop update` reads the manifest's `autoupdate` block, fetches the sidecar, and bumps `version` + `hash`. Waiting and verification discipline for the release pipeline lives in the `kai-brew-release` skill.

## Agent rules

Commit to `main`, push after each commit. Every commit closes a same-repo issue with `closes #N`. The commit-msg hook enforces this. Full operating context for Kai lives in `coilysiren/agentic-os-kai/AGENTS.md`.

## See also

- [README.md](README.md) - human-facing intro.
- [docs/FEATURES.md](docs/FEATURES.md) - inventory of what ships today.
- [.coily/coily.yaml](.coily/coily.yaml) - allowlisted commands.

Cross-reference convention from [coilysiren/agentic-os-kai#313](https://github.com/coilysiren/agentic-os-kai/issues/313).
