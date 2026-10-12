> **Feature plan:** [Step 1](./website_redesign_step1_solution_assessment.md) · [Step 2](./website_redesign_step2_feature_description.md) · [Step 3](./website_redesign_step3_development_plan.md) · [Step 4](./website_redesign_step4_implementation_summary.md)

Debug mode: enabled

## Setup
- Branch `feature/website-redesign`, created from `feature/quiet-debug-mode` (unmerged to `master`) so the quiet debug contract in use applies. A PR to `master` will include those commits unless that branch merges first.
- Planning commit `d6dec11` holds the approved plans, debug log, and `docs/plans/README.md` entry.
- `.gitignore` now ignores `/temp/` at the maintainer's request; it is outside this feature's allowed files and is left uncommitted pending the maintainer's call.
- The maintainer updated `temp/Railspike Readings.html` after Step 3: the first voice is now "Gulko's original" and the last is "Daniel Gackle". No scope change; Stage 3–4 use the updated file.

## Stage 1 - New logo asset
- Changes:
  - Replaced `railspike-logo.png` with a 512×512 palette PNG exported from `temp/Rail Spike Cross-Section Icon.png`; near-white and near-black pixels snapped to flat colors to remove compression noise.
- Verification:
  - Size 4,388 bytes (was 1,445,612), under the 100 KB target.
  - Viewed the exported image: rail, plate, and amber spike intact with clean edges; color matches the supplied icon.
  - The README references the same filename, so no README change was needed.
  - Runtime, deployment, and release checks not applicable to this stage.
- Notes:
  - The icon has an opaque white background, which will show as a white tile on dark backgrounds; Stage 2 handles placement in dark mode.
