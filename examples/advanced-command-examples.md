# 🚀 Advanced Command Examples

> Practical examples for the more powerful built-in commands and bundled skills, with context on when to reach for each one.

All examples use documented commands. See [Command Reference](../docs/command-reference.md) for the full list and [Authoring Skills](../docs/authoring-skills.md) to build your own.

---

## `/code-review`

### Quick pre-commit check

```text
/code-review
```

**Use when:** You want a fast pass over your uncommitted diff before pushing. Runs a correctness and cleanup review, reports findings, does not modify files.

**Best for:** Small to medium changes, catching obvious bugs before they reach CI.

### Auto-fix on the way to PR

```text
/code-review --fix
```

**Use when:** You want Claude to apply the review findings to your working tree immediately. Review plus automated fix in one step.

**Avoid when:** You are in the middle of a rebase or have uncommitted stash you don't want touched.

### Post inline PR comments

```text
/code-review ultra --comment
```

**Use when:** You are reviewing a PR and want findings posted as inline GitHub comments. `ultra` runs a deeper cloud review; `--comment` posts the results to the PR.

**Requires:** A GitHub repo with the Claude GitHub App installed (`/install-github-app`).

### Review a specific file or folder

```text
/code-review src/auth/
```

**Use when:** You only care about a specific part of the diff — useful in large PRs.

---

## `/batch`

### Migrate all API calls across a large codebase

```text
/batch migrate every fetch() call in src/ to use our new apiClient wrapper
```

**Use when:** You have a mechanical change that touches many files independently. `batch` researches the codebase, decomposes the work into parallel units, shows you the plan, then spawns one background subagent per unit in its own git worktree.

**Best for:** Renaming, migrations, mass refactors, adding logging/metrics to every handler.

**Avoid when:** The change has tight cross-file dependencies (e.g., a database schema migration that must run in order). Use `/plan` + manual implementation there.

### Add a standard copyright header to every source file

```text
/batch add the standard copyright header to every .ts and .tsx file in src/ that is missing it
```

---

## `/debug`

### Investigate a reproduction you can describe

```text
/debug the payment webhook silently drops events when the payload exceeds 8 KB
```

**Use when:** You know the symptom but not the cause. `debug` enables session debug logging, reads it, and works through the problem step by step.

### Start from an error message

```text
/debug TypeError: Cannot read properties of undefined (reading 'userId') at middleware/auth.ts:34
```

**Best for:** Stack traces, flaky tests, "works on my machine" issues.

---

## `/loop`

### Continuous watch during active development

```text
/loop 2m run the test suite and summarize any new failures
```

**Use when:** You want Claude to poll a condition while you work on something else. Here: run tests every 2 minutes and report failures.

### Background maintenance check

```text
/loop check for new GitHub issues labeled "bug" and triage them into the backlog
```

**Use when:** You want a proactive agent running alongside your session. Omit the interval and Claude self-paces based on the task.

> [!TIP]
> Use `/background` first to detach the session, then `/loop` so the agent runs independently without blocking your terminal.

---

## `/deep-research`

### Technical architecture comparison

```text
/deep-research compare FastAPI, NestJS, and Laravel for a multi-tenant SaaS backend: developer experience, performance, ecosystem maturity, and hosting options
```

**Use when:** You need a well-sourced answer to a complex question with multiple angles. `deep-research` fans out web searches, cross-checks sources, and synthesizes a cited report.

**Best for:** Architecture decisions, evaluating libraries/frameworks, competitive analysis, due diligence.

**Expect:** A longer result — typically several minutes, then a detailed cited report.

### Investigate an unfamiliar codebase

```text
/deep-research how does authentication work in this repo? trace the flow from HTTP request to session creation
```

---

## `/ultraplan`

### Plan a large refactor before touching code

```text
/ultraplan extract the billing module into a standalone microservice: identify all dependencies, define the API contract, and propose a phased migration
```

**Use when:** The scope is large enough that diving in without a plan risks rework. `ultraplan` opens an interactive planning session in the browser where you can review and edit the plan before Claude executes it.

---

## `/security-review`

### Before merging an auth or payment change

```text
/security-review
```

**Use when:** You are about to merge changes to authentication, authorization, payment flows, or anything that handles user data or secrets. Analyzes uncommitted changes for injection, auth bypass, and data exposure risks.

> [!IMPORTANT]
> `security-review` covers common vulnerability patterns but is not a substitute for a professional security audit on high-stakes changes.

---

## Combining commands

### Full review-and-ship workflow

```text
/code-review         # find issues
/code-review --fix   # apply fixes
/verify              # confirm the app still runs
/diff                # inspect final diff
```

### Parallel feature work

```text
/batch implement the five endpoints described in docs/api-spec.md, one subagent per endpoint
```

Then while that runs:

```text
/loop 5m check whether the batch agents have opened their PRs and summarize progress
```

---

Sources: [Commands reference](https://code.claude.com/docs/en/commands) · [Skills documentation](https://code.claude.com/docs/en/slash-commands)
