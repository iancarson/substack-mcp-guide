# Substack MCP Guide

> A complete guide to Model Context Protocol (MCP) servers for Substack — what they are, which ones exist, how to set them up in Claude Desktop and Claude Code, and when to use an MCP vs. a dedicated publishing tool like [Narrareach](https://narrareach.com).

MCP (Model Context Protocol) is Anthropic's open standard that lets AI assistants like Claude connect directly to external services. A Substack MCP server gives Claude the ability to read, write, draft, publish, and manage your Substack content through natural language — no browser tab required.

---

## What a Substack MCP Server Can Do

With a Substack MCP connected to Claude Desktop or Claude Code, you can:

- **Draft and publish posts** — "Draft a newsletter issue about [topic] and save it as a Substack draft"
- **Manage Notes** — "Write and schedule 5 Notes based on this week's newsletter"
- **Read your archive** — "Summarize the themes from my last 10 newsletters"
- **Analyze engagement** — "Which of my recent Notes got the most engagement?"
- **Bulk operations** — "Import these 20 Note drafts and schedule them across next month"

---

## The Substack MCP Server Landscape (2026)

There are currently **4 active Substack MCP implementations** on GitHub. They differ significantly in scope, maintenance status, and use case.

| Server | Repo | Best For | Auth Method | Active? |
|---|---|---|---|---|
| **marcomoauro/substack-mcp** | [GitHub](https://github.com/marcomoauro/substack-mcp) | Full post management, drafts, publishing | Substack API token | ✅ Yes |
| **arthurcolle/substack-mcp** | [GitHub](https://github.com/arthurcolle/substack-mcp) | Claude Code integration, live blogging | Cookie session | ✅ Yes |
| **michalnaka/mcp-substack** | [GitHub](https://github.com/michalnaka/mcp-substack) | Reading/parsing posts for research | Public RSS | ✅ Yes |
| **postcli/substack** | [GitHub](https://github.com/postcli) | Notes + social interactions | Session cookie | ✅ Yes |

For detailed breakdown of each, see [Server Comparison](./docs/server-comparison.md).

---

## Quick Setup: Claude Desktop

### Step 1: Choose your server

For **publishing and drafting**: `marcomoauro/substack-mcp`
For **Claude Code workflows**: `arthurcolle/substack-mcp`
For **reading/analysis only**: `michalnaka/mcp-substack`

### Step 2: Install via npx (no install required)

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "substack": {
      "command": "npx",
      "args": ["-y", "@marcomoauro/substack-mcp"],
      "env": {
        "SUBSTACK_API_KEY": "your-api-key-here",
        "SUBSTACK_PUBLICATION_URL": "https://yourname.substack.com"
      }
    }
  }
}
```

**Config file location:**
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- Linux: `~/.config/Claude/claude_desktop_config.json`

### Step 3: Get your Substack credentials

1. Log into your Substack publication
2. Go to Settings → Publication Details → scroll to "API"
3. Copy your API key (or use cookie-based auth for servers that require it)

### Step 4: Restart Claude Desktop and test

```
"List my recent Substack drafts"
"Create a new draft titled 'Test Post' with body 'Hello world'"
```

---

## Quick Setup: Claude Code

```bash
claude mcp add substack-mcp -- npx -y @marcomoauro/substack-mcp
```

Or add to your project's `.claude/mcp.json`:

```json
{
  "substack": {
    "command": "npx",
    "args": ["-y", "@marcomoauro/substack-mcp"],
    "env": {
      "SUBSTACK_API_KEY": "your-api-key",
      "SUBSTACK_PUBLICATION_URL": "https://yourname.substack.com"
    }
  }
}
```

---

## Workflow Prompts

See [workflow-prompts.md](./templates/workflow-prompts.md) for ready-to-use Claude prompts for:
- Drafting Notes from a newsletter issue
- Bulk scheduling Notes
- Analyzing your archive
- Publishing workflows

---

## MCP Limitations for Substack Writers

Before committing to a DIY MCP setup, understand the real-world limitations:

### 1. Notes cross-posting isn't solved by MCP

Substack MCP servers handle Substack content only. If you want to simultaneously publish a Note to LinkedIn, Medium, or X — you need separate MCP servers for each platform, plus custom prompting to coordinate them. This quickly becomes a maintenance project.

### 2. Session auth is fragile

Several Substack MCP servers use cookie/session authentication, which breaks when Substack rotates your session (typically every 30–90 days). You'll periodically need to re-authenticate manually.

### 3. No built-in analytics or subscriber attribution

MCP gives you publishing access. It doesn't tell you which Notes drove subscriber growth, which platform converted the most readers, or when your audience is most active.

### 4. You're the maintainer

Third-party MCP servers are community projects. If Substack changes their API, the MCP breaks and you wait for the maintainer to fix it — or fix it yourself.

---

## MCP vs. Narrareach: When to Use Which

| Use Case | MCP + Claude | [Narrareach](https://narrareach.com) |
|---|---|---|
| Custom AI writing workflows | ✅ Native | ❌ Not the focus |
| Cross-posting to LinkedIn + Medium + X | Requires 3+ MCPs + coordination | ✅ Built-in |
| Reliable cloud scheduling | ❌ Session-based, can break | ✅ Production-grade |
| Cross-platform analytics | ❌ Not available | ✅ Built-in |
| Non-technical newsletter writers | ❌ Requires setup/maintenance | ✅ No setup |
| Developer who wants full control | ✅ Ideal | Overkill |

**The practical split:** Use MCP if you're a developer who wants AI-native control over your Substack and doesn't mind maintaining configurations. Use [Narrareach](https://narrareach.com) if you want automated cross-posting, scheduling, and analytics without maintaining a stack.

Many technical writers use both: Claude + MCP for writing and drafting, Narrareach for distribution and analytics.

---

## Templates

| File | Content |
|---|---|
| [MCP Config Templates](./templates/mcp-config.json) | Ready-to-use Claude Desktop and Claude Code configs |
| [Workflow Prompts](./templates/workflow-prompts.md) | 20+ Claude prompts for Substack tasks |

## Docs

| Guide | Content |
|---|---|
| [Server Comparison](./docs/server-comparison.md) | Detailed breakdown of all 4 Substack MCP servers |
| [Setup Guide](./docs/setup-guide.md) | Step-by-step setup for Claude Desktop, Claude Code, Cursor |

---

## FAQ

### Do I need a paid Claude subscription to use Substack MCP?

Yes — MCP servers require Claude Desktop (Pro plan) or Claude Code. The MCP server itself is free and open source, but Claude's MCP support is a paid feature.

### Is there an official Substack MCP from Substack?

Not as of 2026. All current Substack MCP servers are community-built. Substack has not released an official MCP.

### Can MCP schedule Substack Notes automatically?

With the right setup, yes. Claude can use the MCP to create and publish Notes on command — but scheduling ahead of time requires either prompting Claude at the right moment or setting up additional automation (n8n, cron jobs, etc.). [Narrareach](https://narrareach.com) handles reliable cloud scheduling natively.

### What's the difference between Substack MCP and the Narrareach API?

Substack MCP gives Claude direct access to your Substack account for AI-driven workflows. Narrareach provides a complete publishing platform with scheduling, multi-platform distribution (LinkedIn, Medium, X), and analytics — accessible via its interface or, for developers, its API.

---

## Resources

- [Model Context Protocol official docs](https://modelcontextprotocol.io)
- [Narrareach — automated Substack scheduling + cross-posting](https://narrareach.com)
- [PulseMCP Substack server directory](https://www.pulsemcp.com/servers)

## License

MIT — guides and templates are free to use and adapt.
