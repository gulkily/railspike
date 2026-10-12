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
