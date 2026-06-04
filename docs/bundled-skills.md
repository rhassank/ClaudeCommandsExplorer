# 🧩 Bundled Skills

> Skills that ship with Claude Code and are available in every session.

Unlike most built-in commands, which execute fixed logic, **bundled skills are prompt-based**: they give Claude detailed instructions and let it orchestrate the work with its tools. You invoke them like any skill — type `/` followed by the name — and Claude can also trigger some of them automatically when relevant.

## The bundled skills

| Skill | What it does |
| :-- | :-- |
| `/code-review [low…ultra] [--fix] [--comment] [target]` | Review the current diff for correctness bugs and for reuse, simplification, and efficiency cleanups. `--fix` applies findings to your working tree, `--comment` posts them as inline GitHub PR comments, and `ultra` (or `/code-review ultra`) runs a deep cloud review. |
| `/simplify [target]` | A cleanup-only review — four agents run in parallel covering reuse, simplification, efficiency, and level of abstraction — and applies the fixes. From v2.1.154 it does **not** look for correctness bugs; use `/code-review` for those. |
| `/debug [description]` | Enable debug logging for the session and troubleshoot by reading the debug log. Optionally describe the issue to focus the analysis. |
| `/batch <instruction>` | Orchestrate large-scale changes in parallel: researches the codebase, decomposes the work into 5–30 independent units, and after you approve, spawns one background subagent per unit in its own git worktree. Each implements its unit, runs tests, and opens a PR. Requires a git repo. |
| `/loop [interval] [prompt]` | Run a prompt repeatedly while the session stays open. Omit the interval and Claude self-paces; omit the prompt and Claude runs a maintenance check or `.claude/loop.md`. Alias: `/proactive`. |
| `/run` | Launch and drive your project's app to see a change working in the running app, not just in tests. (v2.1.145+) |
| `/verify` | Build and run your app to confirm a code change does what it should, without falling back to tests or type checks. (v2.1.145+) |
| `/run-skill-generator` | Record how to build, launch, and drive your app from a clean environment, writing a per-project skill at `.claude/skills/run-<name>/` so `/run` and `/verify` follow the recipe. (v2.1.145+) |
| `/claude-api [migrate \| managed-agents-onboard]` | Load Claude API reference material for your project's language and Managed Agents. Activates automatically when your code imports `anthropic` or `@anthropic-ai/sdk`. `migrate` upgrades existing API code to a newer model. |
| `/fewer-permission-prompts` | Scan your transcripts for common read-only Bash and MCP calls, then add a prioritized allowlist to project `.claude/settings.json` to reduce permission prompts. |

## Run and verify your app

Three of these work together to confirm changes against a running app instead of just tests:

- `/run` and `/verify` work without setup — they infer the launch from your project type and from your README, `package.json`, or `Makefile`.
- That inference gets unreliable for projects needing a database, env file, graphical session, or multi-step build. `/run-skill-generator` records the recipe once so every agent in the repo follows it.

> [!TIP]
> Bundled skills are invoked exactly like skills you write yourself. The difference is only that they ship with Claude Code. See [Authoring Skills](authoring-skills.md) to build your own.

## A few built-ins are also available as skills

A handful of built-in commands are reachable through the Skill tool too, including `/init`, `/review`, and `/security-review`. Others like `/compact` are not.

---

Sources: [Skills — Bundled skills](https://code.claude.com/docs/en/slash-commands#bundled-skills) · [Commands reference](https://code.claude.com/docs/en/commands)
