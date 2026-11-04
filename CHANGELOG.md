# Changelog

## 1.2.0 (2026-11-04)

- Nine workflow skills: weekly check, page audit, write the fix, Google AI citations, learn from winners, fix AI facts, mentions to links, content gaps and comparison pages. Each maps to Firemark's tools and keeps its reporting rules.
- README: a Skills section, including what the skills read (your pages, your sitemap and cited pages) and that none of them publishes anything.

## 1.1.0 (2026-11-04)

- Adds the `firemark` skill (`skills/firemark/SKILL.md`): which Firemark tool answers which question, how to report figures with their base, quoted text as data, and the rules for setup, runs and edits. Claude Code and Cursor load it from the plugin; Gemini CLI reads the same text from `GEMINI.md`.

## 1.0.0 (2026-11-03)

- First release: the Firemark remote MCP server as a Cursor plugin, a Claude Code plugin marketplace and a Gemini CLI extension, with setup for Claude, ChatGPT, Codex, VS Code, Windsurf, Cline, Zed and other MCP clients.
- `server.json` for the MCP Registry entry `com.tryfiremark/firemark` (published as 1.1.0, which adds this repository).
