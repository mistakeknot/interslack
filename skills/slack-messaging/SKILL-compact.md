# Slack Messaging (compact)

Send and read Slack messages from the command line using `slackcli`.

Resolve the installed skill symlink and set `SKILL_DIR` to its actual directory
before invoking bundled helpers. A read request authorizes reading; sending
messages, installing tools, and extracting authentication need their own task
authority. Never print or include tokens in prompts, evidence, or commits.

## When to Invoke

Use when asked to send or read Slack messages, check channels, test Slack integrations, or interact with a Slack workspace.

## Authentication

```bash
# Interactive setup (walks through browser token extraction)
"$SKILL_DIR/scripts/extract-tokens" <workspace-url>

# Manual setup
slackcli auth login-browser --xoxd="xoxd-..." --xoxc="xoxc-..." --workspace-url=https://workspace.slack.com

# Verify
slackcli auth list
```

## Core Commands

```bash
# Find channels
slackcli conversations list
slackcli conversations list | grep -i "channel-name"

# Send message
slackcli messages send --recipient-id=C0XXXXXXXX --message="Hello"

# Reply in thread
slackcli messages send --recipient-id=C0XXXXXXXX --message="Reply" --thread-ts=1769756026.624319

# Read messages
slackcli conversations read C0XXXXXXXX --limit=10
slackcli conversations read C0XXXXXXXX --limit=10 --json

# Read thread
slackcli conversations read C0XXXXXXXX --thread-ts=1769756026.624319
```

## Key Facts

- `--recipient-id` is always a channel ID (C...) or DM channel ID (D...)
- Browser tokens (xoxc/xoxd) act as the logged-in user, not a bot
- Tokens expire on browser logout; re-extract to refresh
- Multiple workspaces supported; auto-routes by channel ID
- Credentials stored at `~/.config/slackcli/workspaces.json`

## Testing Integrations

```bash
# Verify a message was posted
slackcli conversations read CHANNEL_ID --limit=5 --json | jq '.messages[] | select(.text | contains("expected"))'
```

---
*For installation, multi-workspace setup, and full token notes, read SKILL.md.*
