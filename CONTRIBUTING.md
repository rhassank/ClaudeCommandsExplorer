# Contributing

Thanks for helping keep this reference accurate. Because this repo documents a real, fast-moving product, **accuracy is the bar.**

## The golden rule

> Every command claim must match the official Claude Code documentation. If you add or change a command entry, cite the source.

Primary sources:
- [Commands reference](https://code.claude.com/docs/en/commands)
- [Skills documentation](https://code.claude.com/docs/en/slash-commands)

## What we accept

- **Corrections** when a command's name, arguments, purpose, alias, or availability changes upstream.
- **New commands** added to Claude Code (with the official purpose).
- **Custom-skill examples** built only from documented features.
- **Docs and interactive-site improvements.**

## How the command list is maintained

The interactive site (`index.html`) and `docs/command-reference.md` are generated from a single data set. When you add or edit a command:

1. Update the command's entry (name, `args`, `type`, `group`, `purpose`, optional `aliases`/`note`).
2. Regenerate both the site and the reference so they stay in sync.
3. Keep `type` accurate: `built-in`, `skill` (bundled skill), or `workflow`.

> [!NOTE]
> Don't hand-edit only one of `index.html` / `command-reference.md` — they must agree. Update the data source and regenerate.

## Quality bar for custom-skill examples

- Use **only documented features**: frontmatter fields, `$ARGUMENTS` / `$0` / `$1` / `$name`, `` !`cmd` `` injection, `allowed-tools`, `context: fork`.
- No invented syntax. If it isn't in the [skills docs](https://code.claude.com/docs/en/slash-commands), it doesn't go in.
- Skills with side effects should set `disable-model-invocation: true`.

## Safety

> [!IMPORTANT]
> - No secrets, tokens, or credentials in examples.
> - No destructive defaults (no `rm -rf`, no force-push to shared branches).
> - Skills should propose changes a human approves, not act silently.

## Style

- GitHub-flavored Markdown.
- Prompts and config in fenced code blocks (` ```yaml ` for SKILL.md, ` ```text ` for terminal).
- Keep the existing badge and emoji conventions.

## Code of conduct

Be kind, be constructive, assume good faith.
