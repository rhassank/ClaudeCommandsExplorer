<div align="center">

# ⚡ Claude Code Slash Commands

### A searchable reference for every slash command in Claude Code — and how to build your own

Built-in commands, bundled skills, and workflows, sourced from Anthropic's official documentation. Plus a complete guide to authoring custom commands as skills.

<br />

[![Made for Claude Code](https://img.shields.io/badge/Made%20for-Claude%20Code-ff6a3d?style=for-the-badge)](https://code.claude.com/docs/en/commands)
[![License: MIT](https://img.shields.io/badge/License-MIT-4fd1c5?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-57c98a?style=for-the-badge)](CONTRIBUTING.md)

![Commands](https://img.shields.io/badge/commands-86-ff6a3d)
![Bundled skills](https://img.shields.io/badge/bundled%20skills-10-57c98a)
![Source](https://img.shields.io/badge/source-official%20docs-60a5fa)

<br />

**[🖥️ Open the interactive reference →](index.html)** &nbsp;·&nbsp; **[📖 Command reference](docs/command-reference.md)** &nbsp;·&nbsp; **[🛠️ Build your own](docs/authoring-skills.md)**

</div>

---

> [!IMPORTANT]
> **Disclaimer:** This is an **independent, unofficial** community resource. It is **not affiliated with, endorsed by, or sponsored by Anthropic**. See the full [Disclaimer](#%EF%B8%8F-disclaimer) below. Everything here is sourced from the official [Claude Code documentation](#-official-documentation) — always verify against the live docs, since Claude Code changes often.

## 📑 Table of Contents

- [Disclaimer](#%EF%B8%8F-disclaimer)
- [Official documentation](#-official-documentation)
- [What slash commands are](#-what-slash-commands-are)
- [The three kinds of commands](#-the-three-kinds-of-commands)
- [Quick start](#-quick-start)
- [Browse the commands](#-browse-the-commands)
- [Build your own](#-build-your-own)
- [Documentation](#-documentation)
- [Repository structure](#-repository-structure)
- [Contributing](#-contributing)
- [License](#-license)

---

## ⚠️ Disclaimer

This repository is an **independent, unofficial** community reference. It is **not affiliated with, endorsed by, sponsored by, or maintained by Anthropic**. "Claude" and "Claude Code" are trademarks of Anthropic, used here only to describe the tool this reference documents.

- The content is compiled from Anthropic's **public documentation** and reflects a **snapshot in time**. Claude Code is updated frequently, so commands may be added, renamed, or removed after this was written.
- This reference may contain **errors, omissions, or outdated information**. It is provided "as is," without warranty of any kind (see [LICENSE](LICENSE)).
- **The official Anthropic documentation is always the authoritative source.** When in doubt, follow the [official docs](#-official-documentation) and type `/` in your own Claude Code session to see what's actually available to you.

If you represent Anthropic and would like any content changed or removed, please [open an issue](CONTRIBUTING.md).

---

## 🔗 Official Documentation

Always verify against — and prefer — the official source:

| Topic | Official Anthropic documentation |
| :-- | :-- |
| 📋 All commands (built-in, skills, workflows) | https://code.claude.com/docs/en/commands |
| 🧩 Skills & custom commands | https://code.claude.com/docs/en/slash-commands |
| 🔀 Workflows | https://code.claude.com/docs/en/workflows |
| 🧠 Subagents | https://code.claude.com/docs/en/sub-agents |
| 🔌 Plugins | https://code.claude.com/docs/en/plugins |
| 📚 Claude Code docs home | https://code.claude.com/docs |

> [!NOTE]
> Every documentation page in this repo also links back to its specific official source at the bottom.

---

## 🤔 What slash commands are

In Claude Code, slash commands control the session from inside it — switch models, manage permissions, clear context, review a diff, run a workflow. Type `/` to see what's available, or `/` plus letters to filter.

Two rules: a command is only recognized at the **start** of your message, and text after the command name is passed to it as **arguments**.

```text
/review 1234
```

`/review` is the command; `1234` is the argument.

---

## 🧩 The three kinds of commands

| Kind | What it is | Examples |
| :-- | :-- | :-- |
| **Built-in** | Behavior coded into the CLI | `/init` · `/clear` · `/compact` · `/model` · `/diff` · `/review` · `/security-review` |
| **Bundled skill** | A prompt handed to Claude that it can also trigger automatically | `/code-review` · `/debug` · `/batch` · `/loop` · `/run` · `/verify` · `/simplify` |
| **Bundled workflow** | A dynamic workflow that fans work across subagents | `/deep-research` |

And the fourth, most powerful option: **commands you write yourself** as [skills](docs/authoring-skills.md).

---

## 🚀 Quick start

1. **Browse** — open [`index.html`](index.html) for the searchable, filterable reference (press <kbd>/</kbd> to search, filter by type or workflow group).
2. **Look it up** — or read the [Command Reference](docs/command-reference.md) grouped by workflow phase.
3. **Build your own** — turn a repeated prompt into a `/command` with the [authoring guide](docs/authoring-skills.md).

```text
# In Claude Code, try a real bundled skill:
/code-review --fix
```

---

## 🗂️ Browse the commands

<div align="center">

| Section | What's inside | Open |
| :-- | :-- | :-- |
| 🖥️ **Interactive reference** | All 86 commands, searchable & filterable | [→](index.html) |
| 📖 **Command reference** | The full table, grouped by workflow phase | [→](docs/command-reference.md) |
| 🧩 **Bundled skills** | `/code-review`, `/debug`, `/batch`, `/run`… | [→](docs/bundled-skills.md) |
| 🔀 **Bundled workflows** | `/deep-research` and the workflow view | [→](docs/bundled-workflows.md) |

</div>

> [!TIP]
> In the interactive site, the **Skill** and **Workflow** badges mark the prompt-based commands; everything else is built into the CLI.

---

## 🛠️ Build your own

Custom commands **are skills**. Create a `SKILL.md` and its directory name becomes the command:

```yaml
# ~/.claude/skills/summarize-changes/SKILL.md  ->  /summarize-changes
---
description: Summarize uncommitted changes and flag risks.
---

## Current changes
!`git diff HEAD`

## Instructions
Summarize the changes above, then list any risks.
```

The `` !`git diff HEAD` `` line injects the live diff before Claude reads the prompt; `$ARGUMENTS` (and `$0`, `$1`, named args) capture input. Full details:

- [Authoring Skills](docs/authoring-skills.md) — the complete model, frontmatter, scopes
- [Arguments & Injection](docs/arguments-and-injection.md) — `$ARGUMENTS` and `` !`cmd` ``
- [Custom Skill Examples](examples/custom-skill-examples.md) — copy-ready skills
- [SKILL.md template](templates/skill-template.md) · [command-file template](templates/command-file-template.md)

---

## 📖 Documentation

| Guide | What you'll learn |
| :-- | :-- |
| [Getting Started](docs/getting-started.md) | How commands work; the three kinds |
| [Command Reference](docs/command-reference.md) | Every command, grouped by workflow |
| [Bundled Skills](docs/bundled-skills.md) | The prompt-based commands that ship with Claude Code |
| [Bundled Workflows](docs/bundled-workflows.md) | `/deep-research` and managing background work |
| [Authoring Skills](docs/authoring-skills.md) | Build and share your own commands |
| [Arguments & Injection](docs/arguments-and-injection.md) | Pass input and inject live data |
| [Best Practices](docs/best-practices.md) | Write skills that stay reliable |

---

## 🧱 Repository structure

```text
claude-code-slash-commands/
├── index.html                      # Searchable interactive reference
├── README.md
├── CONTRIBUTING.md
├── LICENSE
├── docs/
│   ├── getting-started.md
│   ├── command-reference.md        # full official table (generated)
│   ├── bundled-skills.md
│   ├── bundled-workflows.md
│   ├── authoring-skills.md
│   ├── arguments-and-injection.md
│   └── best-practices.md
├── examples/
│   ├── custom-skill-examples.md    # real, copy-ready SKILL.md files
│   └── team-and-sharing.md
├── templates/
│   ├── skill-template.md
│   └── command-file-template.md
└── assets/
    ├── images/
    └── badges/
```

---

## 🤝 Contributing

Found a command that changed, or want to add a custom-skill example? See [CONTRIBUTING.md](CONTRIBUTING.md). The golden rule: **everything must match the official docs** — cite the source for any command claim.

---

## 📄 License

Licensed under the **[MIT License](LICENSE)** — use it, fork it, share it. The software and content are provided "as is," without warranty of any kind, as stated in the license and the [Disclaimer](#%EF%B8%8F-disclaimer) above.

The MIT license covers this repository's own content only. It does not grant any rights to Anthropic's trademarks or documentation; "Claude" and "Claude Code" remain trademarks of Anthropic.

<div align="center">
<br />
<sub>Community reference. Not affiliated with Anthropic. "Claude" and "Claude Code" are products of Anthropic. Command data sourced from <a href="https://code.claude.com/docs/en/commands">code.claude.com/docs</a>.</sub>
</div>
