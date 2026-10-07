# Skills

My personal agent skills, installable with the [Vercel `skills` CLI](https://github.com/vercel-labs/skills).

## Install

```bash
# all skills, globally, for Claude Code
npx skills@latest add oheidemann/skills -g -a claude-code

# a single skill
npx skills@latest add oheidemann/skills -g -a claude-code -s adversarial-review

# see what's in here without installing
npx skills@latest add oheidemann/skills -l
```

Drop `-a claude-code` to pick agents interactively, or use `-a '*'` for every agent. Update later with `npx skills update -g`.

## Skills

| Skill | What it does |
| --- | --- |
| [adversarial-review](skills/adversarial-review/SKILL.md) | Three-pass code review (finder, adversary, referee) in isolated subagents. User-invoked. |
| [park](skills/park/SKILL.md) | File a loose idea into the repo's `parking-lot/`, folding it into a matching concept if one exists. User-invoked. |
| [settle-code-review](skills/settle-code-review/SKILL.md) | Walk a review's open findings one at a time with the user; a standing implementer builds each decision on a review branch. User-invoked. |
