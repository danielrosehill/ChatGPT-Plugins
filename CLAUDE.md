# ChatGPT-Plugins: agent notes

Public catalogue (plugin marketplace) of Daniel Rosehill's ChatGPT-compatible plugins.
Created 2026-10-16 as a placeholder until OpenAI offers more formal ways to share plugins.
The README is for humans. This file is for agents.

- **This repo holds only the catalogue** (`.claude-plugin/marketplace.json`) and the README.
  Each plugin lives in its own public repo and is referenced with a `github` source. Edit
  plugins in their own repos, never here.
- **Every plugin here is a fork** of one or more Claude Code plugins from
  `danielrosehill/Claude-Code-Plugins`, adapted to ChatGPT's limits. To make a new one, use the
  project skill `.claude/skills/fork-for-chatgpt`.
- **Public.** Nothing household-specific or personal goes here. The household's private
  plugins are in `danielrosehill/Residence-Skills` (source) and
  `danielrosehill/Residence-Skills-Marketplace-ChatGPT` (what the household workspace imports).
- **Unverified:** whether ChatGPT's GitHub import resolves `github`-sourced entries.
  Vendored relative sources are proven (Residence-Skills-Marketplace-ChatGPT, 2026-10-16). Record
  the first import result in the README's maintainer notes.

| Plugin | Repo | Claude Code source(s) |
|---|---|---|
| `israel-research` | `danielrosehill/Israel-Research-Skills` | Claude-Israel-Agent-Skills-Plugin, Claude-Israel-Shopping-Plugin, Claude-Israel-Opening-Hours-Plugin, Aliexpress-Israel-Skills, Israel-Phonebook-Manager |
| `rtl-conformity` | `danielrosehill/RTL-Conformity-Skills` | Claude-RTL-Email, Claude-Hebrew-Correspondence-Plugin |
