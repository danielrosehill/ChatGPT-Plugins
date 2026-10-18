---
name: fork-for-chatgpt
description: Fork one of Daniel's Claude Code plugins into a public, ChatGPT-compatible plugin repo and list it in the danielrosehill/ChatGPT-Plugins catalogue. Use when asked to "make a ChatGPT version of <plugin>", "fork <plugin> for ChatGPT", "add <plugin> to the ChatGPT marketplace", or to adapt skills from danielrosehill/Claude-Code-Plugins for ChatGPT.
---

# Fork a Claude Code plugin for ChatGPT

> Since 2026-10-18 the general version of this procedure, covering private and public routes, a portability scanner and the verified import facts, is the `chatgpt-porting` plugin (`danielrosehill/Claude-ChatGPT-Porting-Plugin`, private marketplace). Prefer `chatgpt-porting:port-plugin-to-chatgpt`. This project skill stays as the Route B quick reference.

The full versions of Daniel's plugins live in the Claude Code marketplace
[`danielrosehill/Claude-Code-Plugins`](https://github.com/danielrosehill/Claude-Code-Plugins)
(local clone: `~/repos/github/ai-agents-and-prompts/ai-claude-marketplaces/Claude-Code-Plugins`).
A ChatGPT fork is a **new public repo** holding a cut-down, instruction-only version of
one or more of those plugins. This repo's catalogue then points at it.

The worked examples are
[`Israel-Research-Skills`](https://github.com/danielrosehill/Israel-Research-Skills)
(12 skills merged from 5 Claude plugins) and
[`RTL-Conformity-Skills`](https://github.com/danielrosehill/RTL-Conformity-Skills).
Copy their layout.

## 1. Pick the source and decide the scope

- Find the source plugin(s) in the Claude marketplace's `.claude-plugin/marketplace.json`.
  Each entry's `source.repo` is the plugin repo. Clone it into the scratchpad. Don't edit the
  original.
- One ChatGPT plugin can merge skills from several Claude plugins on one subject, as
  `israel-research` does. Prefer that over many tiny plugins.
- If a public ChatGPT fork on the subject already exists, **add to it** rather than
  starting a parallel repo.

## 2. Adapt to what ChatGPT can run

ChatGPT plugins (as of 2026-10-16) run **Agent Skills** and remote MCP servers only. For each
component of the source plugin:

| Source has | In the ChatGPT fork |
|---|---|
| `skills/<name>/SKILL.md` | Keep. Frontmatter `name` = folder name, and `description` says what it does and when to use it |
| Slash commands (`commands/`) | Turn the useful ones into skills, or drop them |
| Subagents (`agents/`) | Fold the instructions into a skill, or drop them |
| Hooks | **Drop.** They don't run in ChatGPT, and they make a plugin ineligible for OpenAI's public directory |
| Scripts the skill shells out to | Rewrite as instructions the model can follow with web search/fetch or code execution, or drop the skill |
| `.mcp.json` (local/stdio servers) | Drop. A `.mcp.json` labels the plugin *Desktop only*. A **remote** streamable-HTTP server can go in a root `mcp.json`, with auth under `mcpServers.<name>.extensions["com.openai"].auth`. But it is ignored unless a root `plugin.json` exists too, and even then chatgpt.com offers it only in the desktop app (verified 2026-10-17). Keep instruction-only skills in a plugin with no MCP declaration |
| Claude-specific tool names (`Bash`, `WebFetch`, `mcp__…`, Claude in Chrome) | Describe the capability instead ("search the web", "your Google Drive tool") |
| Machine-specific paths, personal data, household facts | Remove. These repos are public |

Keep bulky reference data in the skill's own `references/` folder. Date any fact that goes
stale (prices, thresholds, endpoints) and tell the agent to re-check it. Stay inside the safe
envelope: ≤ 500 files, ≤ 25 MB per file, ≤ 50 MB total.

## 3. Create the public repo

- **Name:** `<Subject>-Skills`, e.g. `Israel-Research-Skills`. Create it with
  `gh repo create danielrosehill/<Name> --public`. Daniel asking for a ChatGPT fork is the
  approval to publish it, but say in one line that it will be public. Local clone goes in the
  `~/repos/github/` topic folder that fits (see `~/repos/github/README.md`).
- **Layout:**
  - `.claude-plugin/plugin.json`: `name`, `version` (start `0.1.0`), `description` ending
    "Instruction-only; works in Claude and ChatGPT.", `author`, `repository`,
    `license: "MIT"`, `keywords`, and `extensions["com.openai"].interface` (`displayName`,
    `shortDescription`, `developerName: "Daniel Rosehill"`, `category`, `capabilities`, two
    `defaultPrompt` examples). Copy the shape from Israel-Research-Skills.
  - `.claude-plugin/marketplace.json`: a single-plugin marketplace with `"source": "./"`, so
    the repo also installs in Claude Code on its own.
  - `skills/<name>/SKILL.md` (+ `references/`).
  - `README.md` with a skills table that has a **"Derived from"** column naming the source
    skill and Claude plugin for each skill.
  - `LICENSE` (MIT) and a short `CLAUDE.md`: what the repo is, that it's the source of truth
    for the ChatGPT fork, and the source plugin(s) it was cut from.
- Commit and push.

## 4. List it in this catalogue

In `danielrosehill/ChatGPT-Plugins`:

1. Add an entry to `.claude-plugin/marketplace.json`:
   `{"name": …, "source": {"source": "github", "repo": "danielrosehill/<Name>"}, "description": …, "category": …}`.
   Validate with `jq .`.
2. Add a row to the README's **Plugins** table, with the source repo and links to the fuller
   Claude Code version(s). If the subject was in "Other Claude Code plugins with
   ChatGPT-adapted counterparts", move it out of that table.
3. Commit and push. Workspaces that imported the catalogue pick it up at their daily sync.

## 5. Optional: the household workspace

To give the fork to Daniel and Hannah's ChatGPT Business workspace too, add it to the
`EXTERNAL` map in `Residence-Skills/skills/publish-to-chatgpt/scripts/publish.sh`
(`[<plugin-name>]="danielrosehill/<Name>"`). Commit, push, and run `publish.sh`. Then
list it in `Residence-Skills-Marketplace-ChatGPT/CLAUDE.md`. Do this only if Daniel asks. The
new plugin arrives in the workspace as *Available* until an admin sets it to *Installed*.

## Report

Give the new repo URL, which skills were kept, converted or dropped (and why), and whether it
was added to the household workspace.
