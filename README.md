# Skills

Agent skills I use to make AI-assisted work more deliberate, capable, and efficient.

The repository follows a simple rule: each skill should encode one reusable discipline, stay small enough to understand, and compose cleanly with other skills and agents.

## Install

Install with [skills.sh](https://skills.sh):

```bash
npx skills@latest add VedankPurohit/skills
```

Then select the skills and supported agents you want to install them on.

## Skills

### Productivity

- [`orchestrate`](./skills/productivity/orchestrate/SKILL.md) — Manage substantial coding, research, exploration, and review through the smallest useful team of available agents, then synthesize and verify their work.

## Philosophy

- Delegate work, not accountability.
- Match the team to the task instead of spawning a fixed swarm.
- Use the least expensive model likely to meet the quality bar.
- Keep the main agent responsible for integration, verification, and the final answer.
- Treat every worker result as evidence to inspect, not truth to repeat.

## Repository layout

```text
skills/
  productivity/
    orchestrate/
      SKILL.md
      agents/openai.yaml
      references/model-bench.md
```

## License

[MIT](./LICENSE)
