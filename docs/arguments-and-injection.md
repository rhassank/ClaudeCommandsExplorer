# 🔣 Arguments & Dynamic Injection

> Pass input to a skill and pull live data into it before Claude reads it.

These are the two mechanisms that make custom commands powerful and reusable.

## String substitutions (arguments)

When you invoke a skill, what you type after the name is available through substitution variables:

| Variable | Description |
| :-- | :-- |
| `$ARGUMENTS` | All arguments passed, as a single string. If absent from the content, arguments are appended as `ARGUMENTS: <value>`. |
| `$ARGUMENTS[N]` | A specific argument by 0-based index, e.g. `$ARGUMENTS[0]`. |
| `$N` | Shorthand for `$ARGUMENTS[N]` — `$0` is the first, `$1` the second. |
| `$name` | A named argument declared in the `arguments` frontmatter list. |
| `${CLAUDE_SESSION_ID}` | The current session ID. |
| `${CLAUDE_EFFORT}` | The current effort level (`low`–`max`). |
| `${CLAUDE_SKILL_DIR}` | The directory containing the skill's `SKILL.md`. Use it to reference bundled scripts. |

### Example — all arguments

```yaml
---
name: fix-issue
description: Fix a GitHub issue
disable-model-invocation: true
---

Fix GitHub issue $ARGUMENTS following our coding standards.

1. Read the issue description
2. Implement the fix
3. Write tests
4. Create a commit
```

Running `/fix-issue 123` sends Claude "Fix GitHub issue 123 following our coding standards…".

### Example — positional arguments

```yaml
---
name: migrate-component
description: Migrate a component from one framework to another
---

Migrate the $0 component from $1 to $2.
Preserve all existing behavior and tests.
```

`/migrate-component SearchBar React Vue` → `$0`=`SearchBar`, `$1`=`React`, `$2`=`Vue`. Indexed arguments use shell-style quoting, so wrap multi-word values in quotes: `/my-skill "hello world" second`.

## Dynamic context injection

The `` !`<command>` `` syntax runs a shell command **before** the skill content is sent to Claude. The output replaces the placeholder, so Claude receives real data, not the command.

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
Summarize this pull request...
```

What happens:

1. Each `` !`<command>` `` executes immediately, before Claude sees anything.
2. Its output replaces the placeholder in the skill content.
3. Claude receives the fully-rendered prompt with the real data inlined.

This is preprocessing — Claude does not run these commands; it only sees the result.

### Rules and gotchas

- The inline form is only recognized when `!` is at the **start of a line** or right after whitespace. `KEY=!`cmd`` is left as literal text.
- Substitution runs **once**; command output is not re-scanned for further placeholders.
- For multi-line commands, use a fenced block opened with ` ```! `:

````markdown
## Environment
```!
node --version
npm --version
git status --short
```
````

- Set `"disableSkillShellExecution": true` in settings to disable this (each command becomes `[shell command execution disabled by policy]`). Bundled and managed skills are unaffected.

> [!TIP]
> Combine the two: inject live context with `` !`cmd` `` and target it with `$ARGUMENTS`. That's how a single skill stays reusable across runs.

---

Sources: [Skills — string substitutions](https://code.claude.com/docs/en/slash-commands#available-string-substitutions) and [dynamic context injection](https://code.claude.com/docs/en/slash-commands#inject-dynamic-context)
