# UX Orchestrator

A reusable agent skill for supervising iterative UX implementation with Orca agents and Git worktrees. It keeps a stable integration preview available while workers implement changes, then carries user feedback through review, verification, and integration.

## Key features

- **Parallel work with clear ownership:** Give each coding task an isolated branch and worktree, with a bounded deliverable and explicit edit ownership.
- **Stable review preview:** Keep the integration preview running while task previews use separate ports. Check the combined experience after integration.
- **Feedback that stays current:** Update acceptance criteria as feedback arrives and check returned work against the latest requirements.
- **Preserved design alternatives:** Save complete variants on named branches and record the exact source revision for exports.
- **Durable project history:** Maintain `ux improvements.md` with completed changes, reasoning, completion times, and a separate **Questions for PM** section.
- **Verification before integration:** Review actual changes and evidence, run relevant checks, and distinguish visible prototype behavior from backend support.
- **Automatic resource cleanup:** Release settled workers and remove verified, merged temporary worktrees and branches while retaining the integration preview and saved alternatives.
- **Project-specific configuration:** Keep paths, ports, model preferences, task status, and export targets in project notes so the skill can be reused across projects.

## Requirements

- An agent environment that loads `SKILL.md` skills and supports Orca supervised workers.
- Orca with the installed **orchestration** and **orca-cli** skills. Their version-matched CLI guides define command syntax, worker lifecycle, settlement, and resource ownership.
- Git for isolated coding branches and worktrees, plus the project's development and verification commands.
- For external exports, the relevant authenticated tools and destination access.

The Orca dependency skills are supplied by the user's installed environment and are not bundled here. This repository contains workflow instructions, not a standalone agent runtime or export tool.

## Install

For the skills location used by this environment:

```bash
mkdir -p ~/.agents/skills
gh repo clone robertye-design/ux-orchestrator ~/.agents/skills/ux-orchestrator
```

This is a private repository: sign in with GitHub CLI and use an account with repository access. If your agent uses a different skill directory, clone the repository there as `ux-orchestrator`, keeping `SKILL.md` and `references/` together. If that directory already exists, back it up or update it deliberately before installation.

Start a new session or reload skills as supported by your agent environment, and confirm that `ux-orchestrator`, `orchestration`, and `orca-cli` are available.

## Example request

```text
Use $ux-orchestrator to coordinate these UX improvements in this project:
[describe the requested changes and acceptance criteria].
Keep the current preview available while independent tasks proceed.
Preserve the existing design as an alternative before replacing it.
```

The coordinator reads the project's `ux improvements.md`, including **Questions for PM**, and any referenced active plan. It owns the current acceptance criteria, review, integration, combined verification, and completion log. Workers own their bounded implementation and verification tasks.

## Workflow reference

- [Skill entrypoint](SKILL.md)
- [Implementation workflow](references/implementation-workflow.md)
- [Automatic cleanup procedure](references/implementation-workflow.md#7-automatic-cleanup-after-merge-or-task-completion)

The skill describes the coordination workflow. It follows the user's authorized scope and the installed Orca guides for operations.
