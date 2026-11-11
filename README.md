# kvazzie/skills

Personal agent skills for repository conventions and response formatting.

## Skills

### `response-formatting`

The central skill for response formatting. Its description asks agents to apply it to every response. It separates incidental asides and explanations of instructions and limitations from the main response with a Markdown blockquote. It is available for automatic invocation in supporting agents, but selection depends on the agent and is not guaranteed.

### `test-conventions-gate`

An automatically invoked guard for permanent tests. It activates when an agent needs to add a test but the repository does not make the intended test types, runner, layout, naming, style, dependencies, or commands clear. The skill records the evidence for that ambiguity and hands the setup work to a fresh session instead of inventing a convention or hiding a test under `scripts/`.

### `establish-testing`

The explicit workflow used by the fresh session. It researches the repository, interviews the user, installs the agreed test infrastructure, writes `TESTING.md`, adds a short pointer to the applicable `AGENTS.md`, verifies the setup, and returns a small handoff to the original session.

## Install

List the skills:

```bash
npx skills add kvazzie/skills --list
```

Install the skills:

```bash
npx skills add kvazzie/skills \
  --skill response-formatting \
  --skill test-conventions-gate \
  --skill establish-testing
```

Use the setup workflow once without installing it:

```bash
npx skills use kvazzie/skills@establish-testing
```

The workflow uses Matt Pocock's `grilling` skill for the interview and `handoff` when a portable file is needed for manual transfer. When either dependency is unavailable locally, the agent loads it for one run with `npx skills use mattpocock/skills@<skill>`.

## Flow

1. An agent reaches `test-conventions-gate` while working on a test.
2. The skill explains why the repository does not yet provide a safe, unambiguous convention.
3. When the environment supports it, the agent starts a fresh interactive session with the handoff text after the user chooses the current working tree or a new worktree. Otherwise, it creates a portable handoff file for the user to start the session.
4. The fresh session invokes `establish-testing`, settles the decisions with the user, and updates the repository.
5. It returns the handoff text directly to the original session when the environment supports delivery, or creates a portable handoff file for the user to bring back. For a separate worktree, the changes must also be transferred to the original working tree.

The original session may continue production work when the task does not require test-first development. It must leave tests and test infrastructure alone until the setup session finishes.

## License

MIT
