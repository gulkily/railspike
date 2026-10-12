# Railspike

<img src="./railspike-logo.png" alt="Railspike rail and spike logo" width="96" height="96">

Railspike is a file-based, approval-gated workflow for keeping AI-assisted feature work scoped, reviewable, and verified.

Use it with Claude Code, GitHub Copilot, or Codex when a feature needs a decision record and deliberate review points—not just a plausible patch.

## Why use this?
- Keeps multi-step feature work inside the model context window by splitting guidance across files.
- Forces approvals between steps so the assistant cannot sprint ahead without human review.
- Encourages reuse of shared UI/API components instead of letting the AI fork markup or payloads.
- Limits plan bloat so every deliverable stays within a page and can be reviewed quickly.

If you frequently see Claude/Codex derail because requirements evolve mid-stream, treat this repo as the “rails” that keep both you and the assistant honest.

## Quick start

Install Railspike as a Git submodule at `docs/railspike` with one Git command. Updates are handled by your agent using native Git; there is no CLI utility.

[Main instructions](./RAILSPIKE.md) · [Website](https://gulkily.github.io/railspike/)

From the **root of a clean, non-bare Git working tree**, run these read-only checks first. Stop if a check does not have the stated result; do not clean, reset, stash, remove, or overwrite anything to make it pass.

```bash
# Both commands must print the same absolute path.
git rev-parse --show-toplevel
pwd -P

# Must print "false".
git rev-parse --is-bare-repository

# Must print nothing. This includes staged, unstaged, and untracked files.
git status --porcelain --untracked-files=all --ignore-submodules=none

# Must exit successfully; docs/railspike must not exist, including as a symlink.
test ! -L docs
test ! -e docs/railspike && test ! -L docs/railspike
```

When all checks pass, add Railspike. This command writes `.gitmodules`, stages the new submodule entry, and creates `docs/railspike`; it does not create a commit.

```bash
git submodule add --branch master https://github.com/gulkily/railspike.git docs/railspike
git status --short
git diff --cached -- .gitmodules docs/railspike
```

Inspect the displayed changes, then commit them through your normal repository workflow. Do not continue if the output shows files beyond `.gitmodules` and `docs/railspike`.

Type `@railspike` and select `RAILSPIKE.md` if your assistant offers it. If file mentions are unavailable, refer explicitly to `docs/railspike/RAILSPIKE.md`. Autocomplete depends on the assistant and its workspace indexing.

In your project, create `docs/plans/` if it does not exist. Then send your supported assistant this first prompt (adapt the story, but keep the explicit step request):

> As a user, I would like to export my saved searches as CSV, please write Step 1 of `@railspike`.

If the decision is straightforward, you may skip Step 1 and ask for Step 2 instead. Review each artifact before continuing. For example:

> Approved Step 1, please continue to Step 2.

After `Approved Step 3`, the assistant creates a feature branch, commits the approved planning documents first, then makes a separate commit—with the matching Step 4 summary update—for every completed stage. See the [failure-mode guide](./docs/failure-modes.md) for recovery guidance.

The first run should take only a few minutes: read the four-step overview, send the prompt, and inspect the resulting Step 1 artifact. Do not approve a step you have not reviewed.

## Repo layout
- `RAILSPIKE.md` – one-page overview of the entire chain plus key rules and warning signs.
- `docs/workflow/` – canonical instructions for each step. The assistant reprints these every time it advances.
  - `step1_solution_assessment.md`
  - `step2_feature_description.md`
  - `step3_development_plan_before.md`, `step3_development_plan_do.md`, `step3_development_plan_after.md`
  - `step4_implementation_before.md`, `step4_implementation_do.md`, `step4_implementation_after.md`
- `docs/plans/` (create per feature) – where you store the working artifacts: `{feature}_stepN_*.md` plus any auxiliary research. Move large efforts into `docs/plans/{feature}/` and update a local README for navigation.
- [BACKLOG.md](./BACKLOG.md) – remaining maintainer tasks, including launch verification and replacement examples.

## Reusing across projects

When cloning a project that already includes Railspike, either clone with `--recurse-submodules` or initialize just Railspike afterward:

```bash
git submodule update --init -- docs/railspike
```

This checks out the revision recorded by the host project, often in detached HEAD state. It does not update to the latest upstream revision.

### Ask your agent to update Railspike

> Update Railspike at `docs/railspike` using the Git workflow in its README. Stop if the host or submodule has unreviewed changes or unexpected configuration. Fast-forward only. Outline the upstream changes, old and new revisions, and any required actions; show me the host-project diff. Then offer to commit only the submodule-pointer change or leave it uncommitted for review. Do not commit until I choose.

The agent should read this procedure before updating. From the **host repository root**, the following guarded commands check the installation and fetch `master`. A clean detached checkout from clone initialization is supported, as is a clean `master` checkout. Run the entire block, stopping on any error:

<!-- railspike-update-start -->
```bash
(
set -eu
stop() { printf '%s\n' "$*" >&2; exit 1; }
expected_url=https://github.com/gulkily/railspike.git
[ "$(git rev-parse --is-bare-repository)" = false ] || stop 'Use a non-bare host repository.'
[ "$(git rev-parse --show-toplevel)" = "$(pwd -P)" ] || stop 'Start at the host repository root.'
[ -z "$(git status --porcelain --untracked-files=all --ignore-submodules=none)" ] || stop 'Review host changes before updating.'
[ ! -L docs ] && [ ! -L docs/railspike ] || stop 'Refusing a symlinked installation path.'
[ "$(git ls-files -s -- docs/railspike | cut -d ' ' -f 1)" = 160000 ] || stop 'Expected a registered Railspike submodule.'
[ "$(git config --file .gitmodules --get submodule.docs/railspike.path)" = docs/railspike ] || stop 'Unexpected submodule path.'
[ "$(git config --file .gitmodules --get submodule.docs/railspike.url)" = "$expected_url" ] || stop 'Unexpected registered URL.'
[ -f docs/railspike/.git ] || stop 'Initialize Railspike with git submodule update --init -- docs/railspike first.'
[ "$(git -C docs/railspike rev-parse --show-toplevel)" = "$(pwd -P)/docs/railspike" ] || stop 'Unexpected submodule checkout.'
[ -z "$(git -C docs/railspike status --porcelain --untracked-files=all --ignore-submodules=none)" ] || stop 'Review submodule changes before updating.'
[ "$(git -C docs/railspike remote get-url origin)" = "$expected_url" ] || stop 'Unexpected submodule origin.'
for configured_branch in "$(git config --file .gitmodules --get submodule.docs/railspike.branch || :)" "$(git config --local --get submodule.docs/railspike.branch || :)"; do
  case "$configured_branch" in ''|master) ;; *) stop 'Unexpected update branch.' ;; esac
done
case "$(git -C docs/railspike branch --show-current)" in
  ''|master) ;; *) stop 'Expected master or a detached checkout.' ;;
esac
old_revision=$(git -C docs/railspike rev-parse HEAD)
git -C docs/railspike fetch origin master
git -C docs/railspike merge-base --is-ancestor "$old_revision" FETCH_HEAD || stop 'Upstream diverged or local commits are ahead; inspect history.'
git -C docs/railspike -c merge.autostash=false merge --ff-only FETCH_HEAD
new_revision=$(git -C docs/railspike rev-parse HEAD)
printf 'Railspike: %s -> %s\n' "$old_revision" "$new_revision"
git -C docs/railspike log --oneline "$old_revision..$new_revision"
git diff --submodule=log -- docs/railspike
git status --short
)
```
<!-- railspike-update-end -->

After a successful update, summarize the relevant upstream changes and required actions, inspecting the upstream diff as needed. If the revision changed, offer **commit the pointer update** or **leave it uncommitted for review**. On approval, recheck that only `docs/railspike` changed, stage that path alone, and commit it. An already-current installation needs no commit.

If a check fails, stop and explain it. Do not reset, clean, stash, delete files, change remotes, or force an update to make a check pass. Fetch can change remote-tracking metadata even when an update is refused. If a network operation or update is interrupted, inspect the current checkout and host diff before retrying; do not assume rollback.

## How to run the chain with your AI pair
1. Kick things off with a plain request like `As a user, I would like to <story>, please write Step 1 of RAILSPIKE.md.` Make the story explicit so the assistant starts from the user’s perspective.
2. Let the assistant draft the artifact in `docs/plans/`, then review/edit it directly or issue follow-up instructions until you’re satisfied.
3. When the doc hits the bar, reply verbatim with `Approved Step N, please continue to Step N+1.` The bot must stop until that phrase arrives, so you control scope creep.
4. Repeat the review/approval loop for each step. Keep Step 1-3 planning docs uncommitted through drafting/review.
5. After `Approved Step 3`, create the Step 4 feature branch and make the first commit with only the approved Step 1-3 docs.
6. During Step 4, make at least one stage-scoped commit per completed stage, and include that stage's Step 4 summary update in the same commit.

The strict per-step files mean you always paste a small, targeted instruction block into the chat; no more scrolling through a 4k-token mega-brief.

## Workflow at a glance

**Approval chain: each planning step needs explicit approval before the next begins.**

```mermaid
flowchart TB
    subgraph PLAN ["Planning (uncommitted, docs/plans/)"]
        direction LR
        A([Feature request])
        S1["Step 1 (optional):<br/>Solution assessment"]
        S2["Step 2:<br/>Feature description"]
        S3["Step 3:<br/>Development plan"]
    end
    subgraph IMPL ["Implementation (feature branch)"]
        direction LR
        BR["Create branch +<br/>commit Steps 1–3"]
        S4["Stage N: implement, verify,<br/>commit with summary update"]
        M{"More<br/>stages?"}
        F["Final verification<br/>and handoff"]
    end
    A -.->|Complex| S1
    A -->|Simple| S2
    S1 -->|Approved Step 1| S2
    S1 -.->|Revise| S1
    S2 -->|Approved Step 2| S3
    S2 -.->|Revise| S2
    PLAN -->|Approved Step 3| IMPL
    S3 -.->|Revise| S3
    BR --> S4
    S4 --> M
    M -->|Next stage| S4
    M -->|Done| F
    classDef gate fill:#bf870033,stroke:#bf8700,stroke-width:2px
    classDef commit fill:#1a7f3733,stroke:#1a7f37,stroke-width:2px
    classDef stop fill:#cf222e33,stroke:#cf222e,stroke-width:2px
    class S1,S2,S3 gate
    class BR,S4 commit
```

The plan artifacts live in the consuming repository’s `docs/plans/`; the Railspike instruction files can remain under `docs/railspike/`. Approval gates stop forward progress. The feature branch begins only after Step 3, with a planning-doc commit; every Step 4 stage then gets its own auditable commit.

**Returning to planning: a scope change during Step 4 sends work back to Step 2.**

```mermaid
flowchart TB
    subgraph PLAN ["Planning (uncommitted, docs/plans/)"]
        direction LR
        N([Feature request]) --> S2["Step 2:<br/>Feature description"]
        S2 --> S3["Step 3:<br/>Development plan"]
        S3 --> A{"Approved<br/>Step 3?"}
        A -.->|Revise| S3
    end
    subgraph IMPL ["Implementation (feature branch)"]
        direction LR
        I["Implement<br/>stage"] --> Q{"New requirement,<br/>risk, or scope?"}
        Q -->|No change| V["Verify, update summary,<br/>commit stage"]
        V --> D{"More<br/>stages?"}
        D -->|Next stage| I
        D -->|Done| H([Handoff])
        Q -.->|Scope changed| R["Stop affected work;<br/>return to Step 2 above"]
    end
    PLAN -->|Approved Step 3| IMPL
    classDef gate fill:#bf870033,stroke:#bf8700,stroke-width:2px
    classDef commit fill:#1a7f3733,stroke:#1a7f37,stroke-width:2px
    classDef stop fill:#cf222e33,stroke:#cf222e,stroke-width:2px
    class A,Q,D gate
    class V commit
    class R stop
```

Returning to planning is a feature, not a failure: a new requirement or unresolved risk changes the approved boundary, so it must be reviewed before implementation resumes.

## Documentation checks

Run these before sharing a Railspike change. The link check validates local Markdown paths; review rendered Mermaid diagrams on GitHub after publication because GitHub owns the renderer.

The Markdown-link checker is available in Python, Perl, and Node.js so it can run in installation environments with different runtimes available. Choose whichever version fits your environment; installing all three runtimes is not required. We intentionally maintain these language alternatives with equivalent behavior and no third-party dependencies. When changing the checker itself, verify all three implementations.

```bash
# Choose one Markdown-link checker:
# Python 2.7+ or Python 3
python scripts/check-markdown-links.py

# Perl (core modules only)
perl scripts/check-markdown-links.pl

# Node.js
node scripts/check-markdown-links.mjs

# Then run the Git workflow and whitespace checks:
bash scripts/check-railspike-git-workflow.sh
git diff --check
git status --short
```

## What each step enforces
| Step | Goal | Key outputs |
| --- | --- | --- |
| Step 1 – Solution Assessment (optional) | Resolve ambiguity across competing approaches. | Original query (mechanically corrected only), plus a brief labeled understood-intent note when needed, then a ≤1-page pros/cons doc ending with a recommendation. |
| Step 2 – Feature Description | Nail down problem context, user stories, requirements, shared components, and success criteria. | `{feature}_step2_feature_description.md` |
| Step 3 – Development Plan | Break work into atomic stages with dependencies, verification notes, and component touchpoints. Prefer `## Stage N` headers plus flat bullets for each stage field. | `{feature}_step3_development_plan.md` |
| Step 4 – Implementation | Execute the approved artifact sequentially on a feature branch, logging applicable verification in a Step 4 summary. The artifact may be application changes or explicitly scoped documentation-only work. Prefer `## Stage N - title` headers plus bullets for changes, verification, and notes. | `{feature}_step4_implementation_summary.md` |

Each step/phase file lists guardrails plus "Next" instructions so the model always knows when to stop.

Every Step 1–4 artifact begins with a relative-link bar to the others, keeping the feature record navigable in GitHub.

## Tips for stubborn assistants
- **Reprint instructions**: before starting a step/phase, force the assistant to paste the relevant `docs/workflow/stepX...` file back to you. This keeps both sides aligned and provides an audit trail.
- **Call out risks early**: Step 2 records impact, early validation, and mitigation; Step 3 gates dependents on unresolved risks.
- **Shared component inventory**: Step 2 explicitly asks which canonical UI/API bits already exist. Reuse them; duplication is the fastest way models drift.
- **Finish a feature, not a layer**: Each cycle has a normal entry point, end-to-end outcome, and required recovery. Component-only work is internal maintenance.
- **Proportional verification**: Step 4 records verification appropriate to the approved artifact. Documentation-only work still requires document-integrity, evidence, link/path, and allowed-file-scope checks, but runtime, UI, deployment, migration, and release checks are not required unless the approved documents make a claim that needs them.
- **Documentation-only cycles**: Declare this work type and its allowed documentation file scope in Step 2, retain it in Step 3's Completion Contract, and do not alter application source, tests, CI, deployment configuration, or generated artifacts without returning for approval.

## Extending the process
- Need a domain-specific checklist? Fork one of the step files, add the extra bullets, and point your assistant to the customized version.
- Supporting artifacts (mockups, DB diagrams) belong beside the step docs in `docs/plans/{feature}/`. Reference them inside the deliverables but keep the main files concise.
- When a feature exceeds eight stages, start a new Step 2/3 cycle; each must remain a usable vertical slice.

## Getting help
Because every instruction lives in plain Markdown, you can diff tweaks, annotate lines for your assistant, or even inline reminders like “STOP after this file.” When in doubt, start from `RAILSPIKE.md` and follow the breadcrumbs.
