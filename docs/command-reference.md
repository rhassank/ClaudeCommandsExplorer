# 📖 Command Reference

> Every slash command included in Claude Code, grouped by where it fits in your workflow. Sourced from the [official commands reference](https://code.claude.com/docs/en/commands).

[← Back to README](../README.md) · [🖥️ Interactive reference](../index.html) · [Bundled skills](bundled-skills.md) · [Build your own](authoring-skills.md)

> [!NOTE]
> Not every command appears for every user — availability depends on your platform, plan, and version. Type `/` in Claude Code to see what's available to you. A command is only recognized at the **start** of your message; text after it is passed as arguments.

**Legend:** `Built-in` = coded into the CLI · **`Skill`** = a bundled [skill](bundled-skills.md) Claude can also trigger automatically · **`Workflow`** = a bundled [dynamic workflow](bundled-workflows.md) that fans out across subagents. `<arg>` is required, `[arg]` optional.

## Setup & Config

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/init` | `Built-in` | Initialize the project with a starter CLAUDE.md guide. | — |
| `/memory` | `Built-in` | Edit CLAUDE.md memory files and manage auto-memory. | — |
| `/mcp` | `Built-in` | Manage MCP server connections and OAuth authentication. | — |
| `/agents` | `Built-in` | Manage subagent configurations. | — |
| `/permissions` | `Built-in` | Manage allow, ask, and deny rules for tool permissions. | `/allowed-tools` |
| `/add-dir <path>` | `Built-in` | Add a working directory for file access during the session. | — |
| `/hooks` | `Built-in` | View hook configurations for tool events. | — |
| `/plugin` | `Built-in` | Manage Claude Code plugins. | — |
| `/reload-plugins` | `Built-in` | Reload active plugins to apply changes without restarting. | — |
| `/reload-skills` | `Built-in` | Re-scan skill and command directories mid-session. | — |
| `/skills` | `Built-in` | List available skills; sort by token count, hide skills. | — |
| `/config` | `Built-in` | Open Settings to adjust theme, model, output style, and more. | `/settings` |
| `/statusline` | `Built-in` | Configure Claude Code's status line. | — |
| `/install-github-app` | `Built-in` | Set up the Claude GitHub Actions app for a repository. | — |
| `/install-slack-app` | `Built-in` | Install the Claude Slack app via OAuth. | — |
| `/web-setup` | `Built-in` | Connect GitHub to Claude Code on the web using your gh CLI. | — |
| `/terminal-setup` | `Built-in` | Configure terminal keybindings (Shift+Enter, etc.). | — |
| `/keybindings` | `Built-in` | Open or create your keybindings configuration file. | — |

## Context & Sessions

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/clear [name]` | `Built-in` | Start a new conversation with empty context. | `/reset, /new` |
| `/compact [instructions]` | `Built-in` | Summarize the conversation so far to free up context. | — |
| `/context [all]` | `Built-in` | Visualize current context usage as a colored grid. | — |
| `/btw <question>` | `Built-in` | Ask a quick side question without adding to the conversation. | — |
| `/resume [session]` | `Built-in` | Resume a conversation by ID or name, or open the picker. | `/continue` |
| `/branch [name]` | `Built-in` | Branch the current conversation at this point. | `/fork` |
| `/rewind` | `Built-in` | Rewind code and/or conversation to a previous checkpoint. | `/checkpoint, /undo` |
| `/rename [name]` | `Built-in` | Rename the current session. | — |
| `/export [filename]` | `Built-in` | Export the current conversation as plain text. | — |
| `/copy [N]` | `Built-in` | Copy the last assistant response to the clipboard. | — |
| `/recap` | `Built-in` | Generate a one-line summary of the current session. | — |
| `/goal [condition|clear]` | `Built-in` | Keep working across turns until a condition is met. | — |
| `/focus` | `Built-in` | Toggle a minimal focus view (fullscreen rendering only). | — |
| `/insights` | `Built-in` | Report on your sessions: areas, patterns, and friction points. | — |

## Model & Reasoning

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/model [model]` | `Built-in` | Switch the AI model and save it as your default. | — |
| `/effort [level|auto]` | `Built-in` | Set the model effort/reasoning level (low–max, ultracode). | — |
| `/fast [on|off]` | `Built-in` | Toggle fast mode. | — |
| `/plan [description]` | `Built-in` | Enter plan mode before a large change. | — |

## Review & Ship

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/diff` | `Built-in` | Open an interactive diff viewer of uncommitted and per-turn changes. | — |
| `/code-review [low|…|ultra] [--fix] [--comment] [target]` | **`Skill`** | Review the diff for correctness bugs and cleanups; --fix applies findings, ultra runs a cloud review. | — |
| `/review [PR]` | `Built-in` | Review a pull request locally in your current session. | — |
| `/security-review` | `Built-in` | Analyze pending changes for security vulnerabilities like injection, auth, and data exposure. | — |
| `/simplify [target]` | **`Skill`** | Cleanup-only review (reuse, simplification, efficiency) that applies fixes. <sub>(v2.1.154+)</sub> | — |
| `/run` | **`Skill`** | Launch and drive your app to see a change working in the running app. <sub>(v2.1.145+)</sub> | — |
| `/verify` | **`Skill`** | Build and run your app to confirm a change does what it should. <sub>(v2.1.145+)</sub> | — |
| `/run-skill-generator` | **`Skill`** | Teach /run and /verify how to build and launch your project. <sub>(v2.1.145+)</sub> | — |
| `/autofix-pr [prompt]` | `Built-in` | Spawn a web session that pushes fixes when CI fails or reviewers comment. | — |

## Parallel & Background

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/batch <instruction>` | **`Skill`** | Decompose a large change into 5–30 units and run each in its own git worktree subagent. | — |
| `/tasks` | `Built-in` | List and manage background tasks. | `/bashes` |
| `/background [prompt]` | `Built-in` | Detach the session to run as a background agent and free the terminal. | `/bg` |
| `/stop` | `Built-in` | Stop the current background session. | — |
| `/loop [interval] [prompt]` | **`Skill`** | Run a prompt repeatedly while the session stays open. | `/proactive` |
| `/workflows` | `Built-in` | Open the workflow progress view to watch, pause, or save runs. | — |
| `/ultraplan <prompt>` | `Built-in` | Draft a plan in an ultraplan session, review in browser, then execute. | — |
| `/ultrareview [PR]` | `Built-in` | Deep multi-agent cloud code review (preferred: /code-review ultra). | — |
| `/deep-research <question>` | **`Workflow`** | Fan out web searches, cross-check sources, and synthesize a cited report. | — |
| `/schedule [description]` | `Built-in` | Create, update, list, or run routines on Anthropic-managed cloud infra. | `/routines` |

## Skills & API

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/claude-api [migrate|managed-agents-onboard]` | **`Skill`** | Load Claude API reference for your language; migrate code to a newer model. | — |
| `/debug [description]` | **`Skill`** | Enable debug logging and troubleshoot issues from the session debug log. | — |
| `/fewer-permission-prompts` | **`Skill`** | Scan transcripts and add an allowlist to settings to reduce permission prompts. | — |

## Account & Status

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/login` | `Built-in` | Sign in to your Anthropic account. | — |
| `/logout` | `Built-in` | Sign out from your Anthropic account. | — |
| `/usage` | `Built-in` | Show session cost, plan usage limits, and activity stats. | `/cost, /stats` |
| `/status` | `Built-in` | Open Settings (Status tab): version, model, account, connectivity. | — |
| `/doctor` | `Built-in` | Diagnose and verify your Claude Code installation and settings. | — |
| `/feedback [report]` | `Built-in` | Submit feedback, report a bug, or share your conversation. | `/bug, /share` |
| `/usage-credits` | `Built-in` | Configure usage credits to keep working when you hit a limit. | — |
| `/upgrade` | `Built-in` | Open the upgrade page to switch to a higher plan tier. | — |
| `/release-notes` | `Built-in` | View the changelog in an interactive version picker. | — |
| `/heapdump` | `Built-in` | Write a heap snapshot for diagnosing high memory usage. | — |
| `/help` | `Built-in` | Show help and available commands. | — |
| `/exit` | `Built-in` | Exit the CLI (detaches an attached background session). | `/quit` |

## Remote & Devices

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/teleport` | `Built-in` | Pull a Claude Code on the web session into this terminal. | `/tp` |
| `/remote-control` | `Built-in` | Make this session available for remote control from claude.ai. | `/rc` |
| `/remote-env` | `Built-in` | Configure the default remote environment for web sessions. | — |
| `/desktop` | `Built-in` | Continue the current session in the Claude Code Desktop app. | `/app` |
| `/mobile` | `Built-in` | Show a QR code to download the Claude mobile app. | `/ios, /android` |
| `/chrome` | `Built-in` | Configure Claude in Chrome settings. | — |
| `/sandbox` | `Built-in` | Toggle sandbox mode (supported platforms only). | — |
| `/team-onboarding` | `Built-in` | Generate a team onboarding guide from your usage history. | — |

## Appearance & Misc

| Command | Type | Purpose | Aliases |
| :-- | :-- | :-- | :-- |
| `/theme` | `Built-in` | Change the color theme (light, dark, daltonized, custom). | — |
| `/color [color|default]` | `Built-in` | Set the prompt bar color for the current session. | — |
| `/tui [default|fullscreen]` | `Built-in` | Set the terminal UI renderer and relaunch into it. | — |
| `/scroll-speed` | `Built-in` | Adjust mouse wheel scroll speed (fullscreen only). | — |
| `/voice [hold|tap|off]` | `Built-in` | Toggle voice dictation, or enable a specific mode. | — |
| `/powerup` | `Built-in` | Discover features through quick interactive lessons. | — |
| `/radio` | `Built-in` | Open Claude FM lo-fi radio in your browser. | — |
| `/stickers` | `Built-in` | Order Claude Code stickers. | — |

---

<sub>Sourced from the official [Claude Code commands reference](https://code.claude.com/docs/en/commands) and [skills documentation](https://code.claude.com/docs/en/slash-commands). Verify against the live docs for your version.</sub>