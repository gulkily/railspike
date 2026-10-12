> **Feature plan:** [Step 1](./repo_cleanup_step1_solution_assessment.md) · [Step 2](./repo_cleanup_step2_feature_description.md) · [Step 3](./repo_cleanup_step3_development_plan.md) · [Step 4](./repo_cleanup_step4_implementation_summary.md)

Debug mode: enabled

## Branch and planning commit
- Branch `feature/repo-cleanup`; planning commit `7fffb0e` contains Steps 1–3, this feature's debug log, and the `docs/plans/README.md` entry.
- At `Approved Step 3` the maintainer said "You can leave the backlog file": `BACKLOG.md` is not edited and its pending whitespace fix stays uncommitted and unstaged (see the Step 3 approval note).

## Stage 1 - Baseline evidence and reference check
- Changes:
  - No repository file changed besides this summary; `BACKLOG.md` repairs were removed from scope.
  - `docs/RELEASES.md`, `CONTRIBUTING.md`, `README.md`, `index.html`, and `scripts/` contain no references to the four files.
- Verification:
  - SHA-256 baselines:
    - `HN_POST_DRAFT.md` `66293b50…89e2d`
    - `HN_WRITEUP_READINESS_CHECKLIST.md` `f3a64dff…54b07`
    - `docs/case-study-candidates.md` `f33adba8…dc6c3`
    - `docs/positioning-checklist.md` `56a37397…08d9`
    - `railspike.txt` `575d95c6…e37b`
    - `temp/` (hash of per-file hashes) `db5080d1…1d`
  - `~/railspike-archive/` does not exist yet, so no name conflict.
  - Runtime, UI, deployment, and migration checks: not applicable (documentation-only).
- Notes:
  - **Open for the maintainer:** `BACKLOG.md` lines 3, 12, and 14 link three of the four files. Moving them leaves those links dead and the link checkers fail. Stage 2 is held until the maintainer chooses: edit those lines after all, keep the cited files in place, or accept the dead links.
