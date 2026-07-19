# Contributing

## Adding a skill

1. Copy `plugins/example-skill` to `plugins/<your-skill-name>` and rename the
   nested `skills/example-skill` directory to match.
2. Fill in `plugins/<your-skill-name>/.claude-plugin/plugin.json`.
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
