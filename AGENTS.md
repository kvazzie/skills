# Repository instructions

- Put distributable skills under `skills/<name>/` and keep the frontmatter `name` equal to the directory name.
- Give automatically invoked skills a narrow, model-facing `description`. Mark explicit workflows with `disable-model-invocation: true` and `policy.allow_implicit_invocation: false` in `agents/openai.yaml`.
- Keep handoff templates replaceable. They are prose aids, not schemas, and no workflow may parse or depend on their headings or ordering.
- Keep each skill's supporting templates and references inside that skill's directory.
- Update `README.md` when a skill's public purpose, installation command, or cross-skill flow changes.
- Before publishing, run `npx skills add . --list` and inspect the rendered prompts with `npx skills use . --skill <skill>`.
