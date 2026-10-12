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

## Stage 2 - Modernized QDB look
- Changes:
  - `index.html`: replaced the stylesheet and header markup only; page content, section order, and links are unchanged. The only markup edit besides the header is replacing the hero headline's forced line break with a space (same words) and balancing its wrap.
  - Amber title bar with the logo and wordmark, a slim slash-separated menu (Workflow / Get started / Docs / GitHub), bordered blocks with amber top rules, monospace labels and code, system font stacks.
  - Light and dark color schemes via `prefers-color-scheme`; theme-color set to the amber.
- Verification:
  - Rendered with headless Chrome at 1200 px (light, dark) and 360 px: layout intact, no clipped content.
  - Overflow check at 360 px: `scrollWidth` equals `clientWidth`, so no horizontal scroll.
  - Amber used for bars and borders; link text uses a darker amber (light) or brighter amber (dark) for contrast. Contrast was judged visually, not measured with a tool.
  - `git diff --check` clean; changed files within allowed scope.
  - Deployment and release checks not applicable to this stage.
- Notes:
  - The logo keeps its opaque white tile, shown as a badge on the amber bar; dark mode needs no separate asset.
  - Keyboard focus styles were restyled but not yet exercised; Stage 4 and 5 cover keyboard walkthroughs.
