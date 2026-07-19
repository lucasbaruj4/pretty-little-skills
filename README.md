# Pretty Little Skills

A marketplace of [Claude Code](https://claude.com/claude-code) agent skills.

## Using this marketplace

Add it to Claude Code:

```
/plugin marketplace add lucasbaruj4/pretty-little-skills
```

Then install any skill from it:

```
/plugin install example-skill@pretty-little-skills
```

## Repository layout

```
.claude-plugin/
  marketplace.json      # lists every plugin in this repo
plugins/
  <skill-name>/
    .claude-plugin/
      plugin.json        # plugin metadata (name, version, description, author)
    skills/
      <skill-name>/
        SKILL.md         # the skill itself: frontmatter + instructions
        scripts/         # optional: helper scripts
        references/      # optional: docs loaded on demand
        assets/          # optional: templates/fixtures
```

Each plugin is self-contained and can also be added directly:

```
/plugin marketplace add lucasbaruj4/pretty-little-skills/plugins/<skill-name>
```

## Adding a new skill

1. Copy `plugins/example-skill` to `plugins/<your-skill-name>`.
2. Rename the inner `skills/example-skill` directory to match.
3. Update `.claude-plugin/plugin.json` (name, description, version).
4. Write `SKILL.md`: a short, specific `description` in the frontmatter
   (this is all Claude sees before deciding whether to load the skill),
   followed by clear instructions.
5. Add an entry for your plugin to the root `.claude-plugin/marketplace.json`.
6. Open a PR — see [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
