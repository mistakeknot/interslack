# interslack — Vision and Philosophy

**Version:** 0.1.0
**Last updated:** 2026-02-28

## What interslack Is

interslack is a single-skill Claude Code plugin that bridges agent sessions to Slack. It sends messages, reads channels, and verifies integrations using browser session tokens — no Slack app registration, no OAuth dance, no webhook configuration. You extract xoxc and xoxd tokens from a logged-in browser session, configure slackcli once, and Claude can post to any channel or DM you have access to.

It was extracted from Clavain because Slack access is a domain-specific concern, not a core engineering workflow. Clavain handles engineering sessions; interslack handles what happens when those sessions need to reach the team.

## Why This Exists

Agent sessions produce decisions, deploy results, and status updates that need to reach humans. Without a communication bridge, that information lives only in terminal output — visible to nobody who wasn't watching. interslack makes agent communication a first-class artifact: a message sent to #engineering is durable, team-visible, and timestamped. It closes the loop between autonomous work and human awareness without requiring the agent to manage a Slack app or the user to configure an integration platform.

## Design Principles

1. **Token-scoped authority.** Access is granted by explicit session tokens that expire when the browser session ends. The agent acts as the authenticated user — nothing ambient, nothing persistent beyond what the user explicitly provides. Revocation is log out of Slack.

2. **Messages are receipts.** Sending a Slack message is an evidence artifact: a durable, timestamped record that the agent took a communication action. This aligns with the Demarch principle that every meaningful action produces a receipt. Reading a channel verifies that an expected event occurred.

3. **One thing, composed.** interslack does not orchestrate workflows, manage threads, or parse Slack events. It sends and reads. Composition with other plugins (intercore for task state, interkasten for notes, Clavain for engineering context) produces richer workflows. interslack stays dumb so the compositions stay clean.

4. **No app creation required.** Browser session tokens are available to any Slack user without admin access or app approval. This is the right default for an agent tool: low friction, no IT dependency, explicit access boundary tied to the user's existing session.

5. **Companion, not host.** interslack is a peer of Clavain, not a dependency. Engineering sessions don't require Slack; Slack integration doesn't require an engineering session. The boundary is a clean extraction.

## Scope

**Does:**
- Send messages to channels and DMs via slackcli
- Read recent messages from a channel or thread
- List accessible channels and workspaces
- Verify integration output by reading expected messages back
- Support multiple workspaces via slackcli's auth list

**Does not:**
- Manage Slack apps, bots, or webhooks
- Listen for events or maintain persistent subscriptions
- Handle message formatting beyond plain text
- Store or index Slack history
- Operate without user-provided session tokens

## Direction

- Add a SKILL-compact.md once the skill stabilizes past initial usage patterns
- Evaluate whether webhook-send (curl-based) warrants a second skill for teams that prefer bot tokens over user tokens
- Track whether slackcli gains thread management or reaction support, which would expand the skill's surface area without adding a new skill
