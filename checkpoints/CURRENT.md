# Current Repository Checkpoint

<!-- continuity:current {"active_task":null,"active_task_file":null,"protocol_version":"0.1.0-draft","schema":"project-continuity.current.v1"} -->

This is an as-of projection; live GitHub issues own progression. Link the owning leaf, parent ancestry and dependencies for active work.

## Program state

Phase: bootstrap.

## Completed

- continuity protocol initialized.
- The full agent stack is installed as pinned external checkouts: the multi-agent
  hot-loader, the continuity modules, the content system, and the issue-log surface.
- The `gates` check runs on every pull request and every push to `main`, and `main`
  requires it before merging.
- Auto-merge is armed on owner pull requests, so a green pull request merges itself with
  no human approval step.
- The product README landed on `main` (merge `fefaff1`, PR #1). The first version failed
  the content-system adapter check because it named the helper; the rewrite describes the
  target product instead, and `gates` passed on the fixed tree.

## Active

- none.

## Queued

- create the first bounded task.

## Blockers

None known.

## Next atomic action

Create or identify the GitHub issue, record its NTA task/branch identity, then create the task projection with `continuity task new --issue <URL>`.
