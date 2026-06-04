# 📐 Command File Template (`.claude/commands/`)

> The simpler, older form. A file at `.claude/commands/<name>.md` creates `/<name>`. It still works and supports the same frontmatter — but skills are recommended because they also support supporting files and a directory layout.

> [!NOTE]
> If a skill and a `.claude/commands/` file share the same name, the **skill** takes precedence.

Save as `.claude/commands/<your-command>.md`. The **file name** (without `.md`) becomes the command.

```markdown
---
description: <What it does and when to use it.>
# argument-hint: [target]
# disable-model-invocation: true
# allowed-tools: Bash(git *)
---

<Instructions for the command.>
<Use $ARGUMENTS for input, and !`cmd` to inject live data.>
```

## Example — `.claude/commands/standup.md` → `/standup`

```markdown
---
description: Draft a standup update from today's git activity.
allowed-tools: Bash(git log *)
---

## Today's commits

!`git log --since=yesterday --oneline --author="$(git config user.name)"`

## Instructions

Turn the commits above into a short standup update with three parts:
Yesterday, Today, Blockers. Keep it to a few lines.
```

## When to use a command file vs. a skill

| Use a command file | Use a skill directory |
| :-- | :-- |
| A single prompt, nothing else | You need supporting files, scripts, or reference docs |
| Quick to drop in | You want richer frontmatter behavior and auto-invocation |
| Migrating existing `.claude/commands/` | Building something you'll maintain and share |

To convert a command file into a skill, move `.claude/commands/deploy.md` to `.claude/skills/deploy/SKILL.md`.

---

See [Authoring Skills](../docs/authoring-skills.md) for the full model.
