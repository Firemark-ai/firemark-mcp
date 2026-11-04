<p align="center"><img src="assets/logo.png" alt="Firemark" width="96" height="96"></p>

# Firemark MCP server

**Firemark is the AI visibility tracker built to be run from your AI assistant.** Its MCP server is on every plan from $29, so your assistant can read the brand's rank, competitors, cited sources and ChatGPT fan-out queries, set up the prompt set by interview, and, with your permission, approve and edit your brands.

Firemark asks a fixed set of buyer questions to ChatGPT, Perplexity, Gemini, Google AI Overviews and Google AI Mode on a schedule, and shows which brands each answer names and which sites it cites.

This repository connects Firemark to Cursor, Claude, Claude Code, ChatGPT, Gemini CLI, Codex, VS Code, Windsurf, Cline, Zed and other MCP clients. It is a Cursor plugin, a Claude Code plugin marketplace and a Gemini CLI extension in one. Your assistant can then read your results, find where competitors are named and you are not, and draft prompt and competitor changes for you to confirm.

```
https://app.tryfiremark.com/mcp
```

That is the only official address. It is a remote MCP server (Streamable HTTP). You sign in with your Firemark account (OAuth 2.1 with PKCE). There is no API key, and nothing runs on your machine.

You need a Firemark account with at least one brand: [tryfiremark.com](https://tryfiremark.com). The MCP server is included on every plan, from $29 a month.

## Connect

### Cursor

Install the Firemark plugin from the Cursor Marketplace, or add the server yourself:

1. Open **Customize** in Cursor and choose **New MCP Server**. Cursor opens `mcp.json`.
2. Add Firemark and save:
   ```json
   {
     "mcpServers": {
       "firemark": {
         "url": "https://app.tryfiremark.com/mcp"
       }
     }
   }
   ```
3. Click **Connect** beside firemark, sign in to Firemark and choose **Allow**.

**Cursor CLI:** put the same entry in `~/.cursor/mcp.json`, then run:

```sh
agent mcp login firemark
```

The CLI keeps the sign-in per folder, so run `agent` from the folder you signed in from.

### Claude (claude.ai and Claude Desktop)

1. Open **Customize**, then **Connectors**.
2. Click **+ Add**, then **Add custom connector**. Name it Firemark and paste the server address.
3. Click **Connect**, sign in to Firemark and choose **Allow**.

On Team and Enterprise plans, an owner adds the connector first under Organization settings.

### Claude Code

Install the Firemark plugin from this repository:

```
/plugin install firemark --marketplace Firemark-ai/firemark-mcp
```

On Claude Code versions without that form, run `/plugin marketplace add Firemark-ai/firemark-mcp`, then `/plugin install firemark@firemark`. Or add the server alone:

```sh
claude mcp add --transport http firemark https://app.tryfiremark.com/mcp
```

Then run `/mcp` in Claude Code, choose firemark and sign in.

### ChatGPT

1. On chatgpt.com, open **Plugins**, click **+**, then **Add custom MCP server**.
2. Name it Firemark, paste the server address under Connection and choose **OAuth**.
3. Create it as a plugin, then install it: sign in to Firemark and choose **Allow**.

ChatGPT adds custom MCP servers on the web only. On Business, Enterprise and Edu plans, a workspace admin has to allow plugins with MCP servers first.

### VS Code

Add to `.vscode/mcp.json`, then start the server from the file and sign in:

```json
{
  "servers": {
    "firemark": {
      "type": "http",
      "url": "https://app.tryfiremark.com/mcp"
    }
  }
}
```

### Gemini CLI

```sh
gemini extensions install https://github.com/Firemark-ai/firemark-mcp
```

Then start Gemini CLI and run `/mcp auth firemark` to sign in.

### OpenAI Codex CLI

```sh
codex mcp add firemark --url https://app.tryfiremark.com/mcp
codex mcp login firemark
```

Or add it to `~/.codex/config.toml`:

```toml
[mcp_servers.firemark]
url = "https://app.tryfiremark.com/mcp"
```

### Windsurf

Add to Windsurf's `mcp_config.json` (Windsurf Settings, Cascade, MCP Servers, View raw config) and refresh. Windsurf opens the sign-in on first use.

```json
{
  "mcpServers": {
    "firemark": {
      "serverUrl": "https://app.tryfiremark.com/mcp"
    }
  }
}
```

### Cline

Add to `cline_mcp_settings.json` (MCP Servers, then Configure):

```json
{
  "mcpServers": {
    "firemark": {
      "type": "streamableHttp",
      "url": "https://app.tryfiremark.com/mcp"
    }
  }
}
```

### Zed

Add to Zed's `settings.json`. Zed asks you to sign in the first time it connects.

```json
{
  "context_servers": {
    "firemark": {
      "url": "https://app.tryfiremark.com/mcp"
    }
  }
}
```

### Other MCP clients

Add `https://app.tryfiremark.com/mcp` as a remote (Streamable HTTP) MCP server with OAuth. The client opens Firemark's sign-in, then a consent page that asks what it may do.

## Permissions

The consent page shows three permissions. You can revoke any connection at once on the [Connect the MCP](https://app.tryfiremark.com/account/mcp) page in the app.

| Permission (as the consent page names it) | What it allows | On the consent page |
|---|---|---|
| Read your results | The counts, verdicts and short snippets your screens show, the pages answers cite, and the full text of one answer at a time, on request | Granted when you choose Allow |
| Draft, propose and start a first run | The setup interview and a saved draft, proposals to add or remove prompts and competitors, a confirmed brand's first run, or one retry after a failed run. A draft or proposal takes effect only once a member confirms it. | Granted when you choose Allow |
| Approve and edit your brands | Approve or discard drafts and proposals, and edit a brand's prompts, competitors, groups, schedule and emails | Only if you tick its box (unticked to start) |

No permission lets it start any other run, remove a brand, change a plan, see billing, or manage members or API keys.

## Tools

**Read your results**

| Tool | What it returns |
|---|---|
| `list_brands` | The brands you can read, across your accounts, with each brand's state |
| `get_overview` | The headline of a brand's latest run: answers naming the brand out of answers collected |
| `get_engines` | Each engine's answers naming the brand, out of its base |
| `get_competitors` | Each tracked competitor against the brand, by engine, with rank and sentiment |
| `get_sources` | The sites and pages the answers cite, split by whether they name the brand or a competitor |
| `list_prompts` | The brand's prompts with one verdict per engine (named and linked, named, linked, absent) |
| `get_prompt` | One prompt in detail: each engine's verdict, position, sentiment, competitors and cited URLs |
| `get_answer` | One engine's answer to one prompt, word for word |
| `get_runs` | The run log: dates, status, coverage by engine and answers collected |
| `get_gaps` | Where the brand loses: answers that name a competitor and not the brand, ordered for action |
| `get_source_gaps` | The sites cited when a competitor is named and the brand is not |
| `get_fanouts` | ChatGPT's fan-out queries, and whether the brand's own pages came back to them |
| `get_changes` | What changed since a run, in one digest |
| `get_whats_new` | Product news: what changed in Firemark |
| `get_export_link` | A link to download a brand's CSV files |

**Draft, propose and start a first run**

| Tool | What it does |
|---|---|
| `interview_start` | Starts or resumes a five-step interview that ends in a draft prompt basket |
| `interview_submit_step` | Stores the answers to one step and returns the next |
| `interview_get_basket` | Reads the proposed prompts |
| `interview_save_draft` | Saves the draft and returns the link where a member confirms it |
| `propose_changes` | Proposes prompts and competitors to add or remove on a running brand |
| `start_run` | Starts a confirmed brand's first run, or one retry after a failed run |

**Approve and edit your brands** (only if you tick it on the consent page)

| Tool | What it does |
|---|---|
| `get_setup` | Reads a brand's setup as it stands now |
| `review_draft` | Confirms or discards a new brand's draft |
| `review_proposal` | Approves or discards a brand's open proposal |
| `update_brand` | Edits a brand's details, schedule or emails |
| `update_competitors` | Adds, removes or edits tracked competitors |
| `update_prompts` | Adds, removes or edits prompts |
| `manage_groups` | Creates, renames or deletes prompt groups |
| `set_site_type` | Sets the type of a cited site |

## Example questions

- Which brands do I track?
- How often does ChatGPT name us, out of how many answers?
- Which competitors are named where we are not?
- Which sites do the answers cite when a competitor is named and we are not?
- Which fan-out queries does ChatGPT run where none of our pages come back?
- What changed since last week's run?
- Help me set up tracking for a new brand.

## Security

- Sign-in is OAuth 2.1 with PKCE. Your assistant never sees your password.
- Access tokens last one hour. Refresh tokens last 30 days and rotate.
- Every call is checked against your account membership. A brand you are not a member of answers as if it does not exist.
- Answer text and other quoted content come back marked as data, not instructions.
- Use only `https://app.tryfiremark.com/mcp`. Firemark does not publish any other server address or package.

Report a security issue: see [SECURITY.md](SECURITY.md).

## Links

- [Firemark MCP server](https://tryfiremark.com/mcp)
- [How Firemark measures](https://tryfiremark.com/method)
- [Firemark API](https://tryfiremark.com/docs/api)
- [Pricing](https://tryfiremark.com/pricing)
- [Privacy](https://tryfiremark.com/privacy) · [Terms](https://tryfiremark.com/terms)

## License

[MIT](LICENSE)
