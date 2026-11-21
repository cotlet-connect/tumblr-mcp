---
name: tumblr-cotlet
description: Connect Tumblr to ChatGPT, Claude and other AI agents through Cotlet.dev, so the agent can manage blog posts, queues, drafts and asks in your own signed-in Tumblr account.
---

# Tumblr through Cotlet.dev

## What it does

Cotlet.dev runs your own Chrome in the cloud. The agent works in Tumblr (tumblr.com) there, signed in as you.

## Setup

1. Get an API key at https://cotlet.dev/app.
2. Add the MCP server `https://cotlet.dev/mcp/v1` with header `Authorization: Bearer <your key>`.

## Working rules

- First call `cotlet_app_guide` with app "tumblr".
- Then use `cotlet_browser_open`, `cotlet_browser_read` and `cotlet_browser_click`, one call at a time. Wait for each answer.
- At a sign-in page or CAPTCHA, stop and give the user the browser link.
- Ask the user before sending, publishing, deleting or paying.
- Close the browser with `cotlet_browser_close` when done.

More: https://cotlet.dev/integrations/tumblr-api-mcp-server?utm_source=clawhub&utm_medium=skill&utm_campaign=tumblr
