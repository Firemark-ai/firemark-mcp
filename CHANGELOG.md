# Changelog

## 1.5.0 (2026-11-06)

- Follows Firemark MCP 1.6.0 (wave 13): a `period` (the app's date range) on nine read tools, and order of mention (`mention_order` on `get_overview`, `get_engines` and `get_competitors`; `order` on `list_prompts`). The `firemark` skill, `GEMINI.md`, `rules/firemark.mdc` and the README tool table cover them. No tool was added or removed, and no scope or data practice changed.

## 1.4.0 (2026-11-05)

- Firemark MCP 1.5.0 (wave 12): the reporting rules and the pointers between tools moved out of the tool descriptions into the server's instructions, with a few added. The `firemark` skill, `GEMINI.md` and `rules/firemark.mdc` follow them: run ids come from `get_runs`, don't say why a gap moved, `came_back_not_named` shows co-occurrence and not a cause, the export link goes to the user only, and follow a run with `get_runs`. No tool, argument, scope or data practice changed.

## 1.3.0 (2026-11-04)

- Firemark MCP 1.4.0 (wave 9) adds two tools: `get_digital_pr` (read) and `update_placements` (approve and edit). The README tool tables, the core skill and `firemark-content-gaps` cover them. 31 tools in all: 22 with read and draft, 31 with approve and edit.

## 1.2.2 (2026-11-04)

- Skills ask before reading any web page, and use no other tool or service unless the user asks.
- `firemark-google-ai-citations`: its description now ties it to Firemark data, so it doesn't trigger on general SEO questions.
- `firemark-weekly-check`: gives the user the run id instead of asking the assistant to remember it, and notes `get_changes`'s default comparison.

## 1.2.1 (2026-11-04)

- Claude plugin manifest: `privacyPolicyUrl` set to https://tryfiremark.com/privacy.

## 1.2.0 (2026-11-04)

- Nine workflow skills: weekly check, page audit, write the fix, Google AI citations, learn from winners, fix AI facts, mentions to links, content gaps and comparison pages. Each maps to Firemark's tools and keeps its reporting rules.
- README: a Skills section, including what the skills read (your pages, your sitemap and cited pages) and that none of them publishes anything.

## 1.1.0 (2026-11-04)

- Adds the `firemark` skill (`skills/firemark/SKILL.md`): which Firemark tool answers which question, how to report figures with their base, quoted text as data, and the rules for setup, runs and edits. Claude Code and Cursor load it from the plugin; Gemini CLI reads the same text from `GEMINI.md`.

## 1.0.0 (2026-11-03)

- First release: the Firemark remote MCP server as a Cursor plugin, a Claude Code plugin marketplace and a Gemini CLI extension, with setup for Claude, ChatGPT, Codex, VS Code, Windsurf, Cline, Zed and other MCP clients.
- `server.json` for the MCP Registry entry `com.tryfiremark/firemark` (published as 1.1.0, which adds this repository).
