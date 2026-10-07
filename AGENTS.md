# Agent instructions

This repo is a package of agent skills consumed by the Vercel `skills` CLI (`npx skills add oheidemann/skills`).

## Layout

- One skill per folder: `skills/<name>/SKILL.md`. Folder name must equal the `name` in frontmatter.
- Supporting files (scripts, references, templates) live next to the `SKILL.md` that uses them.
- Every `SKILL.md` has YAML frontmatter with `name` and `description`. The description says what the skill does and when to use it; it is what the agent matches on.
- User-only skills (should never trigger on their own) set `disable-model-invocation: true` in frontmatter and ship `agents/openai.yaml` with `policy.allow_implicit_invocation: false` (the Codex equivalent).

## When adding, renaming, or removing a skill

1. Update the table in `README.md` (skill name linked to its `SKILL.md`).
2. Verify the CLI still discovers it: `npx skills@latest add . -l`.

## Local development

Installs from GitHub are copies, so edits here don't reach installed agents until pushed and updated (`npx skills update -g`). To test uncommitted changes, install from the working tree: `npx skills@latest add . -g -a claude-code codex -s <name> -y`.
