# Substack MCP Server Comparison

Detailed breakdown of every active Substack MCP server in 2026.

---

## 1. marcomoauro/substack-mcp

**Repo:** https://github.com/marcomoauro/substack-mcp
**Maintained:** Yes
**Install:** `npx -y @marcomoauro/substack-mcp`

### What it does
The most complete Substack MCP server. Covers the full post management lifecycle:
- Create, edit, and delete drafts
- Publish posts (free and paid)
- Manage post metadata (title, subtitle, cover image, section)
- Schedule posts for future publication
- List and retrieve existing posts

### Authentication
Uses Substack's API token. More stable than cookie-based auth — tokens don't rotate as frequently as sessions.

### Best for
Writers who want to use Claude for drafting and publishing Substack newsletters. The primary use case is: "Claude, write my newsletter draft about [topic] and save it to Substack."

### Limitations
- Focuses on newsletter posts, not Notes specifically
- No cross-posting to other platforms
- No analytics tools

### Config
```json
{
  "mcpServers": {
    "substack": {
      "command": "npx",
      "args": ["-y", "@marcomoauro/substack-mcp"],
      "env": {
        "SUBSTACK_API_KEY": "YOUR_API_KEY",
        "SUBSTACK_PUBLICATION_URL": "https://yourpublication.substack.com"
      }
    }
  }
}
```

---

## 2. arthurcolle/substack-mcp

**Repo:** https://github.com/arthurcolle/substack-mcp
**Maintained:** Yes
**Focus:** Claude Code integration

### What it does
Built specifically for Claude Code workflows. Features include:
- Create and manage drafts
- Upload images to Substack CDN
- Live blogging — real-time post updates as Claude writes
- Interactive post construction

### Authentication
Cookie/session-based. Requires periodic re-authentication when Substack rotates your session.

### Best for
Developers using Claude Code who want to build newsletter automation into their coding workflow. Example: "As part of my project documentation workflow, save a summary as a Substack draft."

### Limitations
- Session auth breaks every 30–90 days
- Requires manual re-auth when session expires
- Not suited for long-running automated workflows without re-auth handling

---

## 3. michalnaka/mcp-substack

**Repo:** https://github.com/michalnaka/mcp-substack
**Maintained:** Yes
**Focus:** Reading and research

### What it does
Designed for content analysis, not publishing:
- Download and parse Substack posts from any publication
- Search across newsletters
- Feed content to Claude for analysis, summarization, or research

### Authentication
Public RSS — no credentials required for public content. Authenticated access for your own private content.

### Best for
Researchers, newsletter writers doing competitive analysis, or anyone who wants to ask Claude questions about existing Substack content. Example: "Download the last 20 issues of [newsletter] and identify the 5 most common themes."

### Limitations
- Read-only for public content
- Not a publishing tool

---

## 4. postcli/substack (via @postcli)

**Repo:** https://github.com/postcli
**Maintained:** Yes
**Focus:** Notes and social interactions

### What it does
Extends beyond basic publishing to social layer:
- Post and manage Notes
- Like, restack, and comment on Notes
- Manage subscriber interactions
- Social engagement automation

### Authentication
Session cookie-based.

### Best for
Writers who want Claude to manage their Notes feed and social interactions. Example: "Like back everyone who liked my last three Notes" or "Write and post a Note responding to this trend in the feed."

### Limitations
- Session auth fragility (same as arthurcolle)
- Social automation features can risk account flagging if overused
- No cross-posting to external platforms

---

## Side-by-Side Feature Matrix

| Feature | marcomoauro | arthurcolle | michalnaka | postcli |
|---|---|---|---|---|
| Create drafts | ✅ | ✅ | ❌ | ❌ |
| Publish posts | ✅ | ✅ | ❌ | ❌ |
| Manage Notes | Limited | ❌ | ❌ | ✅ |
| Read/parse posts | ✅ | ✅ | ✅ | ✅ |
| Social interactions | ❌ | ❌ | ❌ | ✅ |
| Upload images | ❌ | ✅ | ❌ | ❌ |
| Live blogging | ❌ | ✅ | ❌ | ❌ |
| Auth type | API token | Session | Public/session | Session |
| Auth stability | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| Cross-posting | ❌ | ❌ | ❌ | ❌ |

---

## Recommendation by Use Case

**"I want Claude to write and publish my newsletters"**
→ `marcomoauro/substack-mcp` — most stable API token auth, full post management

**"I'm a developer using Claude Code and want Substack integrated into my workflow"**
→ `arthurcolle/substack-mcp` — built for Claude Code, supports image uploads and live blogging

**"I want to analyze my newsletter archive or a competitor's newsletter"**
→ `michalnaka/mcp-substack` — read-only, no credentials needed for public content

**"I want Claude to manage my Notes and social engagement"**
→ `postcli/substack` — Notes + social layer, accept the session auth overhead

**"I want all of the above plus cross-posting to LinkedIn and Medium without maintaining MCP configs"**
→ [Narrareach](https://narrareach.com/features/substack-mcp-integration) — production-grade distribution platform, no MCP maintenance required
