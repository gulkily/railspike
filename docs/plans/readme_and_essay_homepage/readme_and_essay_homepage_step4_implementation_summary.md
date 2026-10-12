> **Feature plan:** [Step 1](./readme_and_essay_homepage_step1_solution_assessment.md) · [Step 2](./readme_and_essay_homepage_step2_feature_description.md) · [Step 3](./readme_and_essay_homepage_step3_development_plan.md) · [Step 4](./readme_and_essay_homepage_step4_implementation_summary.md)

Debug mode: enabled

## Stage 1 - Verbatim unstyled page
- Changes:
  - `index.html` (6.7 KB) replaced with markup generated from `railspike.txt` by script, not retyped: first line as the single `h1`, blank-line blocks as paragraphs, the one hyphen list as `<ul>`, and a footer with the repository link shown as its URL.
  - Head: title from the essay's first line, description and `og:description` from its first sentence; canonical, icon, and social image values unchanged. No scripts or styles yet.
- Verification:
  - Source: `railspike.txt`, UTF-8, no carriage returns, SHA-256 `575d95c6b2d20bea9d71ed237983d9494613a6b9389da3323ed4587b51c6e37b` (untracked; not committed by this feature).
  - Text comparison: page body text (footer link excluded), whitespace folded, equals the source with list markers removed; 5,113 characters each; "promt" is present.
  - One `h1`; zero `<script>` and `<style>` elements.
- Notes:
  - The link is the only added text and is the URL itself.
  - Styling, contrast, and head comparison with `master` follow in Stage 2.
