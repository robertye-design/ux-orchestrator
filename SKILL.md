---
name: ux-orchestrator
description: >-
  Supervise iterative UX implementation across Orca agents and worktrees while
  keeping a stable preview, carrying user feedback through review and integration,
  and preserving design alternatives. Use when the user requests orchestration
  of UX changes or repository instructions assign that supervision role.
---

# UX Orchestrator

Coordinate parallel UX work so the user can keep reviewing a stable integration
preview while isolated workers implement changes. The coordinator owns the current
acceptance criteria, review, integration, and the combined result.

## Start every session with the project log

Resolve the active project's repository or workspace root and read its
`ux improvements.md`, including **Questions for PM**, before planning or delegating
UX changes. This is the project's durable change history. Read any active plan it
references and give workers the canonical log path; the coordinator owns updates.

For an authorized implementation task, create the log if it is missing, with
**Time**, **Category**, **Improvement description**, and **Reasoning** columns plus
a separate **Questions for PM** section. Preserve an existing log and its questions.

After verification and integration, append each completed improvement with the
date and time it was completed and an explicit timezone convention. Use a trusted
clock or recorded completion/commit time. For historical backfills, identify the
source of the timestamp; mark unknown times instead of inventing them. Keep pending
work in the plan, and preserve existing history rather than rewriting it each session.

## Relationship to Orca skills

Read the installed `orchestration` skill and load its version-matched CLI guide
before operating supervised workers. That guide owns role classification, command
syntax, Run/Task/Dispatch authority, messaging, settlement, and resource ownership.
Use `orca-cli` as directed by that guide for worktree and terminal operations.

This skill adds the implementation workflow; it does not define alternative Orca
commands or lifecycle rules. Use it within the user's authorized scope. A request
for advice or a workflow preference alone does not start implementation workers.
Follow the official skill's handoff route when the user wants ownership transferred
without supervision.

## Implementation workflow

Read [the implementation workflow](references/implementation-workflow.md) when
planning or supervising iterative UX changes. It covers coordinator and worker
responsibilities, isolated implementation, stable previews, evolving feedback,
preserved alternatives, verification, and cleanup.

## Automatic cleanup

Cleanup is part of completion. Automatically release a settled worker agent when
no immediate follow-up remains; do not ask again to clean up task resources.
Remove its temporary worktree and task branch after verified code is merged, or
after a task with no code changes is complete and its evidence is retained outside
the worktree. Follow [the cleanup procedure](references/implementation-workflow.md#7-automatic-cleanup-after-merge-or-task-completion)
and Orca's settlement and ownership rules. Keep the integration preview and
explicitly preserved alternatives. Record completed cleanup and any resources
retained by user ownership or unresolved work in the project notes and final report.

Keep project paths, ports, branches, source revisions, export targets, current
model preferences, and task status in project notes. The reusable skill records
the workflow, so another project can use it without inheriting this session's
configuration.
