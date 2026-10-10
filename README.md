# ai-note-taking-app

An AI note-taking application for higher-education lecture capture: capture lecture
audio, transcribe it, and turn the transcript into study material a student can read,
search, and revise from. The project intent, audience, and boundaries live in
[`PROJECT.md`](PROJECT.md) and [`.content-system/project-brief.json`](.content-system/project-brief.json).
No implementation exists yet.

## Repository layout

This repository is an adopter of the agent stack: a set of pinned external tools that
govern how work is recorded, validated, and delivered. Nothing is vendored — each tool
is pinned to a certified commit and cloned at validation time.

| Component | Role | Owns |
| --- | --- | --- |
| **ACS** — agent-custom-setup | Multi-agent hot-loader | `.coord/` |
| **PCM** — project-continuity-modules | Task continuity and progression | `PROJECT.md`, `checkpoints/`, `tasks/`, `HANDOFF.md` |
| **CGM** — content-generation-modules | Content system and brief | `.content-system/` |
| **OIO** — observational-issue-ops | Issue-log surface and triage | `.oio/`, `.github/ISSUE_TEMPLATE/` |

The certified version set is published by the release train
(`Pukujan/agent-stack-train`) and mirrored in [`stack-manifest.json`](stack-manifest.json).
When one component moves, all four move together.

## Validation

Every pull request and every push to `main` runs [`acs-gates.yml`](.github/workflows/acs-gates.yml)
(job `gates`, `ubuntu-latest`). It fails closed: the stack manifest is checked against the
release train, then PCM, CGM, ACS, and the installed OIO surface are each validated in turn.
`gates` is the required status check on `main`.

## Auto-merge

[`auto-merge.yml`](.github/workflows/auto-merge.yml) arms GitHub's native auto-merge
(squash) on pull requests opened by the repository owner. A PR merges itself once `gates`
passes, with no human approval step. It only *arms* auto-merge — it never force-merges,
never bypasses `gates`, and never touches PRs from other authors.

## Working in this repository

- The operating contract for agents is [`AGENTS.md`](AGENTS.md).
- Exact pinned commands for every validator are in
  [`.github/workflows/acs-gates.yml`](.github/workflows/acs-gates.yml).
- Windows note: the OIO installer requires descriptor-relative no-follow filesystem
  operations and refuses on native Windows. Run it under WSL (see
  [observational-issue-ops#32](https://github.com/Pukujan/observational-issue-ops/issues/32)).
