# Railspike rename checklist

Rename Feature Development Process (FDP) to Railspike across the repository, installation instructions, and public presentation. The existing `railspike-logo.png` and `railspike-header.html` are the starting assets. The naming decisions below are settled; implementation and publishing status are tracked separately.

Backwards compatibility is explicitly out of scope: the maintainer is the only known user. Make a clean rename without legacy aliases, compatibility pointers, support for old installation paths or prompts, or an existing-user migration procedure. Update the maintainer's own checkout and any installations as needed. Preserve historical references where accurate; they are not compatibility commitments.

## Naming and scope

- [x] Do not maintain backwards compatibility with FDP; the maintainer is the only known user.
- [x] Use **Railspike** as the product name. Drop the proposed `rsp` utility; the agent will perform updates using native Git commands. The [abandoned CLI specification](./docs/plans/rsp_cli_spec.md) is retained only as historical context.
- [x] Installation uses one native `git submodule add` command; clone initialization also remains a native Git operation.
- [x] After updating Railspike, the agent outlines the changes and offers the user a choice: commit the submodule-pointer update or leave it uncommitted for review. Do not commit automatically.
- [x] Document a copyable request for the agent to update Railspike, with repository-state checks and fast-forward-only updates. The agent reports the old and new revisions, summarizes relevant upstream changes and any required user actions, shows the host-project diff, and asks whether to commit only the pointer update or leave it uncommitted.
- [x] Standardize the display name as **Railspike** and repository/path spelling as `railspike`; use “formerly FDP” only where historical context helps.
- [x] Use `gulkily/railspike` as the repository, with canonical URL `https://github.com/gulkily/railspike` and clone URL `https://github.com/gulkily/railspike.git`. References are updated; renaming the hosted repository remains pending.
- [x] Use `docs/railspike` as the installation path in host projects.
- [x] Replace active references to `docs/fdp` with `docs/railspike` without supporting the old path.
- [x] Use `RAILSPIKE.md` as the main instruction filename, replacing `FEATURE_DEVELOPMENT_PROCESS.md`; in host projects it will be `docs/railspike/RAILSPIKE.md`.
- [x] Rename the main instruction file and update all active references without leaving a compatibility pointer.
- [x] Use `docs/workflow/` within the Railspike repository for the per-step instructions currently under `docs/dev/feature_process/`.
- [x] Move the per-step instructions to `docs/workflow/` and update all active path references.
- [x] Use `@railspike` as the assistant prompt shorthand, with `@RAILSPIKE.md` as the intended file mention when the assistant offers autocomplete.
- [x] Update copyable assistant prompts to `@railspike`, with an explicit `docs/railspike/RAILSPIKE.md` fallback and no `@fdp` alias.
- [ ] Verify file mention resolution in the supported assistants, including whether typing `@railspike` offers `@RAILSPIKE.md`.
- [x] Keep the four-step workflow and approval rules unchanged during the rename. Any behavior changes are separate work.

## Documentation and examples

- [x] Update the title, introduction, installation commands, update commands, prompts, diagrams, and example labels in [README.md](./README.md).
- [x] Update product references in [RAILSPIKE.md](./RAILSPIKE.md), `docs/workflow/`, [CONTRIBUTING.md](./CONTRIBUTING.md), [docs/RELEASES.md](./docs/RELEASES.md), and [docs/failure-modes.md](./docs/failure-modes.md).
- [x] Update current explanatory copy in `examples/` and `examples/fixtures/`, including prompts and installation paths where applicable.
- [x] Preserve historical accuracy in `docs/plans/`, source quotations, and completed case studies. Add context for the old name where needed; do not rewrite commit hashes or unrelated `gulkily/v3` source URLs.
- [x] Audit filenames containing `fdp`, especially historical plans and `scripts/check-fdp-git-workflow.sh`; rename only where useful, updating every referring link.
- [x] Update [HN_POST_DRAFT.md](./HN_POST_DRAFT.md) and [HN_WRITEUP_READINESS_CHECKLIST.md](./HN_WRITEUP_READINESS_CHECKLIST.md) with the new name, final links, and matching product description.
- [x] Review `todo.txt` and `improve_mermaid.txt` for active references. Replace obsolete CLI proposals with the agreed agent-run Git update workflow.

## Installation and repository rename

- [x] Revise fresh-install and update instructions together, including `.gitmodules` URL/path keys, origin checks, submodule initialization, and pointer review commands.
- [ ] Update any maintainer-owned installations and host-project prompts or documentation to the new URL and `docs/railspike` path as needed; no general existing-user migration procedure is required.
- [x] Preserve clean-working-tree checks, occupied-path checks, and fast-forward-only updates in the Railspike installation and update workflow.
- [x] Update the workflow fixture in [scripts/check-railspike-git-workflow.sh](./scripts/check-railspike-git-workflow.sh) to match the chosen names and paths. Keep its temporary-directory prefix and cleanup guard in agreement.
- [x] Exercise a fresh Railspike install and subsequent Railspike updates in disposable repositories, including clone/init, update, and dirty-state refusal. Legacy FDP installations are outside the test scope.
- [ ] Rename the hosted repository when the renamed documentation and installation instructions are ready; update its description, homepage, topics, and any configured integrations.
- [ ] Update local Git remotes and ensure the local checkout directory uses `railspike`; adjust editor/workspace references affected by the move.
- [x] Keep `master` as the branch name for now; a rename to `main` is out of scope.
- [x] Verify the current hosted repository's default branch is `master` and use it consistently. Correct the HN draft's `blob/main` example link to match. Recheck after the hosted rename.
- [ ] Verify fresh clones from the canonical Railspike URL work after the hosted rename. Update active repository links; old URL redirects are not a release requirement.

