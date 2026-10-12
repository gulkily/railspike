# Homepage from scratch — Railspike debug log

## 2026-10-12T18:43Z — Step 1 (solution assessment)

### Necessary/useful instructions
- `docs/workflow/step1_solution_assessment.md` § Structure (Original Query, then Understood Intent): kept the user's wording intact while recording the removal of the old page and the branch state separately. Retain.
- `RAILSPIKE.md` § Warning Signs for Step 1 (>1 page, >4 options): held the document to three options. Retain.
- `RAILSPIKE.md` § Railspike Debug Mode: an explicit \"debug mode on\" in the request was recorded as `enabled` without ambiguity. Retain.

### Redundant/unnecessary instructions
- The Original Query rules appear in both `RAILSPIKE.md` § Key Rules and `step1_solution_assessment.md` § Structure with different wording. Suggest consolidating to one statement.
- The \"do not create Step 2 until Approved Step 1\" gate is repeated in three places. Suggest keeping the Step 1 file's version and linking.

### Inapplicable instructions
- Plan organization and commit rules under § Planning Artifacts: nothing is moved or committed at Step 1.
- Step 1 `## Review and revision`: no revision requested yet.

### Uncertain assessments
- The workflow places implementation after Step 3, but the request asked to remove the old designs first. The deletion was applied as an uncommitted working-tree change on a new branch from `master`; the instructions do not say how a pre-planning removal should be committed (a stage-1 commit after the planning commit is assumed).
- The instructions give no rule for the branch name or base when earlier unmerged feature work exists; the new branch was cut from `master` and the unmerged branch left alone.
- \"Get rid of the old designs\" could include plan records and logos; the narrower reading (only `index.html`) was taken.

## 2026-10-12T18:48Z — Step 2 (feature description)

### Necessary/useful instructions
- `step2_feature_description.md` § Delivery scope (work type and allowed files): kept the paper and logo features out of this one and bounded the homepage to `index.html`. Retain.
- § Risks \"impact, earliest validation, mitigation\": exposed the copy-quality and cross-feature dependency risks early. Retain.
- § Shared component inventory: showed that the page has no shared components of its own, only a referenced logo and linked docs. Retain.

### Redundant/unnecessary instructions
- Success criteria and Completion boundary both carry release checks. Suggest stating which section owns verification.
- The reprint-instructions rule repeats the file's own header for a user who already has it; a short summary was used.

### Inapplicable instructions
- Documentation-only clauses in Delivery scope and Completion boundary: this is an application change.
- API and data wording in the shared component inventory.

### Uncertain assessments
- A step document for one of three related features had to refer to the other two; the instructions do not say how cross-feature dependencies should be recorded beyond Risks.
- \"No UI mockups or implementation details\" sits uneasily with a content-led page; concrete copy requirements were stated as requirements, not wording.

## 2026-10-12T19:11Z — Step 3 (development plan)

### Necessary/useful instructions
- `step3_development_plan_do.md` § Structure (Completion Contract, Key Risks first): surfaced the blank-site risk from the deleted `index.html` before any work. Retain.
- `step3_development_plan_after.md` item 3 (plan completes the Contract): prompted a final verification stage. Retain.
- `RAILSPIKE.md` § Warning Signs for Step 3: kept to six stages of about an hour. Retain.

### Redundant/unnecessary instructions
- The uncommitted-planning rule appears in the Before file, the After file, and `RAILSPIKE.md` § Commit discipline. Suggest consolidating.
- Stage size is given as both \"about <=1 hour\" and \"<=50 lines of change\". Suggest one measure.

### Inapplicable instructions
- Database and function-signature guidance in the Do file.
- Documentation-only Completion Contract variant.

### Uncertain assessments
- The instructions do not say how to commit an unrelated user-requested edit made during planning (`BACKLOG.md`); it was left uncommitted and flagged.
- A pre-planning file deletion has no defined commit slot; it was folded into the first working-page commit (Stage 1) so no commit leaves the site blank.
