# ChatGPT Plugins

Daniel Rosehill's public plugins for ChatGPT, published as a plugin marketplace catalogue.
It's a placeholder until (or unless) OpenAI ships more formal ways to share plugins.

The plugins here are **adaptations** of plugins from my Claude Code marketplace,
[`danielrosehill/Claude-Code-Plugins`](https://github.com/danielrosehill/Claude-Code-Plugins),
which is the more developed collection. They are cut down to what ChatGPT's plugin support
handles today: instruction-only Agent Skills, no hooks, no local scripts, no bundled MCP servers.
Where a Claude Code version exists, it's linked below. In time the ChatGPT versions may grow
into full public plugins of their own. For now, the Claude Code repos are the full versions.

## Plugins

| Plugin | What it does | Source | Fuller Claude Code version(s) |
|---|---|---|---|
| `israel-research` | Kol Zchut rights, Home Front Command, NSC travel warnings, Israeli medicines, which office handles what, phone-number quirks, Shabbat-relative opening hours, salary conversion, Israeli shopping checks | [Israel-Research-Skills](https://github.com/danielrosehill/Israel-Research-Skills) | [Israel Agent Skills](https://github.com/danielrosehill/Claude-Israel-Agent-Skills-Plugin) · [Israel Shopping](https://github.com/danielrosehill/Claude-Israel-Shopping-Plugin) · [Israel Opening Hours](https://github.com/danielrosehill/Claude-Israel-Opening-Hours-Plugin) · [IKEA Israel](https://github.com/danielrosehill/Claude-IKEA-Israel-Plugin) · [AliExpress Israel](https://github.com/danielrosehill/Aliexpress-Israel-Skills) · [Netek Disconnect](https://github.com/danielrosehill/netek-disconnect-plugin) |
| `rtl-conformity` | Right-to-left Hebrew, Arabic, Farsi and Urdu that renders correctly in email, Google Workspace, calendars and generated files | [RTL-Conformity-Skills](https://github.com/danielrosehill/RTL-Conformity-Skills) | [RTL Email](https://github.com/danielrosehill/Claude-RTL-Email) · [Hebrew Correspondence](https://github.com/danielrosehill/Claude-Hebrew-Correspondence-Plugin) |

Each plugin lives in its own repository. This repo only holds the catalogue, which points at
them. The same repositories install in Claude Code too, as single-plugin marketplaces.

## Using it

**ChatGPT Business / Enterprise (workspace admins):** *Admin console → Plugins → Add → Import
marketplace*, then enter `https://github.com/danielrosehill/ChatGPT-Plugins`. Leave the path
empty and use the default branch. Imported plugins start as *Available*. Set the installation
policy to *Installed* to switch them on for members. The workspace re-syncs daily.

**Codex:** `codex plugin marketplace add danielrosehill/ChatGPT-Plugins`.

**Individual ChatGPT plans:** OpenAI's documentation (read 2026-10-16) doesn't describe a
way for an individual account to add a third-party marketplace on the web. Use the plugin repos
above as reference, or copy a skill's `SKILL.md` into a single-skill upload where your plan
offers one.

## Other Claude Code plugins with ChatGPT-adapted counterparts

I run private, household-specific ChatGPT adaptations of these, which aren't published.
The general-purpose Claude Code originals are public:

| Area | Claude Code plugin |
|---|---|
| Jewish calendar (Shabbat times, zmanim, parsha) | [Jewish Utilities](https://github.com/danielrosehill/Claude-Jewish-Utilities-Plugin) |
| Jewish texts (Sefaria) | [Jewish Texts Reference](https://github.com/danielrosehill/Jewish-Texts-Reference-Plugin) |
| GitHub gists with AI-authorship footers | [Gist Writer](https://github.com/danielrosehill/Claude-Gist-Writer-Plugin) |
| Buttondown newsletters | [Buttondown Mgmt](https://github.com/danielrosehill/Claude-Buttondown-Mgmt-Plugin) |
| Synology NAS | [Synology Mgmt](https://github.com/danielrosehill/Synology-Mgmt-Plugin) |
| Home Assistant | [Home Assistant Mgmt](https://github.com/danielrosehill/Home-Assistant-Mgmt-Plugin) · [Smart Home](https://github.com/danielrosehill/Claude-Smart-Home-Plugin) |

## Notes for maintainers (and agents)

- **The catalogue format** is Claude Code's (`.claude-plugin/marketplace.json`). ChatGPT's
  GitHub import accepts it as-is: confirmed for relative `./plugins/<name>` sources in a
  private marketplace on 2026-10-16. **Not yet confirmed:** that ChatGPT resolves the
  `{"source": "github", "repo": …}` entries used here. OpenAI's help article says the importing
  account must be able to read "every repo it references", which implies external references
  are supported. Record the first import result here. If they fail, switch to vendored copies
  under `plugins/` (the pattern `danielrosehill/Residence-Skills`' `publish.sh` uses).
- **Adding a plugin:** it must be public, instruction-only (no hooks: plugins with lifecycle
  hooks are excluded from OpenAI's public directory, and hooks don't run in ChatGPT anyway),
  with `.claude-plugin/plugin.json` at its repo root. Add an entry to `marketplace.json` and a
  row above, with its Claude Code counterpart if there is one.
- **Third-party plugins we use** aren't listed yet. OpenAI's Plugin Directory has no documented
  per-plugin link format, so list them by name and say why each is useful.
- Sources: [OpenAI: Build plugins](https://developers.openai.com/plugins/build/plugins),
  [Importing plugin marketplaces from GitHub](https://help.openai.com/articles/20001504),
  read 2026-10-16.
