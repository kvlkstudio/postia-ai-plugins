---
name: postia
description: Write, schedule and publish social media posts through Postia. Use when the user wants to post to Telegram, Instagram, Facebook, Threads, X, LinkedIn, WordPress or other channels connected to Postia, to check what was scheduled or published, or to see how channels are growing and how deliveries went.
---

# Postia

The Postia MCP server acts on the user's own Postia account.

1. `list_channels` for the channel ids. Use only channels with `active: true`.
2. `create_post` with the text and channel ids. It is saved as a draft; nothing goes out yet.
3. Attach pictures or video with `add_media_from_url` (public links only).
4. Show the user the final text and the channels, and ask before
   `publish_post` or `schedule_post`. Times are ISO 8601 with a time zone.
5. `get_post` afterwards shows where it went, with links and errors per channel.

For numbers: `get_audience` is followers per channel over time, as the networks
report them; `get_publishing_stats` is Postia's own record of what was
published, failed or skipped. Postia has no reach, views or likes per post, so
do not offer them. Both need a plan with analytics; if the call says it is not
part of the plan, tell the user it is in Postia under Plan.

The first call opens the browser to sign in to Postia and allow access. The user can disconnect the assistant in Postia: Settings > Account > AI assistants.
