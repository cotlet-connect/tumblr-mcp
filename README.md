# Tumblr MCP server for ChatGPT and Claude

Tumblr has a public API v2 with OAuth. The Cotlet.dev page reports no official Tumblr MCP server, checked 17 October 2026. Cotlet.dev connects ChatGPT, Claude and other AI agents to your own signed-in Tumblr account for blog posts, queues, drafts and asks. Changes ask for your approval by default.

## What you can ask

> Read posts waiting in my queue.

> List drafts on my blog.

> Draft answers to new asks for my review.

> Queue reblogs tagged pixel art after I approve.

## Connect in 2 minutes

Start at https://cotlet.dev/signup?app=tumblr, sign in to Tumblr with your own account in your Cotlet Cloud Browser, and create an API key in the console for editors or scripts. Export the key as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps & Connectors → Create, add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev using OAuth.

### Claude

Settings → Connectors → Add custom connector, enter `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repository provides a local MCP server with seven browser helper tools. It speaks MCP over stdio, lists those helpers without a key, and forwards calls to the hosted Cotlet.dev server. The hosted integration separately provides the 15 workflow tools listed on the live page. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"tumblr":{"command":"python3","args":["/absolute/path/to/tumblr-mcp/tumblr_agent.py","serve"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t tumblr-mcp .
docker run -i --rm -e COTLET_API_KEY tumblr-mcp
```

Tools: `tumblr_guide`, `tumblr_status`, `tumblr_open`, `tumblr_read`, `tumblr_click`, `tumblr_type`, `tumblr_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Clone this repository and run:

```bash
export COTLET_API_KEY="your-key"
python3 tumblr_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 tumblr_agent.py status    # is Tumblr ready in your Cotlet.dev account
python3 tumblr_agent.py guide     # Tumblr screens and sign-in link
python3 tumblr_agent.py read      # open Tumblr, read the page, close the browser
python3 tumblr_agent.py tools     # list Cotlet.dev tools
python3 tumblr_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Tumblr users

**Does Tumblr have an API?**

Yes. Tumblr has a public API v2 with OAuth for posts, queues, drafts, submissions, follows and notes.

**What does the hosted Tumblr integration provide?**

The live page describes 15 workflow tools for blogs, posts, queues, drafts, asks, notes and follows. This repository supplies seven local browser helper tools that forward to Cotlet.dev.

**Do changes need my approval?**

Posting, editing, reblogging, answering or deleting asks, deleting posts and following blogs ask for approval by default. You can change this per tool.

**Is this official?**

No. Cotlet.dev is independent and is not affiliated with Tumblr.

## Source

[Tumblr integration and all 15 hosted workflow tools](https://cotlet.dev/integrations/tumblr-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=tumblr)

---

More: https://cotlet.dev/integrations/tumblr-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=tumblr

Start free: https://cotlet.dev/signup?app=tumblr&utm_source=github&utm_medium=readme&utm_campaign=tumblr
