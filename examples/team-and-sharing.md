# 👥 Team & Sharing

> How to distribute skills (custom commands) so a whole team uses the same ones.

Where a skill lives determines who can use it. This is the official scope model.

| Scope | Path | Applies to | How to share |
| :-- | :-- | :-- | :-- |
| **Personal** | `~/.claude/skills/<name>/SKILL.md` | All your projects | Just yours |
| **Project** | `.claude/skills/<name>/SKILL.md` | This project only | Commit to version control |
| **Plugin** | `<plugin>/skills/<name>/SKILL.md` | Where the plugin is enabled | Distribute the plugin |
| **Managed** | Managed settings | All users in the org | Deploy org-wide |

When the same name exists at multiple levels: **enterprise overrides personal overrides project.** Plugin skills are namespaced `plugin-name:skill-name`, so they never collide.

## Pattern 1 — Commit project skills

Put your team's commands in `.claude/skills/` and commit them. Every clone gets the same workflow for free. Treat the skill files like code — review changes to them in PRs.

> [!IMPORTANT]
> A project skill's `allowed-tools` only takes effect after a teammate accepts the workspace trust dialog. Review skills before trusting a repository — a skill can grant itself broad tool access or inject shell commands via `` !`cmd` ``.

## Pattern 2 — Standardize the review and ship steps

Agree on the bundled and custom commands everyone runs before review:

```text
/code-review        # find correctness bugs and cleanups
/security-review    # injection, auth, data exposure
/diff               # eyeball the change
```

Because these are real, shared commands, every PR gets the same bar.

## Pattern 3 — Onboard with `/team-onboarding`

`/team-onboarding` generates a guide from your Claude Code usage history — your sessions, commands, and MCP servers over the past 30 days — that a teammate can paste as a first message to get set up quickly.

## Pattern 4 — Keep skills fresh mid-session

`/reload-skills` re-scans skill and command directories so skills added or changed on disk become available without restarting. `/reload-plugins` does the same for plugins.

## Controlling visibility across a team

- `skillOverrides` in settings sets a skill to `on`, `name-only`, `user-invocable-only`, or `off` without editing its `SKILL.md` — useful for skills checked into a shared repo. The `/skills` menu writes it for you.
- `disable-model-invocation: true` blocks programmatic invocation entirely.

---

Sources: [Skills — where skills live](https://code.claude.com/docs/en/slash-commands#where-skills-live) and [share skills](https://code.claude.com/docs/en/slash-commands#share-skills)
