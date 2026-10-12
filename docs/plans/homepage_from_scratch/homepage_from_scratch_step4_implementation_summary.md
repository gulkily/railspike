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
