> **Feature plan:** [Step 1](./prompted_installation_step1_solution_assessment.md) · [Step 2](./prompted_installation_step2_feature_description.md) · [Step 3](./prompted_installation_step3_development_plan.md) · [Step 4](./prompted_installation_step4_implementation_summary.md)

Debug mode: disabled

## Stage 1 - Prompted installation

- Changes: replaced manual quick-start commands with the chosen installation sentence; framed existing checks as agent guidance and documented inspection ordering, stop conditions, limitations, and result reporting.
- Verification: `python scripts/check-markdown-links.py` passed (62 files); `bash scripts/check-railspike-git-workflow.sh` passed; `git diff --check` passed. Compared installation command blocks and the update procedure against the planning commit: unchanged. Reviewed inspection-to-installation flow and confirmed only README and this summary changed.
- Notes: welcome handoff follows in Stage 2. Runtime, UI, deployment, migration, and release checks are not applicable to this documentation-only change.
