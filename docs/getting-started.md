# 🚀 Getting Started

> How slash commands work in Claude Code, and where to go next.

## What a slash command is

In Claude Code, a slash command controls the session from inside it: switch models, manage permissions, clear context, review a diff, run a workflow, and more. Type `/` to see every command available to you, or type `/` followed by letters to filter.

Two rules from the [official docs](https://code.claude.com/docs/en/commands):

- A command is only recognized at the **start** of your message.
- Text after the command name is passed to it as **arguments**.

```text
/review 1234
```

Here `/review` is the command and `1234` is the argument (a PR number).

## Three kinds of commands

Claude Code ships with three kinds, and this repo documents all of them:

| Kind | What it is | Examples |
| :-- | :-- | :-- |
| **Built-in** | Behavior coded into the CLI. | `/init`, `/clear`, `/compact`, `/model`, `/diff`, `/review` |
| **Bundled skill** | A prompt handed to Claude that it can also trigger automatically. | `/code-review`, `/debug`, `/batch`, `/loop`, `/run`, `/verify` |
| **Bundled workflow** | A dynamic workflow that fans work out across many subagents. | `/deep-research` |

See the full list in the [Command Reference](command-reference.md), or browse it interactively in [`index.html`](../index.html).

## You can also write your own

This is the big one. **Custom commands are skills.** You create a `SKILL.md` file and its directory name becomes the command:

```text
.claude/skills/summarize-changes/SKILL.md   →   /summarize-changes
```

Older `.claude/commands/<name>.md` files still work too. Skills add optional features like supporting files, frontmatter, and automatic invocation. Learn the model in [Authoring Skills](authoring-skills.md).

> [!NOTE]
> Not every built-in command appears for every user — availability depends on your platform, plan, and Claude Code version. The interactive reference lists what exists in the docs; type `/` in your own session to see what's available to you.

## Where to go next

| If you want to… | Read |
| :-- | :-- |
| Browse every command | [Command Reference](command-reference.md) · [Interactive site](../index.html) |
| Understand the bundled skills | [Bundled Skills](bundled-skills.md) |
| Understand `/deep-research` and workflows | [Bundled Workflows](bundled-workflows.md) |
| Build your own command | [Authoring Skills](authoring-skills.md) |
| Use arguments and live data | [Arguments & Injection](arguments-and-injection.md) |
| Write reliable skills | [Best Practices](best-practices.md) |

Sources: [Commands reference](https://code.claude.com/docs/en/commands) · [Skills documentation](https://code.claude.com/docs/en/slash-commands)
