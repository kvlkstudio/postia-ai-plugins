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

list_channels, get_network_settings, get_setting_choices,
get_composer_library, list_posts, get_post, create_post, update_post,
preview_post, start_upload, finish_upload, upload_media_base64,
add_media_from_url, set_media_alt, reorder_media, remove_media, remove_cover, schedule_post, publish_post,
unschedule_post, retry_publication, duplicate_post, delete_post,
get_removable, take_down, send_on, create_share_link, revoke_share_link,
list_cloud_drives, browse_cloud, add_cloud_file, list_channel_sets,
save_channel_set, delete_channel_set, save_folder, delete_folder,
move_to_folder, save_hashtag_set, delete_hashtag_set, save_signature,
set_default_signature, delete_signature, update_watermark,
set_default_watermark, delete_watermark, get_setting_defaults,
save_setting_defaults, list_relay_rules, save_relay_rule,
set_relay_rule_active, delete_relay_rule, get_relay_history,
set_channel_active, rename_channel, set_default_destination,
list_notifications, mark_notifications_read, get_plan,
get_audience, get_publishing_stats, refresh_analytics (on plans with analytics).
Posts are drafts until publish_post or schedule_post.
