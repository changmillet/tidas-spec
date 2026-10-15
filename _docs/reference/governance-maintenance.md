---
title: Repository governance maintenance
docType: reference
scope: repo
status: active
authoritative: true
owner: tidas-spec
language: en
whenToUse:
  - when changing documentation ownership, coverage, routing or review rules
whenToUpdate:
  - when the governance maintenance boundary or validation procedure changes
checkPaths:
  - .docpact/**
  - _docs/reference/governance-maintenance.md
lastReviewedAt: 2026-10-16
lastReviewedCommit: 2fcf1c94f019e4ad7f2cfdccc57d817bbdc6cca4
lastReviewedNote: "Reviewed for #44: documentation navigation and dependency-monitoring governance are separate from the unchanged specification, package and publication contracts."
---

The repository contract remains [AGENTS.md](../../AGENTS.md), and the published
contributor and release guide remains [README.md](../../README.md).
[The Docpact configuration](../../.docpact/config.yaml) owns documentation
ownership, coverage, routing and review bindings.

Review configuration-only navigation and rule maintenance against this note
and record that review in the configuration and this nonpublished reference.
Do not refresh the shipped README merely to record that unchanged publication
boundaries were reviewed. A review must still check that each changed path has
the correct owner, required document and route, and that existing content and
release review obligations remain effective.

An actual change to ownership, repository responsibility, delivery rules or
other standing contracts must update AGENTS.md and any affected README
guidance. Changes to specification content, build behavior, package identity,
qualification or publication must update the documents that own those facts
and pass their existing rules. A configuration edit cannot substitute for those
source-document changes or remove their review obligations. The separate
dependency-monitoring procedure is in
[dependency-updates.md](dependency-updates.md).

Before accepting a governance change, use the workspace's Docpact wrapper with
this repository's absolute `--root`: validate the configuration strictly, lint
the complete changed-path set, inspect coverage and confirm routing. Check
positive and negative cases: an AGENTS, specification-asset or build/package
change must still require review of README.md; a monitoring-only change must
route to the dependency note, and a configuration-only change to this note.
Neither maintenance path should require a metadata-only README edit.

This reference is outside the published file whitelist. Dependency monitoring
does not change the asset-only package, toolchain, generated artifact hashes,
existing candidate CI, guarded manual publication or exact workspace
integration requirements. If those facts actually change, use their owning
contracts and validation rather than treating the change as maintenance.
