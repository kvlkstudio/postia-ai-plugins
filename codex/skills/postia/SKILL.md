---
name: postia
description: Write, schedule and publish social media posts through Postia. Use when the user wants to post to Telegram, Instagram, Facebook, Threads, X, LinkedIn, WordPress or other channels connected to Postia, to check what was scheduled or published, or to see how channels are growing and how deliveries went.
---

# Postia

The Postia MCP server acts on the user's own Postia account.

1. `list_channels` for the channel ids. Use only channels with `active: true`.
2. For each network in the post, `get_network_settings` (pass `network`) tells
   what it takes: privacy, audience, category, tags, playlist, first comment,
   poll, flair, link buttons… Fill every setting marked `required`, and the
   ones the user asked for. Settings with `choices_from` read their options
   from `get_setting_choices`. Signatures, watermarks, hashtag sets and
   folders come from `get_composer_library`.
3. `create_post` with the text and channel ids, plus `title` (YouTube, Reddit,
   Pinterest, blogs…), `settings`, and `channel_overrides` for a channel that
   needs its own text. It is saved as a draft; nothing goes out yet.
4. Attach files — pictures, videos, documents:
   - local files of any size: `start_upload`, then
     `curl -sf -T "<file>" "<upload_url>"`, then `finish_upload`;
   - small files when there is no shell: `upload_media_base64`;
   - a public https link to the file, or a Google Drive, Dropbox or
     OneDrive share link: `add_media_from_url`.
   Order of upload is the order in the carousel; `reorder_media` changes it.
   Give every picture `alt` (what it shows, for people who cannot see it)
   when attaching it, or later with `set_media_alt`. For a video cover, upload a
   picture with `as: "cover"`.
5. `preview_post` and fix what its `warnings` say (too long, dropped media,
   missing title). Show the user the final text and the channels, and ask
   before `publish_post` or `schedule_post`. Times are ISO 8601 with a time
   zone.
6. `get_post` afterwards shows where it went, with links and errors per
   channel; `retry_publication` resends a failed one, `duplicate_post` makes a
   new draft from an old post.

Beyond a single post:
- Already published: `get_removable` + `take_down` deletes it from a network,
  `send_on` sends it to more channels, `create_share_link` gives a preview
  link for someone to approve. Ask before take_down and send_on.
- Connected drives: `list_cloud_drives`, `browse_cloud`, `add_cloud_file`.
- Channel sets (`list_channel_sets`, `save_channel_set`; `channel_set_id` in
  create_post), folders, hashtag sets, signatures, watermarks and per-network
  defaults (`save_setting_defaults`) can be managed too.
- Autoposting rules: `list_relay_rules`, `save_relay_rule`,
  `set_relay_rule_active`, `get_relay_history`. Ask before creating one.
- `list_notifications` answers "what failed?"; `get_plan` shows limits.

For numbers: `get_audience` is followers per channel over time, as the networks
report them; `get_publishing_stats` is Postia's own record of what was
published, failed or skipped. Postia has no reach, views or likes per post, so
do not offer them. Both need a plan with analytics; if the call says it is not
part of the plan, tell the user it is in Postia under Plan.

The first call opens the browser to sign in to Postia and allow access. The user can disconnect the assistant in Postia: Settings > Account > AI assistants.
