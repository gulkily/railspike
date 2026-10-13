> **Feature plan:** [Step 1](./installation_process_improvements_step1_solution_assessment.md) · [Step 2](./installation_process_improvements_step2_feature_description.md) · [Step 3](./installation_process_improvements_step3_development_plan.md) · [Step 4](./installation_process_improvements_step4_implementation_summary.md)

Debug mode: disabled

## Stage 1 - Default copy installation

- Changes: README now defaults to a single reviewed snapshot copied into the project, records provenance, preserves existing work/staging, verifies completeness, and documents bounded failure recovery. Submodules require explicit request and reviewed-revision matching. Organized the checklist and repaired its source links.
- Verification: reviewed dirty/staged work, nested repositories, unsafe extraction, occupied/redirected destinations, source-record collision, suspicious content, revision mismatch, and partial-copy recovery; evidence is recorded in the checklist. Targeted Markdown path/navigation checks and `git diff --check` passed; changed paths match the approved scope.
- Notes: `python3 scripts/check-markdown-links.py` reports preexisting failures in unrelated untracked plans and unchanged research evidence. Feature links resolve in this workspace; the supplied source log remains untracked and will not accompany a clone. This stage validates instructions, not a live installation. Runtime, UI, deployment, migration, and release checks are inapplicable to this documentation-only change. Manual updates and welcome changes follow in later stages.

## Stage 2 - Manual updates and reuse

- Changes: documented ordinary cloning of committed copies, manual updates against the recorded baseline, local-edit preservation, provenance ambiguity, recovery copies, and failed-replacement recovery. Labeled submodule initialization and updates separately; automatic conversion/updating remains excluded.
- Verification: reviewed unchanged/edited copies, missing provenance, unavailable baseline, partial replacement, concurrent edits, and existing submodules. `bash scripts/check-railspike-git-workflow.sh` passed; the marked update block matches `master` byte for byte. Targeted document paths/anchor and `git diff --check` passed; only README, checklist, and this summary changed.
- Notes: fixture coverage applies to the retained submodule update path; new copy-update behavior is instruction/scenario review. Runtime/UI/deployment/migration/release checks remain inapplicable. Stage 1's repository-wide link limitations still apply.
