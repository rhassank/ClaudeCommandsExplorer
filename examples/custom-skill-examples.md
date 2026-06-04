# 💼 Custom Skill Examples

> Complete, copy-ready skills built with the real Claude Code authoring model. Each is a `SKILL.md` you drop into `.claude/skills/<name>/`.

All of these use only documented features: frontmatter, `$ARGUMENTS`, `` !`cmd` `` injection, `allowed-tools`, and `context: fork`. See [Authoring Skills](../docs/authoring-skills.md) for the full reference.

## Summarize uncommitted changes

`~/.claude/skills/summarize-changes/SKILL.md` → `/summarize-changes`

```yaml
---
description: Summarizes uncommitted changes and flags anything risky. Use when the user asks what changed, wants a commit message, or asks to review their diff.
---

## Current changes

!`git diff HEAD`

## Instructions

Summarize the changes above in two or three bullet points, then list any risks
such as missing error handling, hardcoded values, or tests that need updating.
If the diff is empty, say there are no uncommitted changes.
```

## Commit, gated so only you trigger it

`~/.claude/skills/commit/SKILL.md` → `/commit`

```yaml
---
name: commit
description: Stage and commit the current changes
disable-model-invocation: true
allowed-tools: Bash(git add *) Bash(git commit *) Bash(git status *)
---

## Status

!`git status --short`

## Instructions

Stage the changes and create a single conventional-commits message that
describes them. Show me the message before committing.
```

`disable-model-invocation: true` means Claude won't commit on its own — only you can run `/commit`.

## Fix a GitHub issue by number

`~/.claude/skills/fix-issue/SKILL.md` → `/fix-issue 123`

```yaml
---
name: fix-issue
description: Fix a GitHub issue
argument-hint: [issue-number]
disable-model-invocation: true
---

Fix GitHub issue $ARGUMENTS following our coding standards.

1. Read the issue description
2. Understand the requirements
3. Implement the fix
4. Write tests
5. Create a commit
```

## Summarize a pull request (forked, read-only)

`~/.claude/skills/pr-summary/SKILL.md` → `/pr-summary`

```yaml
---
name: pr-summary
description: Summarize changes in a pull request
context: fork
agent: Explore
allowed-tools: Bash(gh *)
---

## Pull request context
- PR diff: !`gh pr diff`
- PR comments: !`gh pr view --comments`
- Changed files: !`gh pr diff --name-only`

## Your task
Summarize this pull request: what changed, why it likely changed, and any risks.
```

Runs in a forked `Explore` agent so it stays read-only and doesn't clutter your main context.

## Migrate a component between frameworks

`~/.claude/skills/migrate-component/SKILL.md` → `/migrate-component SearchBar React Vue`

```yaml
---
name: migrate-component
description: Migrate a component from one framework to another
argument-hint: [component] [from] [to]
---

Migrate the $0 component from $1 to $2.
Preserve all existing behavior and tests.
```

## Background knowledge (Claude-only)

`~/.claude/skills/legacy-billing/SKILL.md`

```yaml
---
name: legacy-billing
description: How the legacy billing system works. Reference when touching invoicing or payment code.
user-invocable: false
---

The legacy billing service runs nightly batch jobs, not real-time...
(reference content Claude applies when relevant)
```

`user-invocable: false` hides it from the `/` menu — it's knowledge, not a command.

> [!TIP]
> Start any new skill from the [SKILL.md template](../templates/skill-template.md), or use the [command-file template](../templates/command-file-template.md) for the simpler `.claude/commands/<name>.md` form.

---

Sources: [Skills documentation](https://code.claude.com/docs/en/slash-commands)
