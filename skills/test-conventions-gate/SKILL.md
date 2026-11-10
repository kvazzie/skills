---
name: test-conventions-gate
description: Use before adding any test or persistent executable behavior check to a repository when the intended test types, framework or runner, file location, naming, style, dependencies, or commands are missing, incomplete, contradictory, or unclear. Diagnose the ambiguity and hand testing setup to a fresh session before choosing a convention. Skip disposable diagnostic probes that will not remain in the repository.
---

# Test conventions gate

A file's purpose decides whether it is a test. Any behavior check that will remain in the repository belongs to the project's test system, even when it could be named a script.

Use this gate to stop an agent from silently making a project-level testing decision. Do not use it as a wrapper around ordinary test writing when the applicable conventions are already clear.

## Check the gate

Before creating the test, inspect the current sources of truth that can settle the decision:

- applicable `AGENTS.md`, `CLAUDE.md`, and `TESTING.md` files;
- package manifests, dependency locks, task definitions, and documented commands;
- test runner and coverage configuration;
- CI workflows that execute tests;
- existing tests, fixtures, helpers, and their directory and naming patterns.

The gate is open only when these sources determine every choice needed for the proposed test: its type, runner, location, filename, style, dependencies, and command. A framework being technically available does not prove that the project wants it. One stray test or empty directory does not establish a convention.

When the choices are clear, read the applicable testing instructions and return to the original work. Do not create a handoff.

## Explain why the gate is closed

When any required choice remains uncertain, explain the actual evidence and the reasoning. Describe what was inspected, what it establishes, where sources disagree, and which decision would otherwise be invented. Do not substitute a label such as `missing`, `incomplete`, or `conflicting` for the explanation.

Distinguish among:

- no applicable rule;
- a rule that leaves a choice open;
- sources that prescribe different choices;
- an ecosystem default that the repository has not adopted.

Carry forward anything the user already specified. Prior answers reduce the interview; they do not make the remaining gaps safe to guess.

## Hand setup to a fresh session

Use the `handoff` skill to create a portable Markdown handoff in the operating system's temporary directory. If `handoff` is unavailable, run:

```bash
npx skills use mattpocock/skills@handoff
```

Follow the emitted handoff instructions. Use [outbound-handoff.template.md](outbound-handoff.template.md) as a checklist, not as a schema. Tailor the document to the original task and include:

- the original request and the permanent test it requires;
- the concrete evidence and reasoning that closed this gate;
- all testing decisions already supplied by the user;
- the exact choices still requiring agreement;
- relevant repository paths and current working state;
- an explicit user request for the fresh session to invoke `establish-testing`;
- a fallback telling the fresh-session agent, not the user, to run `npx skills use kvazzie/skills@establish-testing` if the skill is unavailable;
- a requirement to return only after the testing setup is complete.

## Start the setup session

Check the current environment's available tools and instructions for creating a fresh, user-interactive session and returning its result to this session. Follow the host's rules for those tools. A background subagent that cannot interview the user is not a substitute. Do not assume any particular host is installed.

When a fresh session can be started, ask the user whether to use the current working tree or a new worktree. Explain that a new worktree starts from a committed revision and does not automatically contain uncommitted changes. Wait for their answer before starting it. If the chosen location cannot access the repository state needed for setup, explain the limitation and agree on how to provide that state before proceeding. Preserve unrelated changes and follow the repository's Git workflow.

Start the fresh session in the chosen location with the handoff and enough context to find the original session. Make sure it can read the handoff, including when sessions do not share a temporary directory. Ask it to interview the user, complete `establish-testing`, and send the completion handoff back through the host's supported mechanism when available. Include the repository and working-tree paths, and for a new worktree ask it to identify its branch and the changes that must be transferred. Report the new session's link or identifier to the user.

In T3, when its thread tools and host instructions permit this workflow, use the thread launch tool with an explicit workspace strategy: use the project root or bind the existing worktree to match the current location, or request a new worktree from the appropriate committed base. Capture the originating thread's identity and instruct the setup thread to send the completion handoff back with the thread messaging tool. Use the tools' current documentation for arguments and permissions.

If the host cannot start an interactive session, give the handoff path to the user and ask them to start one. If automatic return is unavailable or fails, ask the user to bring the completion handoff back. Report launch or delivery failures rather than claiming success.

## Bound the original session

Until the setup result returns:

- leave tests, test dependencies, runner configuration, test commands, and testing documentation unchanged;
- stop the whole implementation when the task requires TDD or any other test-first workflow;
- otherwise, production work may continue without crossing the testing decisions delegated to the fresh session.

When the completion handoff arrives, confirm the setup changes are present in this working tree. If they are in a separate worktree, coordinate their transfer while preserving unrelated changes and following the repository's Git workflow; do not assume a reported completion made them available here. Then re-read the applicable `AGENTS.md` and the referenced sections of `TESTING.md`. The current session may still hold their old contents. Resume the original test only from the newly written sources of truth.
