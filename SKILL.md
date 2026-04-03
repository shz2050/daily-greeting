---
name: daily-greeting
description: Daily greeting Skill. Automatically sends greeting messages to all bound channels when OpenClaw starts. Triggers each agent to send their own daily greeting based on their persona. Executes once per day with local persistence.
---

# Daily Greeting Skill

## Features

- 🎯 **Auto-trigger**: Executes on Gateway startup (via BOOT.md)
- 📊 **State persistence**: Records execution status, prevents duplicate runs
- 🔌 **Multi-platform**: Supports Discord, Feishu, etc.
- ⏰ **Working days filter**: Only triggers on weekdays (configurable)
- 🔄 **Resettable**: Supports manual reset

## Installation

1. Clone or copy skill to `~/.openclaw/skills/daily-greeting/`
2. Ensure script is executable: `chmod +x scripts/greeting.sh`

## Usage

### Manual Execution

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run
```

### Auto-trigger

Add to workspace `BOOT.md`:

```markdown
# BOOT.md

<!-- daily-greeting:start -->
Please execute daily greeting:
```
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run
```

After execution, reply ONLY: `NO_REPLY`.
<!-- daily-greeting:end -->
```

**Record install info (for clean uninstall):**
```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh install ~/.openclaw/workspace/BOOT.md
```

## Configuration

Configure in `config.json`:

```json
{
  "enabled": true,
  "workingDaysOnly": true,
  "delayMs": 3000,
  "excludeAgents": ["main"],
  "triggerMessage": "Please send a daily greeting to your bound channel. Requirements: 1) Compose the greeting in the user's preferred language (infer from channel history and user context); 2) Include relevant status information based on your agent role and ongoing tasks with the user (e.g., if you're a todo agent, summarize progress and today's priorities; if you're a diary agent, mention ongoing projects); 3) Use message tool to send to your bound channel; 4) End conversation after sending"
}
```

## Greeting Content

Each agent organizes their own greeting message based on their persona and sends it to their bound channel.

## Commands

| Command | Description |
|---------|-------------|
| `bash scripts/greeting.sh run` | Execute greeting manually |
| `bash scripts/greeting.sh status` | View execution status |
| `bash scripts/greeting.sh reset` | Reset state (allows re-trigger) |
| `bash scripts/greeting.sh install` | Record BOOT.md path (for uninstall) |
| `bash scripts/greeting.sh uninstall` | Remove skill and clean BOOT.md |

## State File

State is stored in `data/state.json`:

```json
{
  "lastRun": "2026-04-03T10:40:00Z",
  "agents": {
    "diary": "completed"
  }
}
```

## Uninstall

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh uninstall
```

This will:
1. Read the recorded BOOT.md path from `data/install.json`
2. Remove **only** the marked daily-greeting section
3. Delete the skill directory

## Open Source License

MIT License - Welcome contributions!