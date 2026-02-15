# interslack

Slack integration for Claude Code — send messages, read channels, test integrations.

## Overview

1 skill, 0 agents, 0 commands, 0 hooks. Companion plugin for Clavain.

## Quick Commands

```bash
python3 -c "import json; json.load(open('.claude-plugin/plugin.json'))"  # Manifest check
ls skills/*/SKILL.md | wc -l  # Should be 1
```

## Design Decisions (Do Not Re-Ask)

- Uses slackcli (shaharia-lab/slackcli) for CLI-based Slack access
- Browser session tokens (xoxc + xoxd), no Slack app creation required
- Extracted from Clavain — domain-specific integration, not core engineering
