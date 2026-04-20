# shiny-skills ✨

[中文](./README.zh.md)

A curated library of Claude Code skills that make you go "wow" — each one transforms a mundane task into something surprisingly delightful.

## What is a Skill?

A **skill** is a SKILL.md file that Claude Code detects automatically. When a user's request matches the skill's trigger conditions, Claude loads the skill and follows its instructions — no plugins, no setup, just drop the folder into `~/.claude/skills/`.

## Skills

| Skill | What it does |
|-------|-------------|
| [shiny-image-creation-skill](./shiny-image-creation-skill/) | Transforms a simple description into a structured AI image prompt across 27+ visual styles |

> More skills coming. Contributions welcome.

## Installation

```bash
git clone https://github.com/fluentlc/shiny-skills.git

# Install a specific skill
cp -r shiny-skills/<skill-name> ~/.claude/skills/
```

Each skill directory contains its own README with usage details.

## Contributing

Want to add a new skill? Open a PR — any skill that makes someone's jaw drop is welcome.

## License

MIT
