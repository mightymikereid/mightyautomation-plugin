# Mighty Automation — MCP Connector

The official [Mighty Automation](https://mightyautomation.com) MCP server and
plugin. Connect your AI client — Grok Bot, Cursor, Claude, ChatGPT, VS Code,
or any MCP-compatible agent — to your Mighty Automation marketing workspace
so it can create contacts, manage your pipeline, send email, book
appointments, and drive automations for you.

- **Endpoint:** `https://mcp.mightyautomation.com/api/mcp` (Streamable HTTP, stateless)
- **Auth:** `Authorization: Bearer mva_mcp_…` — your MCP API key

## Install (Cursor / Agent Plugins)

1. In your Mighty Automation dashboard, open **Integrations → Zapier & other
   tools → AI connectors (MCP) → Generate key**. Copy the `mva_mcp_…` key —
   it is shown once.
2. Add this plugin to your client. In Cursor, install the `mightyautomation`
   plugin (or add `mcp.json` from this repo to your MCP config).
3. When prompted, set the `MA_MCP_KEY` variable to your key. Never commit a
   real key anywhere — the `${MA_MCP_KEY}` placeholder stays a placeholder.
4. Ask your agent to call `whoami` — if it answers with your workspace, you
   are connected.

### Manual MCP config (any client)

```json
{
  "mcpServers": {
    "mightyautomation": {
      "url": "https://mcp.mightyautomation.com/api/mcp",
      "headers": { "Authorization": "Bearer mva_mcp_YOUR_KEY" }
    }
  }
}
```

## Tools (21)

| Tool | What it does |
| --- | --- |
| `whoami` | Identify the workspace your key belongs to |
| `get_credit_balance` | Current credit balance, lifetime totals, recent ledger entries |
| `upsert_contact` | Create or update a CRM contact by email |
| `update_contact` | Update fields on an existing contact |
| `find_contact` | Look up a contact by email |
| `get_contact` | Full contact record with notes, tags and activity |
| `list_contacts` | Page through contacts (filters, search, dates) |
| `search_leads` | Search leads by lifecycle stage, query, date |
| `add_tag` | Add tags to a contact |
| `add_note` | Attach a note to a contact |
| `send_email` | Send a transactional email to a contact |
| `list_pipeline_stages` | List the workspace's pipeline stages |
| `list_appointments` | List scheduled appointments |
| `create_booking_link` | Create a shareable booking link |
| `list_automations` | List workspace automations |
| `enroll_automation` | Enroll a contact in an automation |
| `import_file` | Import a file (image/*, audio/*, video/*, PDF; max 10 MB) |
| `list_events` | Read the workspace event feed |
| `create_hook` | Subscribe a webhook to a workspace event |
| `list_hooks` | List active webhook subscriptions |
| `delete_hook` | Remove a webhook subscription (idempotent) |

## Pricing

- Requires a paid **Mighty Automation plan** — $97/mo including
  $100 in credits (see [mightyautomation.com](https://mightyautomation.com)).
- MCP calls are metered against your workspace credits at **$0.005 per
  successful tool call**. Failed calls (validation errors, not found) are
  free, and `whoami` / `get_credit_balance` are always free.
- If your plan lapses, calls are rejected until billing is restored.

## Security

- Keys are scoped to one workspace — a key can never reach another tenant.
- Revoke or rotate keys any time from the Integrations page.
- Never paste your key into public places; treat it like a password.

## Links

- Docs: [mcp.mightyautomation.com](https://mightyautomation.com/docs/mcp)
- Product: [mightyautomation.com](https://mightyautomation.com)
- Privacy: [mightyautomation.com/privacy](https://mightyautomation.com/privacy)
- Terms: [mightyautomation.com/terms](https://mightyautomation.com/terms)
- Support: support@mightyautomation.com

## License

MIT — see [LICENSE](LICENSE).
