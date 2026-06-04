# 📐 SKILL.md Template

> Copy this into `.claude/skills/<your-command>/SKILL.md`. The **directory name** becomes the command you type. Delete the comments before using.

```yaml
---
# Only `description` is recommended; everything else is optional.
description: <What it does and WHEN to use it — include words users would say.>

# --- Optional fields ---
# name: <display label in skill listings; does NOT change what you type>
# when_to_use: <extra trigger phrases / example requests>
# argument-hint: [issue-number]            # shown during autocomplete
# arguments: [issue, branch]               # enables $issue / $branch
# disable-model-invocation: true           # only YOU can invoke (use for side effects)
# user-invocable: false                    # only CLAUDE can invoke (background knowledge)
# allowed-tools: Bash(git *) Read Grep     # tools allowed without a prompt while active
# disallowed-tools: AskUserQuestion        # tools removed while active
# model: inherit                           # or a specific model
# effort: high                             # low | medium | high | xhigh | max
# context: fork                            # run in an isolated subagent
# agent: Explore                           # subagent type when context: fork
# paths: src/**/*.ts                       # only auto-activate for matching files
# shell: bash                              # bash (default) or powershell
---

## Context  (optional — inject live data BEFORE Claude reads this)

!`<shell command whose output is inlined, e.g. git diff HEAD>`

## Instructions

<State the one job. Use $ARGUMENTS / $0 / $1 for input the user passes.>
<State non-goals explicitly, e.g. "Do not change behavior" or "Show me before applying.">
```

## Filled-in example

```yaml
---
description: Review the current diff for bugs and unclear names. Use before committing.
allowed-tools: Bash(git diff *)
---

## Current diff

!`git diff HEAD`

## Instructions

Review the diff above. List correctness bugs, missing error handling, and
unclear names with line references. Do not rewrite the files — just report findings.
```

## Checklist

- [ ] `description` includes natural trigger keywords, key use case first
- [ ] Directory name is the command you want to type
- [ ] Side-effecting? Add `disable-model-invocation: true`
- [ ] Live data needed? Use `` !`cmd` `` injection
- [ ] Input needed? Use `$ARGUMENTS` / `$0` / `$1`
- [ ] Body is concise (it stays in context all session)
- [ ] Safe to share and commit (no secrets, no destructive defaults)

---

See the full [Authoring Skills](../docs/authoring-skills.md) guide and [Arguments & Injection](../docs/arguments-and-injection.md).
