---
title: Dependency update maintenance
docType: reference
scope: repo
status: active
authoritative: true
owner: tidas-spec
language: en
whenToUse:
  - when reviewing a Dependabot proposal or changing its configuration
whenToUpdate:
  - when dependency monitoring scope or its maintenance procedure changes
checkPaths:
  - .github/dependabot.yml
  - _docs/reference/dependency-updates.md
lastReviewedAt: 2026-10-16
lastReviewedCommit: 2fcf1c94f019e4ad7f2cfdccc57d817bbdc6cca4
lastReviewedNote: "Reviewed for #44: bounded development-dependency and Actions monitoring uses existing candidate validation and preserves the asset-only publication contract."
---

Dependabot monitors the root development dependency graph and GitHub Actions.
The schedule, release cooldown, proposal limits and groups are defined in
[the configuration](../../.github/dependabot.yml). npm major updates remain
eligible as separate proposals. There is no automatic merge configuration.

The shared workspace policy is maintained in
[`_docs/workspace-dependency-update-policy.md`](https://github.com/tiangong-lca/workspace/blob/main/_docs/workspace-dependency-update-policy.md),
tracked by [workspace #1894](https://github.com/tiangong-lca/workspace/issues/1894).
Repository changes follow the controller and review requirements in
[AGENTS.md](../../AGENTS.md), targeting `main` with exact workspace integration
after merge.

The existing `spec / verify candidate` PR job validates proposals. Review the
manifest and lockfile changes, require its frozen install and candidate checks
to pass, and resolve failures through the normal tracked change workflow.
Monitoring configuration does not authorize publication. The existing manual
publication procedure remains in [README.md](../../README.md).

`toolchain.json` remains the source for the exact build runtime. Dependabot
recognizes pnpm from `pnpm-lock.yaml`, but its version detection reads
`package.json` and the lockfile rather than this custom toolchain file; the
updater may run a different pnpm version. Do not add a `packageManager` field to
the published metadata merely to influence the updater. Confirm the first
hosted npm proposal installs and verifies with the repository's pinned
toolchain before considering that lane operational. If its lockfile is
incompatible, pause that lane and record the update-job evidence in #44 while
retaining Actions monitoring.

This maintainer note is outside the package's `files` whitelist. Changes to
monitoring alone do not require regenerating the specification manifest or
archive, or editing the shipped README.
