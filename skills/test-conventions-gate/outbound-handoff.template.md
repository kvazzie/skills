# Testing setup handoff

This template is a writing aid, not a data format. Reorder or rename sections when that makes the handoff clearer.

## Required workflow

Invoke `$establish-testing` before setting up tests. This is an explicit user request carried by this handoff. If that skill is unavailable, run `npx skills use kvazzie/skills@establish-testing` and follow the emitted instructions.

## Original work

Describe the original task and the permanent test it requires. State whether the original session is blocked by a test-first workflow or may continue production work.

## Why testing setup was delegated

Explain in prose why the current repository state does not determine a safe testing convention. Cite the files, configuration, commands, and examples that support the explanation. Name each decision that would otherwise be guessed.

## Decisions already supplied

Record testing choices the user has already made so the fresh session does not ask for them again.

## Repository context

Point to the relevant code, manifests, instructions, test files, configuration, CI, and working state. Reference artifacts rather than copying them.

Record the original session's return route when the host supports one, and the chosen working-tree location. For a separate worktree, identify the original working tree and explain what repository state the setup session can access.

## Completion required

Finish the testing setup, update the repository, verify it, and return a handoff for the original session. Do not return open design questions as a completed result.

Send the completion handoff through the specified return route when available. Otherwise give it to the user to bring back. If using a separate worktree, include its path, branch, and the changes the original session needs to transfer.
