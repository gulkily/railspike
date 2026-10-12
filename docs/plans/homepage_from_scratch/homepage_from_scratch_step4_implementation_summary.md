> **Feature plan:** [Step 1](./homepage_from_scratch_step1_solution_assessment.md) · [Step 2](./homepage_from_scratch_step2_feature_description.md) · [Step 3](./homepage_from_scratch_step3_development_plan.md) · [Step 4](./homepage_from_scratch_step4_implementation_summary.md)

Debug mode: enabled

## Stage 1 - Working unstyled page
- Changes:
  - New `index.html` (2.8 KB) replaces the removed file in the same commit, so no commit leaves the site blank: claim, what it is, install command, first prompt, and approval step, with `.gitmodules` review note, quick-start link, and source and license links.
  - Head metadata (title, description, canonical, icon, Open Graph) kept at the same URLs; text updated to the new claim.
  - No stylesheet or script yet; the page uses browser defaults until Stage 4.
- Verification:
  - Claim-source check: every sentence below was matched verbatim against `README.md` by script (all found).
    - Tagline, "Markdown instructions your agent follows", and plan-then-stop behavior: README intro.
    - Branch, one stage at a time, verify and commit: README intro.
    - Supported agents: README intro; no CLI or runtime dependencies: README intro.
    - Install command, first prompt, `.gitmodules` review, `Approved Step 1`: README Quick start.
  - Links: only `railspike-logo.png` (exists), the repository, `#quick-start` (heading exists), `LICENSE` (exists), and the canonical URL.
  - Page has no scripts, styles, or third-party requests; rendered once in headless Chrome at 1280×720.
- Notes:
  - `BACKLOG.md` has an uncommitted user-requested edit (logo and paper entries); intentionally excluded from stage commits and awaiting the maintainer.
  - First-screen position, contrast, and phone layout are assessed in Stage 4.

## Stage 2 - Real worked example
- Changes:
  - `index.html` gains an "A real example" section from this repository's `quiet_debug_mode` feature: the Original Query, Option A in full with the headings of Options B and C, and the first two recommendation paragraphs, as raw Markdown in code blocks; plus the three planning and stage commit subjects.
  - Links point to the Step 1 file and feature folder at commit `68663ca` and to stage commit `d84023f`, all on `origin/master`.
  - Omissions are marked `[…]` and stated in the text; the page says the approval reply is typed in conversation and not stored.
- Verification:
  - Script check against `git show 68663ca:<file>`: request, Option A, option headings, and recommendation excerpts are each an exact substring of the source; the commit list equals `git log --reverse` for the feature folder.
  - Commits `68663ca` and `d84023f` are ancestors of `origin/master`; the feature folder exists at `68663ca`.
  - Page is 5.7 KB with no scripts or styles.
- Notes:
  - This feature was chosen over the website redesign because it is compact and complete; its outcome is a documentation change, so Step 4 evidence is commit subjects rather than a running demo.
  - `BACKLOG.md` remains an uncommitted maintainer edit, excluded here.

## Stage 3 - Limits, failure modes, and footer
- Changes:
  - `index.html` gains a "Limits and failure modes" section: gates are instructions, not enforcement; it does not read for you; it adds process and is overkill for a one-line fix; plans must stay small; plus three failure modes (approval skipped, scope expands in Step 4, stage commit or verification missing) with recovery.
  - Footer links: source, quick start, `RAILSPIKE.md`, failure-modes guide, license.
- Verification:
  - Script check: each limit and recovery statement was matched against `README.md` and `docs/failure-modes.md`; one sentence that went beyond the source ("nothing in Git or the tooling prevents it") was replaced with the README's own wording.
  - Link check: repository files linked exist in the working tree; hash-pinned example links verified in Stage 2.
  - Page is 7.5 KB, no scripts or styles.
- Notes:
  - The failure-mode bullets are condensed paraphrases of the guide; the guide is linked for the full signals.
  - Claims in the HN draft (for example about hallucinations) were deliberately left out because the README does not state them.
  - `BACKLOG.md` remains an uncommitted maintainer edit, excluded here.

## Stage 4 - Text-first styling
- Changes:
  - Inline stylesheet in `index.html`: system serif body, system monospace code, 42rem measure, light and dark through `prefers-color-scheme`, left-ruled code blocks, and a gold accent for the wordmark and code rules.
  - The install command now sits directly after the intro paragraph, and the sentence about supported agents and "no CLI" moved below it (split so the review note stays next to the command), to keep the install command on the first phone screen. Wording is otherwise unchanged.
- Verification:
  - First screen (iframe at exact viewport size): install command ends at 573 px of 640 px at 360×640 and 421 px of 720 px at 1280×720. Before the reorder it ended at 714 px on the phone.
  - No horizontal overflow at 360 px (scrollWidth 345 = clientWidth) or 1280 px.
  - Contrast (WCAG): light text 17.2, muted 8.1, links 8.0 (7.2 on code), accent 5.5; dark text 14.9, muted 8.4, links 8.8 (7.9 on code), accent 9.6.
  - Light render at 1100 px and dark render (media query unwrapped, because headless Chrome could not emulate the system preference) inspected.
  - The README sentence about reviewing `.gitmodules` still matches verbatim.
- Notes:
  - Page is about 10 KB with no scripts or third-party requests.
  - Real OS dark-mode switching and non-Chromium browsers were not tested.
  - `BACKLOG.md` remains an uncommitted maintainer edit, excluded here.
