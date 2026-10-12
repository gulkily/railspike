# Railspike CLI specification

Status: abandoned. The user decided against a command-line utility. Installation remains one native `git submodule add` command, and the agent will handle updates with native Git commands. See the [rename checklist](../../RAILSPIKE_RENAME_CHECKLIST.md) for the active decisions.

Everything below is the superseded proposal, preserved for historical context. Its command contracts, decisions, and open questions are no longer active requirements.

## Purpose

Give maintainers a small command-line utility for updating an existing Railspike installation in a Git project. Replace the need to compose the documented Git commands manually while leaving changes visible for review and commits under the maintainer's control.

## Confirmed decisions

- Product: **Railspike**; executable: `rsp`.
- Repository: `https://github.com/gulkily/railspike`; clone URL: `https://github.com/gulkily/railspike.git`.
- Host-project installation: `docs/railspike` as a Git submodule, added with one native `git submodule add` command.
- The utility handles updates only; installation and clone initialization use Git directly.
- Main instructions: `RAILSPIKE.md`; per-step instructions: `docs/workflow/` within the Railspike repository.
- Assistant shorthand: `@railspike`, selecting `@RAILSPIKE.md` where autocomplete supports it.
- The four-step workflow and its approval rules remain unchanged.
- No FDP compatibility aliases, legacy-path support, or migration tooling.

## Proposed first-release scope

The following command contract is proposed, not yet approved. The confirmed scope is updates only. Installation, clone initialization, a separate status command, task creation, assistant execution, approval recording, and workflow automation are outside the utility scope.

| Command | Outcome |
| --- | --- |
| `rsp sync` | Fetch and fast-forward an initialized Railspike installation to the supported upstream branch. |
| `rsp --help` | Explain commands, prerequisites, affected paths, and review responsibilities. |
| `rsp --version` | Report the installed utility version. |

### Common behavior

- Resolve the host Git root when invoked from its root or a nested directory. Refuse bare repositories, non-Git locations, and mutation commands invoked from inside the managed Railspike submodule.
- Use the fixed installation path and canonical upstream. Custom paths, arbitrary remotes, and legacy FDP locations are not supported in this release.
- Before mutations, validate the host index and working tree, including untracked files, and the installation's identity and state. Refuse dirty state, unreviewed pointer changes, unexpected URLs or branch configuration, and conflicting paths with an actionable explanation.
- Reject symlinked destination paths or parent directories that could redirect writes outside the intended host location.
- Never create host commits, stash changes, reset history, force updates, or overwrite conflicting content. Touch only the Railspike installation and its required Git metadata; leave unrelated submodules and host files alone.
- Show the operation, target path, and affected Git changes. On success, explain what to review and commit; on failure, identify the failed operation, any partial changes, and a nondestructive next step. Do not claim automatic rollback.
- Return `0` for success, `2` for invalid command usage, and `1` for an unmet prerequisite, unsafe state, or Git/network failure. Send diagnostics to stderr and normal results to stdout.

## Installation and clone initialization (native Git)

From the root of a clean host repository with an unoccupied `docs/railspike` path, installation is one command:

```bash
git submodule add https://github.com/gulkily/railspike.git docs/railspike
```

This uses the upstream default branch and stages `.gitmodules` and the gitlink; the maintainer reviews and commits them. The final repository URL must be live before publishing these instructions. No utility bootstrap is required to add the submodule.

For a host cloned without submodules, initialize the recorded revision with:

```bash
git submodule update --init -- docs/railspike
```

Initialization does not advance the host's recorded pointer. A standard detached checkout is supported by the updater.

### `rsp sync`

Require a clean, initialized installation with expected registration and origin. An uninitialized installation must first use the native Git initialization command above. An absent installation produces guidance to the native installation command; the updater never installs it automatically.

Fetch the canonical upstream default branch (its final name remains to be verified). The documented install command does not set `submodule.<name>.branch`; missing branch configuration is therefore valid. Refuse an explicit conflicting branch override. Require the current commit to be an ancestor of the fetched target before advancing.

A standard detached checkout from native Git initialization is supported: advance the checkout to the fetched commit without inventing a local branch or rewriting local history. For an attached checkout, require the expected branch and a fast-forward-only update. Refuse divergent or locally ahead history.

If already current, succeed without file changes. Otherwise leave the host's changed gitlink unstaged for review; report old and new commit IDs and suggest the scoped diff and review commands. Do not perform a separate utility self-update. If the executable is shipped in the submodule, its on-disk version changes with the reviewed submodule revision; distribution and safe execution across that change remain to be specified.

## Distribution and recovery

Utility distribution, invocation, versioning, implementation language, dependencies, and supported operating systems remain decisions to make. Shipping the updater inside the Railspike submodule is an option; no independent utility installation is needed before adding that submodule.

Do not prescribe execution of a downloaded script through a shell pipe. Keep native Git installation guidance and replace only the manual update flow with the utility once implemented and verified. Existing historical installer plans are background, not the approved contract for this utility.

Preflight refusal must leave repository content and index unchanged. Fetches may change Git metadata even if an update cannot proceed. Incomplete native Git installations must be reported without attempting to repair or overwrite them. An interrupted update must report the observed checkout and pointer state before suggesting a retry. Recovery guidance must preserve existing work and distinguish retryable network errors from path or repository conflicts.

## Acceptance scenarios

- Set up a disposable host using the single documented `git submodule add` command; verify the updater accepts its default configuration without a separate branch setting.
- Clone that host without submodules, initialize with native Git, and verify the recorded commit is checked out even when upstream has advanced.
- Run `rsp sync` from the host root and a nested directory after an upstream advance; verify a fast-forward, an unstaged host pointer change, and no automatic commit. Repeat after committing the pointer to verify the no-op case.
- Refuse dirty hosts, dirty submodules, unreviewed pointer changes, conflicting or symlinked paths, incorrect remotes, missing registrations, uninitialized installations, non-Git/bare contexts, and divergent or locally ahead history without losing content.
- Simulate upstream unavailability and an interrupted update; verify accurate state reporting and safe retry/refusal behavior.
- Verify commands work with spaces in project paths and help and diagnostics match the exit-status contract.
- Verify installation and initialization remain native Git operations, with no utility install, init, or status subcommands.
- Follow the documented utility invocation and update flow on each supported platform before release.

## Decisions to resolve, one at a time

1. Choose the update command name: `rsp sync` or `rsp update`.
2. Choose utility distribution and invocation, including whether it ships inside the submodule.
3. Choose supported platforms and runtime dependencies.
4. Verify the canonical upstream branch and define utility/workflow release versioning.
5. Decide whether to implement the utility during the rename or as a subsequent effort.

## Background

- [Rename decisions](../../RAILSPIKE_RENAME_CHECKLIST.md)
- [Current installation and update guidance](../../README.md)
- [Historical installer proposal](./fdp_installer_step2_feature_description.md)
- [Subsequent Git-native distribution requirements](./fdp_distribution_safety_step2_feature_description.md)
