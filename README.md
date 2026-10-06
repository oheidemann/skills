# Skills

My personal agent skills, installable with the [Vercel `skills` CLI](https://github.com/vercel-labs/skills).

## Install

```bash
# all skills, globally, for every agent
npx skills@latest add oheidemann/skills -g

# a single skill
npx skills@latest add oheidemann/skills -g -s adversarial-review

# see what's in here without installing
npx skills@latest add oheidemann/skills -l
```

Update later with `npx skills update -g`.

## Skills

| Skill | What it does |
| --- | --- |
| [adversarial-review](skills/adversarial-review/SKILL.md) | Three-pass code review (finder, adversary, referee) in isolated subagents. User-invoked. |
| [settle-code-review](skills/settle-code-review/SKILL.md) | Walk a review's open findings one at a time with the user; a standing implementer builds each decision on a review branch. User-invoked. |
