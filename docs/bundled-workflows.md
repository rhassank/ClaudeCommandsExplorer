# 🔀 Bundled Workflows

> Dynamic workflows that fan work out across many subagents and run in the background.

A **workflow** is a command marked as such in the [commands reference](https://code.claude.com/docs/en/commands). It decomposes a job and runs it across multiple subagents rather than executing inline.

## `/deep-research <question>`

Fan out web searches on a question, fetch and cross-check sources, and synthesize a **cited report**.

```text
/deep-research What are the trade-offs between server-driven UI approaches in 2026?
```

## Watching and managing workflows

Workflows run in the background. A few commands help you manage them:

| Command | Purpose |
| :-- | :-- |
| `/workflows` | Open the workflow progress view to watch, pause, resume, or save running and completed workflows. |
| `/tasks` | List and manage background tasks (alias `/bashes`). |
| `/background [prompt]` | Detach the whole session to run as a background agent and free the terminal (alias `/bg`). |
| `/stop` | Stop the current background session. |

## Related: large parallel changes

While `/batch` is classified as a **skill** rather than a workflow, it's the other main way to fan work out across the codebase — it splits a change into 5–30 units and runs each in its own git worktree subagent. See [Bundled Skills](bundled-skills.md).

> [!NOTE]
> `ultracode` effort and the `/ultraplan` / `/ultrareview` (now `/code-review ultra`) commands also orchestrate multi-agent work. See the [Command Reference](command-reference.md).

---

Sources: [Workflows](https://code.claude.com/docs/en/workflows) · [Commands reference](https://code.claude.com/docs/en/commands)
