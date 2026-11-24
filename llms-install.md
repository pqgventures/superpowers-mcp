# Installing the Superpowers MCP server (for agents such as Cline)

Superpowers is a hosted remote MCP server. There is nothing to clone, build or run locally.

- URL: `https://superpowers.tools/mcp`
- Transport: Streamable HTTP
- Auth: `Authorization: Bearer <key>` header

Do not run `npx skills add` for this task: that installs a skill file, not the MCP server.

## 1. Get a key

If the user has no key yet, ask them to sign in at https://superpowers.tools/login and create one under Keys (new accounts get US$5 of credit). An agent can also create an account and key itself:

```sh
curl -s https://superpowers.tools/v1/signup -H 'content-type: application/json' -d '{"email":"USER_EMAIL"}'
```

Never write the key into a file inside the user's project.

## 2. Add the server

### Cline CLI

```sh
cline mcp add superpowers https://superpowers.tools/mcp --transport streamableHttp --header "Authorization: Bearer $SUPERPOWERS_KEY" --yes
```

### Cline in VS Code (`cline_mcp_settings.json`)

```json
{
  "mcpServers": {
    "superpowers": {
      "type": "streamableHttp",
      "url": "https://superpowers.tools/mcp",
      "headers": { "Authorization": "Bearer YOUR_SUPERPOWERS_KEY" },
      "disabled": false
    }
  }
}
```

Clients that support MCP OAuth can use `https://superpowers.tools/mcp/connect` with no key; the user signs in in the browser.

## 3. Check it works

Call the `get_balance` tool (free). It returns the account's credit in US dollars. Then try a real job, for example `generate_image` with `{"prompt": "a red bicycle on a beach"}`.
