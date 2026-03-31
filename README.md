# Dashform MCP Server

Connect AI assistants to [Dashform](https://getaiform.com) — build and manage AI-powered forms, funnels, quizzes, and lead qualification workflows through the Model Context Protocol.


## Features

- **Form Management** — Create, read, update, and delete forms and AI funnels programmatically
- **Reply Collection** — Submit and retrieve form responses
- **AI Lead Qualification** — Use built-in AI to check if a lead is a good fit for a business
- **Service Marketplace** — Search merchants, services, and categories
- **Booking** — Check availability and book appointments through AI agents
- **OAuth 2.1** — Secure authentication with dynamic client registration

## Quickstart

Dashform MCP is a hosted remote server. No local installation is required — just add the endpoint URL to your MCP client.

**Endpoint:** `https://getaiform.com/api/mcp`

**Transport:** Streamable HTTP

**Authentication:** OAuth 2.1 with dynamic client registration (RFC 7591)

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "dashform": {
      "url": "https://getaiform.com/api/mcp"
    }
  }
}
```

Claude Desktop will handle OAuth authorization automatically.

### Cursor

Add to your Cursor MCP settings (`.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "dashform": {
      "url": "https://getaiform.com/api/mcp"
    }
  }
}
```

### VS Code / GitHub Copilot

Add to your VS Code settings (`.vscode/mcp.json`):

```json
{
  "servers": {
    "dashform": {
      "url": "https://getaiform.com/api/mcp"
    }
  }
}
```

### Windsurf

Add to your `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "dashform": {
      "serverUrl": "https://getaiform.com/api/mcp"
    }
  }
}
```

### MCP Inspector

```bash
npx @modelcontextprotocol/inspector --url https://getaiform.com/api/mcp
```

## Tools

### Form Management (requires authentication)

| Tool | Description |
|------|-------------|
| `get_user_info` | Get current user profile (userId, organizationId, name, email) |
| `list_organizations` | List all organizations for a user |
| `list_forms` | List all forms in an organization with reply counts |
| `get_form` | Get full form details including config, questions, and theme |
| `create_form` | Create a new form (structured or dynamic AI type) |
| `update_form` | Update form config, questions, endings, or theme |
| `delete_form` | Permanently delete a form and all its data |
| `create_reply` | Submit a new reply/response to a form |

### Marketplace Discovery (no authentication required)

| Tool | Description |
|------|-------------|
| `list_categories` | List marketplace service categories with merchant counts |
| `search_merchants` | Search merchants by keyword, category, or location |
| `search_services` | Search services across all merchants with price filtering |

### Agent Booking (no authentication required)

| Tool | Description |
|------|-------------|
| `get_business_info` | Get business profile for a published funnel |
| `get_services` | List available services for a funnel |
| `get_form_questions` | Get question schema (keys, types, options) for a funnel |
| `check_fit` | AI-powered lead qualification — checks if a lead matches the business criteria |
| `get_availability` | Get booking availability and scheduling link |
| `book_appointment` | Submit a lead record and book an appointment |

## Authentication

Dashform MCP uses **OAuth 2.1** with the Authorization Code flow and supports **dynamic client registration** (RFC 7591). This means MCP clients like Claude Desktop and Cursor can automatically register and authenticate without manual API key setup.

### OAuth Endpoints

| Endpoint | URL |
|----------|-----|
| Authorization | `https://getaiform.com/oauth/authorize` |
| Token | `https://getaiform.com/api/auth/oauth2/token` |
| Client Registration | `https://getaiform.com/api/auth/oauth2/register` |
| Resource Metadata | `https://getaiform.com/.well-known/oauth-protected-resource` |
| MCP Discovery | `https://getaiform.com/.well-known/mcp.json` |

### Scopes

| Scope | Description |
|-------|-------------|
| `openid` | OpenID Connect identity |
| `profile` | User profile information |
| `email` | User email address |
| `read:forms` | Read forms and form data |
| `write:forms` | Create and update forms |
| `read:submissions` | Read form submissions |
| `write:submissions` | Create form submissions |
| `read:webhooks` | Read webhook configurations |
| `offline_access` | Refresh token for long-lived sessions |

## MCP Discovery

The server exposes a discovery endpoint at `/.well-known/mcp.json` that returns the server manifest, including all available tools and the endpoint URL.

```bash
curl https://getaiform.com/.well-known/mcp.json
```

## Use Cases

- **Build forms with natural language** — "Create a customer feedback form with a rating scale and open-ended questions"
- **Manage forms at scale** — List, update, or delete forms across organizations
- **Collect responses** — Submit test data or integrate with automated pipelines
- **AI-powered lead qualification** — "Check if this lead is a good fit for my consulting business"
- **Service discovery** — "Find yoga studios in San Francisco that offer private sessions"
- **Appointment booking** — "Book a free consultation with the nearest available therapist"

## Support

- Email: support@getaiform.com
- Website: [getaiform.com](https://getaiform.com)
- Issues: [GitHub Issues](https://github.com/makloai/mcp-server-dashform/issues)

## License

MIT
