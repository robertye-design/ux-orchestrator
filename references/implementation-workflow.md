# Iterative UX implementation workflow

Apply this guidance when coordinating implementation across Orca workers. Use the
installed CLI's version-matched guide for command syntax and lifecycle operations.

## 1. Coordinator and worker responsibilities

The coordinator owns the current plan and acceptance criteria, distributes work,
answers worker questions, reviews results, integrates verified commits, and checks
the combined result. Keep a concise project note that records decisions, active
owners, completed evidence, and unresolved dependencies so work can resume without
reconstructing the conversation.

Give each worker a bounded deliverable with explicit edit ownership. Workers own
implementation and relevant verification within that boundary. Their completion
report should identify the branch and commit, changed behavior, checks performed,
and any gaps the coordinator needs to resolve. Follow the CLI guide's required
lifecycle report format.

Review the actual changes and evidence before integration. Resolve overlapping
ownership before two workers edit the same area. The coordinator remains
responsible for cross-task behavior after integration.

## 2. Isolated implementation and launch preferences

For independent coding tasks in a Git repository, use a separate branch and
worktree for each task. Read-only reviewers may inspect existing worktrees.
Choose each task's base deliberately: related changes need the agreed integration
baseline; an alternative or export may need an explicitly preserved revision.
Folder workspaces remain valid and do not require introducing Git.

Carry the user's requested agent, model, and reasoning effort into the launch
options. Verify the effective configuration in the launch receipt; a model name
written in a task prompt does not configure the worker. Keep session-specific
preferences in the plan rather than making one model mandatory for every project.

Workers commit verified implementation on their task branches. Integrate after
review, preserving unrelated user changes and alternatives.

Automatically clean up temporary task worktrees, branches, and settled worker
agents after integration and verification, following section 7. Tasks with no
code changes can be cleaned up after their deliverable is verified and evidence
is retained. Keep the integration preview, explicitly saved alternatives, and
workspaces the user is actively using.

## 3. Stable integration preview

When the user is reviewing a running preview, record its worktree, branch, URL,
port, launch command, and owning terminal in project notes. Keep that preview
available while parallel work proceeds. Give task previews and test servers
distinct ports; do not replace the integration server with a worker's checkout.

After integration, check the server response and compilation, then perform the
relevant permitted smoke check for the changed flow. An HTTP 200 alone does not
prove that the interface works. If the preview fails, inspect its actual terminal
and restore it from the recorded worktree and command. Target any necessary
process action narrowly, following Orca ownership rules.

## 4. Evolving user feedback

Treat new feedback as steering the active objective unless the user clearly
replaces or cancels it. Update concrete acceptance criteria and send changes to
affected workers through orchestration messages. Mark superseded requirements so
an earlier brief cannot silently override the latest direction.

Check the current criteria when reviewing returned work, including work that
finished while feedback was arriving. Continue independent tasks while a
clarification is pending; keep dependent work pending when an answer is required.
Use progress updates to explain decisions, completed behavior, and real blockers.

## 5. Preserved alternatives and export provenance

When the user asks to retain a design before replacing it, preserve its complete
state on a named branch and record the commit before implementing the replacement.
Keep alternatives isolated until the user chooses how to use them.

For an export, record which variant and revision must be captured, the required
states, and the target document or page. Give the export worker that exact source
and verify it before capture. Use a separate capture environment when necessary
to keep the integration preview available. Inspect the destination before adding
content and preserve existing work there.

## 6. Evidence and external-tool readiness

Run checks appropriate to the changed behavior in the task worktree, then verify
the important interactions across integrated changes. Record evidence and its
limits; avoid repeating broad checks without a remaining risk or required gate.

Distinguish visible UI behavior from backend support. Copy promising saved data,
form state, or a successful preview does not demonstrate persistence, targeting,
or an external write. Record missing contracts as unresolved work and report the
implemented scope accurately.

For an external deliverable, check that the required tools are callable early.
Authentication state and the current session's loaded capabilities are separate.
If authentication is confirmed but tools are missing, check session loading and
use a fresh configured session when needed; verify the required calls there before
preparing the full export. If the capability is still unavailable, report that
specific gap instead of repeatedly asking the user to authenticate.

Verify completed exports through the target artifact and returned node IDs or
links. Record the source revision, covered states, and any gaps in project notes.
Before reporting completion, finish automatic cleanup through the CLI's lifecycle
rules in section 7 and preserve user-retained worktrees and the active preview.

## 7. Automatic cleanup after merge or task completion

Treat cleanup as required work within the authorized task, with no extra
confirmation for temporary resources created for that task.

1. Accept the current Dispatch's valid completion report and review its result.
   If an immediate follow-up is needed, reuse the worker under a new Dispatch;
   otherwise run the installed guide's `worker-release` promptly. Release archives
   output and closes only the settled agent terminal. Inspect its receipt and
   follow any exact recovery action before acknowledging the Delivery.
2. For coding tasks, merge the verified commits and check the integrated result
   before removing the task worktree or branch. For review, export, or other tasks
   with no code changes, cleanup can follow verified task completion. A failed task
   can release its settled agent, but retain any unmerged work until it has a
   deliberate disposition; failed completion alone never authorizes discarding it.
3. Retain reports and necessary evidence outside the temporary worktree, and
   record commit IDs, deliverable links, task status, and resource ownership in
   the project notes. Check uncommitted and untracked files and all terminals in
   the exact worktree. Stop only positively identified task-owned preview/test
   servers through the documented Orca operations.
4. Remove the clean temporary worktree through `orca-cli`, which may also remove
   its merged task branch. Delete any remaining temporary task branch only when
   its commits are retained in the integration history or it has no unique
   changes. Verify both removals and that no worker
   remains reclaimable in the Run. Preserve the integration server and explicitly
   retained alternatives; do not force-delete unknown files or user-owned resources.
5. Record cleanup as completed before the final report. If Orca retains a resource
   because of user takeover, unresolved ownership, or an uncertain release, obey
   that verdict and report the exact remaining resource and reason. Never replace
   a refused or uncertain worker release with a raw terminal close or process kill.

Timeout, idle appearance, heartbeat, and stale completion are not task completion.
Use the version-matched orchestration guide for settlement, release, recovery,
and authority; this workflow does not change those lifecycle rules.
