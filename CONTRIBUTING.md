# Contributing

## Adding a skill

1. Create `plugins/<your-skill-name>/skills/<your-skill-name>/SKILL.md`.
2. Add `plugins/<your-skill-name>/.claude-plugin/plugin.json` with the
   plugin's name, version, description, and author.
3. Write `SKILL.md` with a specific, trigger-worthy `description` in the
   frontmatter and clear instructions in the body.
4. Register the plugin in the root `.claude-plugin/marketplace.json`.
5. Open a pull request.

## Guidelines

- One skill per plugin directory.
- Keep `SKILL.md` focused — move long reference material into `references/`
  and load it on demand rather than inlining everything.
- Test the skill locally (`/plugin marketplace add <local-path>`) before
  submitting.
