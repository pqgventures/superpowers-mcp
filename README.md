# Superpowers MCP server

**Superpowers** ([superpowers.tools](https://superpowers.tools)) is the pay-per-call toolbox for AI agents: one key and one MCP server for business data, search, scraping, media and AI models, and you pay only when a call works.

This repository holds the setup for the hosted MCP server. There is nothing to install or run: your client connects to `https://superpowers.tools/mcp` (Streamable HTTP).

> Not to be confused with [obra/superpowers](https://github.com/obra/superpowers), the skills library for coding agents. This is the hosted tools marketplace by PQG Ventures.

## What your agent can do with it

- Find a tool by describing the job in plain words (`search_tools`), check its input and price (`inspect_tool`) and run it (`run_tool`).
- Run the same input across several providers and compare results, cost and speed side by side (`compare_providers`).
- Plan a multi-step job and see the cost before running it (`plan`), or run a ready recipe (`run_recipe`).
- Share results as a link anyone can open (`share`, `upload_file`).

The catalog includes AI models (GPT, Claude, Gemini and more through one key), web search, scraping to markdown, image, video and voice generation, SEC filings, sanctions screening, and Brazilian public data (CNPJ, CEP, FIPE, court cases, tenders, official gazettes). Browse it at [superpowers.tools/catalog](https://superpowers.tools/catalog).

Failed calls are free. New accounts get US$5 of credit. Many tools are free to call.

## Install in one step

Each option signs you in with your Superpowers account in the browser. There's no key to paste, and new accounts get US$5 of credit.

### Claude Code plugin

```
/plugin install superpowers --marketplace pqgventures/superpowers-mcp
```

(On Claude Code older than 2.1.275: `/plugin marketplace add pqgventures/superpowers-mcp`, then `/plugin install superpowers@superpowers`.) Then run `/mcp`, pick superpowers and sign in.

### Cursor plugin

Add this repository as a Cursor plugin, or put the server from [mcp.json](mcp.json) in `~/.cursor/mcp.json`.

### Agent Skill (Codex, Claude Code, any agent that reads SKILL.md)

```sh
npx skills add pqgventures/superpowers-mcp
```

The skill teaches your agent when to use Superpowers and how to call it over MCP, or over REST with a key.

### Any MCP client

Add `https://superpowers.tools/mcp/connect` as a remote MCP server and sign in. If your client only takes a key, use `https://superpowers.tools/mcp` with the key, as shown below.

## Get a key

Sign in at [superpowers.tools/login](https://superpowers.tools/login) (Google or an emailed code) and create an API key. An agent can also sign up by itself with `POST https://superpowers.tools/v1/signup`.

## Connect

### Claude Code

```sh
claude mcp add --transport http superpowers https://superpowers.tools/mcp \
  --header "Authorization: Bearer $SUPERPOWERS_KEY"
```

### Cursor (`~/.cursor/mcp.json`) and other clients that take a JSON config

```json
{
  "mcpServers": {
    "superpowers": {
      "url": "https://superpowers.tools/mcp",
      "headers": { "Authorization": "Bearer ${env:SUPERPOWERS_KEY}" }
    }
  }
}
```

### Codex

```sh
codex mcp add superpowers --url https://superpowers.tools/mcp \
  --bearer-token-env-var SUPERPOWERS_KEY
```

The server answers `initialize` and `tools/list` without a key, so you can see the tools before signing up; running a tool needs the key.

## Ready-made recipes

[pqgventures/superpowers-recipes](https://github.com/pqgventures/superpowers-recipes) has 29 agent skills with runnable scripts that use this server: check a Brazilian supplier from its CNPJ, watch competitor ads, make a video ad from a product page, build a verified lead list. In Claude Code: `/plugin marketplace add pqgventures/superpowers-recipes`.

## Tools

| Tool | What it does |
|---|---|
| `plan` | Free. Turns a goal in plain words into steps, tools and cost |
| `search_tools` | Finds tools by describing what you need |
| `inspect_tool` | Input schema, price and category of a tool |
| `run_tool` | Runs one tool; failed runs are free |
| `list_categories` / `compare_providers` | Categories with a shared format, and side-by-side runs across providers |
| `list_jobs` / `run_job` | Multi-step jobs |
| `list_recipes` / `get_recipe` / `run_recipe` / `publish_recipe` | Recipes (skills) for common jobs |
| `get_run` | Result or status of a run |
| `get_usage` / `get_balance` / `create_topup` / `charge_saved_card` | Usage and credit |
| `share` / `get_share` / `upload_file` | Shareable links and file hosting |
| `review_tool` / `get_reviews` / `send_feedback` | Ratings and feedback |
| `get_referral_link` | Invite link |

## Also available

- REST API and docs: [superpowers.tools/docs](https://superpowers.tools/docs)
- For agents: [llms.txt](https://superpowers.tools/llms.txt) and [skill.md](https://superpowers.tools/skill.md)
- Guides with real examples: [superpowers.tools/guides](https://superpowers.tools/guides)

## License

The contents of this repository are MIT licensed. The service itself is operated by PQG Ventures; see the [terms](https://superpowers.tools/terms).