## Logo and website

- [x] Keep the existing [railspike-logo.png](./railspike-logo.png) for launch; no logo redesign.
- [x] Check the existing logo at the header's 54 px and 42 px sizes and produce optimized web/favicon variants as needed.
- [x] Add the logo to the README with appropriate alternative text and consistent sizing.
- [x] Host the initial website as a GitHub Pages project site at `https://gulkily.github.io/railspike/`, using `gulkily/railspike`. Defer a separate organization and custom domain.
- [x] Keep the initial website to one landing page with a workflow overview, installation instructions, and links to the repository and worked example.
- [x] Use `index.html` at the repository root as the GitHub Pages entrypoint, using [railspike-header.html](./railspike-header.html) as the starting point.
- [x] Build the agreed landing page in root-level `index.html`.
- [ ] Verify the chosen website URL when publishing.
- [x] Replace the HTML's placeholder `/about`, `/docs`, and `/get-started` links with working destinations. Make the home link, navigation, and asset paths work under the `/railspike/` hosting base path.
- [x] Build out the page with a concise workflow description, four-step overview, installation/get-started instructions, worked example, and repository link.
- [x] Refine the current “Railspike — Developer Tools” title to describe this project; add a description, favicon, and sharing metadata using the final site URL.
- [x] Check the header at narrow widths, keyboard navigation and focus visibility, logo clarity, and access to essential navigation on mobile.
- [ ] Configure GitHub Pages hosting and HTTPS; verify published navigation and images at `https://gulkily.github.io/railspike/` before promoting the URL.

## Verification and release

- [x] Defer the first public release until after the rename and website are ready. The release version remains undecided.
- [x] Search for `FDP`, `fdp`, `Feature Development Process`, and old repository URLs, including untracked launch drafts. Review each remaining match as intentional history or a missed rename; remove legacy compatibility aliases or pointers.
- [x] Run `python scripts/check-markdown-links.py` and `git diff --check`; run the Perl/Node equivalents if their implementations change.
- [x] Run `bash scripts/check-railspike-git-workflow.sh` after updating the fixture.
- [ ] Manually check HTML links, external repository/example links, and rendered Markdown/Mermaid; the local Markdown checker does not validate these.
- [ ] Walk through the README as a new user, from installation to the first planning artifact, with the renamed prompt and paths.
- [x] Record the rename as an unreleased breaking change in `docs/RELEASES.md`, including canonical paths, prompt, and the lack of backwards compatibility. Release version selection remains deferred.
- [x] Review the final diff and commit the intended documentation, logo, and HTML assets. Exclude unrelated local/editor files.
- [ ] Publish and verify the website after completing the rename.
- [ ] Follow up after the rename and website are ready: choose the first release version, create the signed annotated tag, and publish the GitHub release using `docs/RELEASES.md`.
- [ ] Update the HN submission and other existing public references to the verified canonical URLs.

## Implementation status (October 12, 2026)

- Local work is on `rename/railspike`. No CLI was added; the original logo is reused for the page, README, favicon, and sharing image.
- The main and per-step instructions were compared against their originals after name/path substitutions: workflow and approval behavior are unchanged. Obsolete Step 3/4 compatibility entrypoints were removed.
- Markdown links pass both in the working tree and a clean export of the staged files. Whitespace and the README's exact Git update block pass local checks. Disposable fixtures cover installation, initialization at the recorded revision, attached/detached updates, no-op updates, dirty state, wrong origin/branch, unreviewed pointers, ahead/divergent history, and unavailable upstream.
- Chromium checks passed at 1280, 580, 390, and 320 px, including local assets/links under `/railspike/`, visible mobile navigation, and keyboard navigation. Desktop/mobile screenshots were visually reviewed. Autocomplete and GitHub Markdown/Mermaid rendering still need checks in their actual environments.
- Historical plans, source quotations, original commit links, and the copyright attribution retain FDP where appropriate. The ignored HN readiness checklist is included in the intended launch files because this checklist and the draft link to it.
- GitHub CLI is not authenticated. `gulkily/railspike` is not yet available through an unauthenticated clone check. The existing origin (`gulkily/fdp`) reports `master` as its default branch and is retained until the hosted rename succeeds.

## Remaining publishing steps

1. Authenticate GitHub CLI, then rename `gulkily/fdp` to `gulkily/railspike`; set the description and homepage to the new project name and `https://gulkily.github.io/railspike/`. Review topics and configured integrations.
2. Update the local origin to `https://github.com/gulkily/railspike.git`, publish the reviewed branch, and merge it into `master` through the repository's normal workflow. Update any maintainer-owned host installations separately.
3. Enable GitHub Pages from the `master` branch, `/` (root), and enforce HTTPS. The root `index.html` and `.nojekyll` are ready for this configuration.
4. Verify the live page, images, links, fresh clone, GitHub Markdown/Mermaid rendering, and assistant file mentions before promoting the URLs.
5. Only afterward, choose and publish the first release. HN submission remains a separate follow-up.
