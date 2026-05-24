# Substack MCP Setup Guide

Step-by-step instructions for connecting a Substack MCP server to Claude Desktop, Claude Code, and Cursor.

---

## Prerequisites

Before starting:
- Claude Desktop (Pro plan) or Claude Code installed
- Node.js 18+ installed (`node --version` to check)
- Your Substack publication URL
- Your Substack API key (or session cookie, depending on server)

---

## Getting Your Substack API Key

1. Go to your Substack publication dashboard
2. Click **Settings** in the left sidebar
3. Scroll to the **Integrations** or **API** section
4. Copy the API key shown

If no API key is visible, your Substack plan may not expose one. In that case, use a session cookie-based server (arthurcolle or postcli).

### Getting a Session Cookie (for cookie-based servers)

1. Log into Substack in Chrome
2. Open DevTools (F12) → Application tab → Cookies
3. Find `substack.sid` — this is your session token
4. Copy the value

**Warning:** Session cookies expire every 30–90 days. You will need to update your config when they do.

---

## Setup: Claude Desktop

### 1. Find your config file

| OS | Path |
|---|---|
| macOS | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Windows | `%APPDATA%\Claude\claude_desktop_config.json` |
| Linux | `~/.config/Claude/claude_desktop_config.json` |

### 2. Add the MCP server

Open the file (create it if it doesn't exist) and add:

```json
{
  "mcpServers": {
    "substack": {
      "command": "npx",
      "args": ["-y", "@marcomoauro/substack-mcp"],
      "env": {
        "SUBSTACK_API_KEY": "paste-your-api-key-here",
        "SUBSTACK_PUBLICATION_URL": "https://yourname.substack.com"
      }
    }
  }
}
```

### 3. Restart Claude Desktop

Fully quit and reopen Claude Desktop. The MCP server loads on startup.

### 4. Verify connection

In a new Claude conversation, type:

> "List my recent Substack drafts"

If connected correctly, Claude will return your actual drafts. If you see an error, check your API key and restart.

---

## Setup: Claude Code (CLI)

### Option A: One-line add

```bash
claude mcp add substack -- npx -y @marcomoauro/substack-mcp \
  SUBSTACK_API_KEY=your-key \
  SUBSTACK_PUBLICATION_URL=https://yourname.substack.com
```

### Option B: Project config file

Create `.claude/mcp.json` in your project root:

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

Then run `claude` in that directory — it picks up the config automatically.

### Test in Claude Code

```
/mcp
```

This shows all connected MCP servers. You should see `substack` listed.

---

## Setup: Cursor

Cursor uses the same config format as Claude Desktop.

1. Open Cursor Settings → MCP
2. Click "Add MCP Server"
3. Add the same JSON block as the Claude Desktop config above
4. Cursor picks up changes automatically — no restart needed

---

## Common Errors

### "spawn npx ENOENT"
Node.js is not installed or not in your PATH. Install from nodejs.org and restart your terminal.

### "Authentication failed"
Your API key is wrong or expired. Get a fresh key from Substack settings.

### "Cannot find module"
The npx package hasn't been downloaded yet. Run `npx -y @marcomoauro/substack-mcp` in your terminal first to cache it.

### "Session expired" (cookie-based servers)
Your `substack.sid` cookie has rotated. Get a fresh session cookie from your browser and update the config.

---

## Adding Multiple Substack MCPs

You can run multiple servers simultaneously:

```json
{
  "mcpServers": {
    "substack-publish": {
      "command": "npx",
      "args": ["-y", "@marcomoauro/substack-mcp"],
      "env": {
        "SUBSTACK_API_KEY": "your-key",
        "SUBSTACK_PUBLICATION_URL": "https://yourname.substack.com"
      }
    },
    "substack-research": {
      "command": "npx",
      "args": ["-y", "mcp-substack"],
      "env": {}
    }
  }
}
```

This gives you both publishing tools and research/reading tools in one Claude session.

---

## Security Notes

- **Never commit your API key or session cookie to a public repo** — use environment variables
- Store credentials in `.env` and reference them: `"SUBSTACK_API_KEY": "${SUBSTACK_API_KEY}"`
- If using `.env`, load it before running Claude: `source .env && claude`
- Rotate your Substack API key if you ever accidentally expose it

---

## Want Scheduling + Cross-Posting Without MCP Maintenance?

MCP gives you Claude-native control over Substack. If what you actually want is reliable scheduled publishing + automatic cross-posting to LinkedIn, Medium, and X — [Narrareach](https://narrareach.com/features/substack-mcp-integration) handles that without any config files, credential rotation, or maintenance. Both approaches have their place depending on whether you're a developer or a creator.
