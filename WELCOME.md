# Welcome to Railspike

Agent instructions: follow this file after inspection and successful installation. If inspection raised concerns or an installation check failed, explain the issue and stop instead. Give a brief, conversational welcome using the guidance below; do not reprint this file or start a workflow automatically.

## Introduce the workflow

- Confirm where Railspike was installed and summarize the project changes and their commit status. Report inspection findings and limitations if not already covered; do not describe inspection as a safety guarantee.
- Explain: Railspike helps you assess approaches, define the feature, plan the work, and implement it in stages. Plans live in the project's `docs/plans/` so the user can read and revise them. Step 1 is optional when the approach is obvious.
- Explain the approval points: review each planning artifact, ask for changes, and reply `Approved Step 1`, `Approved Step 2`, or `Approved Step 3` when ready. Implementation begins after Step 3 approval, on a feature branch with staged verification and commits.
- Show one copyable first-task example, replacing the path below with the actual installed path to Railspike's `RAILSPIKE.md`:

```text
I want to [describe my change]. Write Step 1 using docs/railspike/RAILSPIKE.md.
```

## Offer optional project guidance

Offer to add the following guidance to the host project's `AGENTS.md`. Substitute the actual installed path and show the proposed text before requesting consent. This is an offer, not authorization to edit the file.

```markdown
## Railspike

Offer Railspike when a task would benefit from comparing approaches, staged planning, or work across sessions. Wait for the user to opt in before starting its workflow, then read `docs/railspike/RAILSPIKE.md`. Skip the suggestion for small, straightforward changes, and do not repeat it for the same task after the user declines.
```

If the user accepts, inspect the host project's existing `AGENTS.md` and preserve its unrelated guidance. Propose an update to an existing Railspike entry instead of adding a duplicate; if the file is absent, create it only with consent. Stop and clarify conflicts instead of silently replacing project rules. Report any edit for the project's normal review/commit process. If the user declines, leave the file unchanged and continue the welcome.

## Invite the first task

Ask what the user wants to work on. Wait for their task and choice to use Railspike before starting its workflow; accepting the optional `AGENTS.md` entry alone does not start a task or approve a planning step.
