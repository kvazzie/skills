---
name: establish-testing
description: Establish and document a repository's testing system through project research and a user interview, then install and verify the agreed infrastructure for an originating test task.
disable-model-invocation: true
---

# Establish testing

Run this workflow in a fresh session when a handoff explicitly asks for it. Its job is to turn an ambiguous testing situation into a working, documented project convention. The original session owns the test that exposed the gap.

## Load the interview primitive

Use `grilling` as the interview engine. If it is unavailable, run:

```bash
npx skills use mattpocock/skills@grilling
```

Follow the emitted instructions and add the research, decisions, artifacts, and completion criteria below. Work the design tree in rounds. Ask every decision whose prerequisites are settled, recommend an answer, and keep interviewing until no branch remains open. Facts come from the repository and current documentation; decisions come from the user.

## Research the project

Start from the outbound handoff, but verify its claims against the current working tree. Inspect:

- applicable `AGENTS.md`, `CLAUDE.md`, `TESTING.md`, and contributor documentation;
- language and framework manifests, dependency locks, and task definitions;
- existing test dependencies, runner and coverage configuration, CI, tests, fixtures, and helpers;
- architecture boundaries that affect meaningful test types;
- the latest 20 substantive commits and the diffs of the few relevant changes.

Skip merge commits and automated dependency updates when they say nothing about development style. Do not turn this into repository archaeology.

Describe contradictions and incomplete conventions to the user before proposing a repair. Preserve unrelated working-tree changes.

## Settle the design

The interview must decide every applicable item:

- which test types the project uses and the behavioral boundary of each;
- the framework or runner for each type;
- colocated or separate layout, exact directories, and filename patterns;
- test structure, assertions, fixtures, mocks, shared helpers, setup, and cleanup;
- commands for the full suite, each test type, one file, and one case;
- watch and coverage behavior when the project needs them;
- allowed test dependencies and how configuration changes are made;
- CI behavior;
- whether inconsistent existing tests will be preserved, repaired, or migrated;
- where project-wide and package-specific testing documentation belongs;
- how `AGENTS.md` and any independent `CLAUDE.md` should point to that documentation.

Treat built-in runners as candidates, not as adopted conventions. If external tools are being considered, fetch their current primary documentation. Offer no more than three viable options and recommend one based on compatibility, required test types, configuration cost, speed, maintenance, standards, and avoidable vendor lock-in.

Before editing, show the user one consolidated decision record. Begin implementation only after the user confirms that the design tree is closed.

## Build the agreed system

After confirmation:

1. Install the chosen dependencies and update the lockfile.
2. Add the runner, coverage, environment, and task configuration the decisions require.
3. Add standard commands for the full suite and each adopted test type.
4. Create or update the applicable `TESTING.md` from [TESTING.template.md](TESTING.template.md).
5. Add a short pointer to that document in the applicable project `AGENTS.md`.
6. Verify the setup with discovery, an empty-suite run, or a disposable test that is removed after the check.

Do not add a meaningless permanent smoke test merely to make the runner execute. Do not write the original test from the handoff. Do not change CI, migrate existing tests, replace conflicting instructions, or create commits unless the interview, handoff, or a later user message explicitly authorized that action.

## Write testing documentation

Put the general convention in the root `TESTING.md`. In a monorepo, keep shared rules there and use a package-local `TESTING.md` only when that package has a genuinely different test system.

Keep a compact quick-reference table at the top so an agent can recover placement and commands without reading the entire document. Adapt headings and prose to the project, but cover every applicable subject in the template. Omit a section only when it does not apply, never because the decision was skipped.

Add a short pointer to the applicable `AGENTS.md`. Match the surrounding language and structure while preserving this meaning:

```markdown
## Testing

When creating or changing tests, test infrastructure, or test dependencies, read `TESTING.md` first. It defines this project's test types, frameworks, file layout, naming, style, and commands.
```

Handle instruction files as follows:

- update an existing applicable `AGENTS.md`;
- create `AGENTS.md` at the relevant root when neither standard instruction file exists;
- edit `AGENTS.md` when `CLAUDE.md` is a symlink to it;
- when only an independent `CLAUDE.md` exists, or the two files diverge, explain the conflict and agree on the change during the interview;
- when existing testing instructions conflict with `TESTING.md`, get permission before replacing them with a pointer or otherwise resolving the conflict.

## Complete the return

Completion requires all agreed decisions to be written, the infrastructure to work, and the relevant commands to have been run successfully. If work is blocked, keep working with the current user or report the block in this session. Do not produce a completion handoff with unresolved questions.

Once complete, use `handoff`. If it is unavailable, run:

```bash
npx skills use mattpocock/skills@handoff
```

Follow the emitted instructions. Use [return-handoff.template.md](return-handoff.template.md) only as a writing aid. Its wording, headings, and ordering are deliberately replaceable; no agent or automation may parse them as an interface.

Keep the return brief. Point the original session to the applicable `TESTING.md` and the exact sections needed for its test. List changed files and verification results. Do not repeat conventions the original session will read from `TESTING.md`.

Use the return route supplied in the outbound handoff if the host supports it. If delivery is unavailable or fails, give the completion handoff to the user for the original session. When the setup used a separate worktree, include its path, branch, and the changes that must be transferred before the original session can use the setup. Do not claim delivery or transfer succeeded without checking.
