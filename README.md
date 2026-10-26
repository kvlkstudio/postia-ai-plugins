# Postia for Claude Code and Codex

Postia's MCP server is at `https://mcp.postia.app`. Sign-in is OAuth: the
first time, the browser opens Postia, you sign in and press Allow. Connected
assistants are listed, and can be disconnected, in Postia > Settings >
Account > AI assistants.

## Claude Code

```bash
claude plugin marketplace add kvlkstudio/postia-ai-plugins
claude plugin install postia@postia
```

Or the server alone, without the plugin's skill:

```bash
claude mcp add --transport http postia https://mcp.postia.app
```

Then `/mcp` > postia > Authenticate.

## Codex

```bash
codex plugin marketplace add kvlkstudio/postia-ai-plugins
codex plugin add postia@postia
codex mcp login postia
```

Or the server alone:

```bash
codex mcp add postia --url https://mcp.postia.app
codex mcp login postia
```

## Tools

list_channels, list_posts, get_post, create_post, update_post,
add_media_from_url, schedule_post, publish_post, unschedule_post, delete_post.
Posts are drafts until publish_post or schedule_post.
