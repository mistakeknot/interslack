# interslack

Slack integration for Claude Code.

## What this does

Send messages, read channels, and test webhook integrations from Claude Code. Uses browser session tokens (xoxc + xoxd) via slackcli, so you don't need to create a Slack app or deal with OAuth: just grab your session tokens from the browser and go.

Straightforward plumbing for when you need Claude to post updates or check channels.

## Installation

First, add the [interagency marketplace](https://github.com/mistakeknot/interagency-marketplace) (one-time setup):

```bash
/plugin marketplace add mistakeknot/interagency-marketplace
```

Then install the plugin:

```bash
/plugin install interslack
```

Requires [slackcli](https://github.com/shaharia-lab/slackcli) installed and configured with your Slack session tokens.

## Usage

```
"send a message to #engineering saying the deploy is done"
"read the last 10 messages from #alerts"
"test the webhook integration"
```
