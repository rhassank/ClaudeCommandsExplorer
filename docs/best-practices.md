# ✅ Best Practices

> Patterns for writing skills (custom commands) that stay reliable. Drawn from Anthropic's skills documentation.

## 1. Write a description that triggers correctly

Claude decides when to auto-load a skill from its `description`. Include the keywords users would naturally say, and put the key use case first — the combined `description` + `when_to_use` is capped at 1,536 characters in the listing.

```yaml
description: Summarizes uncommitted changes and flags risks. Use when the user asks what changed, wants a commit message, or asks to review their diff.
```

## 2. Keep the body concise

Once invoked, a skill's content stays in context for the rest of the session, so every line is a recurring token cost. State what to do rather than narrating why. Keep `SKILL.md` under ~500 lines and move long reference material into [supporting files](authoring-skills.md#supporting-files) that load only when needed.

## 3. Gate side effects with `disable-model-invocation`

For anything with consequences — `/deploy`, `/commit`, `/send-slack-message` — set `disable-model-invocation: true` so only you trigger it. You don't want Claude deciding to deploy because the code looks ready.

## 4. Inject live context instead of guessing

A skill grounded in real data beats one that hopes Claude infers it. Use `` !`git diff HEAD` ``, `` !`gh pr diff` ``, or a `` ```! `` block so the prompt arrives with current state already inlined. See [Arguments & Injection](arguments-and-injection.md).

## 5. Scope tool access deliberately

`allowed-tools` lets a skill use specific tools without a permission prompt while active — it does not restrict other tools. For project skills checked into `.claude/skills/`, this takes effect only after you accept the workspace trust dialog. **Review project skills before trusting a repo**, since a skill can grant itself broad access.

```yaml
allowed-tools: Bash(git add *) Bash(git commit *) Bash(git status *)
```

## 6. Fork for isolation when it helps

Use `context: fork` with an `agent` (e.g. `Explore`) for research or analysis you want to run in a clean context. Only fork skills that contain an explicit task — pure reference content gives a forked subagent nothing to do.

## 7. Re-invoke after compaction if behavior drifts

Auto-compaction keeps recent skills within a token budget; older ones can be dropped. If a skill seems to stop influencing behavior, the content is usually still present and Claude is choosing other tools — strengthen the `description` and instructions, or re-invoke the skill.

## 8. Troubleshooting

| Symptom | Fix |
| :-- | :-- |
| Skill doesn't trigger | Add natural keywords to `description`; check it appears in "What skills are available?"; invoke directly with `/name`. |
| Skill triggers too often | Make the `description` more specific, or add `disable-model-invocation: true`. |
| Description cut short | Too many skills for the budget — trim text, set low-priority skills to `"name-only"`, or raise `skillListingBudgetFraction`. Run `/doctor` to inspect. |

## 9. Share with the right scope

Personal (`~/.claude/skills/`) for your own workflows, project (`.claude/skills/`, committed) for the team, plugins to distribute broadly, managed settings for org-wide. See [Team & Sharing](../examples/team-and-sharing.md).

---

Sources: [Skills documentation](https://code.claude.com/docs/en/slash-commands)
