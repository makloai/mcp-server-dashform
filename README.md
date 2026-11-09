# Dashform MCP Server

Forms for AI agents. Connect Claude, ChatGPT, Codex, Cursor, or any MCP client to [Dashform](https://getaiform.com) and let it build, publish, and read your forms and the replies they collect.

Tell your assistant the intake you need. It creates the form in Dashform (questions, branching logic, follow-ups, result pages), publishes it with a shareable link, then reads and triages the replies, including each reply's lead score.

Dashform MCP is a hosted remote server. There is nothing to install.

| | |
|---|---|
| Endpoint | `https://getaiform.com/api/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1 with dynamic client registration (RFC 7591). No API key to copy. |
| Docs | [getaiform.com/docs/mcp](https://getaiform.com/docs/mcp) |

## Connect

### Claude

Open **Settings > Connectors**, choose **Add custom connector**, name it "Dashform", and paste `https://getaiform.com/api/mcp`. Sign in to Dashform and choose **Allow**.

### ChatGPT

Open [ChatGPT Plugins](https://chatgpt.com/plugins) and search for **Dashform**, or choose **Add**, then **Add custom MCP server**, paste the endpoint into **Server URL**, and choose **OAuth**.

### Codex

```bash
codex mcp add dashform --url https://getaiform.com/api/mcp
codex mcp login dashform
```

### Claude Code

```bash
claude mcp add --transport http dashform https://getaiform.com/api/mcp
```

### Cursor

Add Dashform to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "dashform": { "url": "https://getaiform.com/api/mcp" } } }
```

### VS Code

Add to `.vscode/mcp.json`:

```json
{ "servers": { "dashform": { "type": "http", "url": "https://getaiform.com/api/mcp" } } }
```

## Permissions

Each permission is an OAuth scope. Reading is separate from writing, and the consent screen lets you untick anything the client shouldn't have.

| Scope | Consent screen shows | Tools it reaches |
|---|---|---|
| `forms:read` | Read your forms | `list_forms`, `get_form`, `list_form_revisions`, `get_form_revision` |
| `forms:write` | Manage your forms | `create_form`, `update_form`, `publish_form`, `delete_form` |
| `replies:read` | Read your replies | `list_replies`, `get_reply` |
| `replies:write` | Manage your replies | `create_reply`, `update_reply`, `delete_reply`, `batch_delete_replies` |
| `offline_access` | Stay connected | Issues a refresh token |

Any granted scope also reaches the Organization tools and the public Marketplace tools. Revoke a connection at any time in Dashform under **Settings > Security**.

## Tools

### Forms

| Tool | What it does |
|---|---|
| `list_my_organizations` | List the Organizations you belong to |
| `get_organization` | Get one Organization by id or slug |
| `list_forms` | List the Forms in an Organization |
| `get_form` | Get one Form |
| `create_form` | Create a Form as a private draft, optionally from a template |
| `update_form` | Change a Form's fields; edits stay a draft until published |
| `publish_form` | Publish a Form, creating the Revision respondents see |
| `delete_form` | Permanently delete a Form with its revisions and replies |
| `list_form_revisions` | List a Form's published Revisions |
| `get_form_revision` | Get one Revision and the questions it asks |

### Replies

| Tool | What it does |
|---|---|
| `list_replies` | List Replies, filtered by lead score verdict, seen time, or completion |
| `get_reply` | Get one Reply with its answers and lead score |
| `create_reply` | Submit a Reply to a published Form |
| `update_reply` | Mark a Reply seen or override its lead score |
| `delete_reply` | Delete one Reply |
| `batch_delete_replies` | Delete up to 100 Replies under one Form |

### Marketplace

| Tool | What it does |
|---|---|
| `list_marketplace_categories` | List the categories merchants are listed under |
| `list_marketplace_profiles` | Find merchants by category, city, or name |
| `list_marketplace_services` | Find services across merchants |
| `get_marketplace_profile` | Get one merchant's profile, services, and booking link |
| `check_marketplace_fit` | Score a lead against a merchant's own qualification rules |

## Example prompts

- "Create a client intake form for my design agency that asks about budget, timeline, and scope, then publish it and give me the link."
- "Summarize this week's replies to my newest form and list the leads with the highest score."
- "Add a question about company size to my lead qualification form and republish it."

## Support

- Email: support@getaiform.com
- Website: [getaiform.com](https://getaiform.com)
- Issues: [GitHub Issues](https://github.com/makloai/mcp-server-dashform/issues)

## License

MIT
