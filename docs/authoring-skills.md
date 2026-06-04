# 🛠️ Authoring Skills (Custom Commands)

> Build your own slash commands. In Claude Code, custom commands **are skills**.

Create a `SKILL.md` file with instructions and Claude adds it to its toolkit. Claude uses a skill when relevant, or you invoke it directly with `/skill-name`.

> [!NOTE]
> **Custom commands have been merged into skills.** A file at `.claude/commands/deploy.md` and a skill at `.claude/skills/deploy/SKILL.md` both create `/deploy` and work the same way. Existing `.claude/commands/` files keep working; skills add a directory for supporting files, frontmatter, and automatic invocation.

## Create your first skill

```bash
mkdir -p ~/.claude/skills/summarize-changes
```

Save this to `~/.claude/skills/summarize-changes/SKILL.md`:

```yaml
---
description: Summarizes uncommitted changes and flags anything risky. Use when the user asks what changed, wants a commit message, or asks to review their diff.
---

## Current changes

!`git diff HEAD`

## Instructions

Summarize the changes above in two or three bullet points, then list any risks
you notice such as missing error handling, hardcoded values, or tests that need
updating. If the diff is empty, say there are no uncommitted changes.
```

The directory name (`summarize-changes`) becomes the command. The `` !`git diff HEAD` `` line injects the live diff before Claude sees the prompt (see [Arguments & Injection](arguments-and-injection.md)). Now ask "What did I change?" or run `/summarize-changes`.

## Where skills live

| Location | Path | Applies to |
| :-- | :-- | :-- |
| Enterprise | Managed settings | All users in your org |
| Personal | `~/.claude/skills/<name>/SKILL.md` | All your projects |
| Project | `.claude/skills/<name>/SKILL.md` | This project only |
| Plugin | `<plugin>/skills/<name>/SKILL.md` | Where the plugin is enabled |

When names collide, enterprise overrides personal, which overrides project. Plugin skills are namespaced `plugin-name:skill-name`. If a skill and a `.claude/commands/` file share a name, the **skill** wins.

## How the command name is set

| Skill location | Command name comes from |
| :-- | :-- |
| `~/.claude/skills/<dir>/SKILL.md` or `.claude/skills/<dir>/SKILL.md` | The **directory name** |
| `.claude/commands/<file>.md` | The **file name** without extension |
| Plugin `skills/<dir>/SKILL.md` | Directory name, namespaced by plugin |

The frontmatter `name` field sets the **display label**, not what you type — except for a plugin-root `SKILL.md`.

## Frontmatter reference

All fields are optional; only `description` is recommended. The most useful ones:

| Field | Description |
| :-- | :-- |
| `description` | What the skill does and when to use it. Claude uses this to decide when to apply it. Put the key use case first (capped at 1,536 chars in the listing). |
| `when_to_use` | Extra trigger phrases / example requests, appended to `description`. |
| `argument-hint` | Autocomplete hint, e.g. `[issue-number]` or `[filename] [format]`. |
| `arguments` | Named positional arguments for `$name` substitution. |
| `disable-model-invocation` | `true` = only you can invoke it (good for `/deploy`, `/commit`). |
| `user-invocable` | `false` = only Claude can invoke it (background knowledge). |
| `allowed-tools` | Tools the skill may use without a permission prompt while active. |
| `disallowed-tools` | Tools removed from the pool while the skill is active. |
| `model` / `effort` | Override the model or effort level while the skill is active. |
| `context: fork` | Run the skill in a forked subagent context. |
| `agent` | Which subagent type to use when `context: fork` is set. |
| `paths` | Glob patterns that limit when the skill auto-activates. |
| `shell` | `bash` (default) or `powershell` for inline shell commands. |

## Control who invokes a skill

By default both you and Claude can invoke a skill. Two fields restrict that:

- `disable-model-invocation: true` — only **you** can invoke it. Use for actions with side effects (`/deploy`, `/commit`, `/send-slack-message`) where you don't want Claude deciding the timing.
- `user-invocable: false` — only **Claude** can invoke it. Use for background knowledge that isn't a meaningful command (e.g. a `legacy-system-context` skill).

## Supporting files

A skill is a directory; `SKILL.md` is the only required file. Add templates, reference docs, example outputs, or scripts and reference them from `SKILL.md` so Claude loads them only when needed:

```text
my-skill/
├── SKILL.md            # required: overview and navigation
├── reference.md        # detailed docs, loaded when needed
└── scripts/
    └── helper.py       # executed, not loaded into context
```

> [!TIP]
> Keep `SKILL.md` under ~500 lines. Once a skill loads, its content stays in context for the rest of the session, so every line is a recurring token cost. State what to do, not why.

## Run a skill in a subagent

Add `context: fork` to run the skill in isolation; the skill content becomes the subagent's prompt. Pick the executor with `agent` (`Explore`, `Plan`, `general-purpose`, or a custom subagent). Only use `context: fork` for skills with an explicit task, not pure reference content.

## Sharing and visibility

- **Project skills:** commit `.claude/skills/` to version control.
- **Plugins:** put skills in a plugin's `skills/` directory.
- **Managed:** deploy org-wide through managed settings.
- **`/reload-skills`** picks up skills added or changed on disk mid-session.

See [Examples](../examples/custom-skill-examples.md) for complete, real skills, and the [SKILL.md template](../templates/skill-template.md) to start.

---

Sources: [Skills documentation](https://code.claude.com/docs/en/slash-commands)
