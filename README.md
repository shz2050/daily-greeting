# Daily Greeting Skill

<!-- Language Navigation -->
[English](README.md) | [中文](docs/README_zh.md)

---

## Overview

A OpenClaw skill that automatically triggers all bound agents to send daily greeting messages when the Gateway starts.

**Give your OpenClaw agents the ability to send personalized daily greetings automatically.**

## Features

| Feature | Description |
|---------|-------------|
| 🎯 **Dual trigger modes** | Supports both BOOT.md (on startup) and cron (scheduled) |
| 📊 **State persistence** | Prevents duplicate executions within the same day |
| 🔌 **Multi-platform** | Works with Discord, Feishu, and other channels |
| ⏰ **Working days filter** | Only triggers on weekdays (configurable) |
| 🔄 **Resettable** | Manual reset available for re-execution |
| 🎨 **Persona-based** | Each agent sends messages in their own style |
| 🧹 **Clean uninstall** | Removes only skill content, no leftover files |

## Quick Start

### One-Click Install (Recommended)

Send OpenClaw this command:

```
Please execute the daily-greeting installation guide:
https://raw.githubusercontent.com/shz2050/daily-greeting/main/guide.md
```

OpenClaw will automatically read the guide and complete the entire installation (skill + BOOT.md setup + install record).

### Manual Installation

```bash
# Clone this repository
git clone https://github.com/shz2050/daily-greeting.git

# Copy to OpenClaw skills directory
cp -r daily-greeting ~/.openclaw/skills/daily-greeting

# Make script executable
chmod +x ~/.openclaw/skills/daily-greeting/scripts/greeting.sh
```

### Auto-trigger Setup

Choose one or both triggering methods based on your usage:

#### Auto-trigger Setup

Both BOOT.md and cron are enabled by default. State check prevents duplicate greetings.

**BOOT.md (triggers on Gateway startup):**

```bash
# Find workspace
ls ~/.openclaw/workspace/

# Create/edit BOOT.md
nano ~/.openclaw/workspace/BOOT.md
```

Add this content:

````markdown
# BOOT.md

<!-- daily-greeting:start -->
Please execute daily greeting:
```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run
```

After execution, reply ONLY: `NO_REPLY`.
<!-- daily-greeting:end -->
````

**Cron (triggers on schedule):**

Default cron: `0 9 * * 1-5` (9am on weekdays)

To modify:
```bash
crontab -e
```

**Record install info:**

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh install ~/.openclaw/workspace/BOOT.md
```

### Commands

```bash
# Run greeting manually
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run

# Check status
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh status

# Reset (allow re-execution)
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh reset

# Uninstall (removes skill and cleans BOOT.md)
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh uninstall
```

## Configuration

Edit `config.json` to customize behavior:

```json
{
  "enabled": true,
  "workingDaysOnly": true,
  "delayMs": 3000,
  "excludeAgents": ["main"],
  "triggerMessage": "Please send a daily greeting to your bound channel. Requirements: 1) Compose the greeting in the user's preferred language (infer from channel history and user context); 2) Include relevant status information based on your agent role and ongoing tasks with the user (e.g., if you're a todo agent, summarize progress and today's priorities; if you're a diary agent, mention ongoing projects); 3) Use message tool to send to your bound channel; 4) End conversation after sending"
}
```

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `enabled` | boolean | `true` | Enable/disable the skill |
| `workingDaysOnly` | boolean | `true` | Only trigger on weekdays (Mon-Fri) |
| `delayMs` | number | `3000` | Delay before execution (milliseconds) |
| `excludeAgents` | array | `["main"]` | Agents to exclude from greeting |
| `triggerMessage` | string | (see above) | Message sent to each agent |

## How It Works

```
Gateway starts
    ↓
BOOT.md executes
    ↓
greeting.sh runs
    ↓
Reads config → checks working day → checks if already run today
    ↓
For each bound agent:
    - Trigger agent with prompt
    - Agent sends personalized greeting to their bound channel
    ↓
State saved to data/state.json
```

## Uninstall

To completely remove daily-greeting skill:

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh uninstall
```

This will:
1. Read the recorded BOOT.md path from `data/install.json`
2. Remove **only** the marked daily-greeting section
3. Delete the skill directory

## Directory Structure

```
daily-greeting/
├── SKILL.md              # Skill definition
├── README.md             # This file
├── guide.md              # Installation guide (for OpenClaw auto-install)
├── LICENSE               # MIT License
├── config.json           # Configuration
├── scripts/
│   └── greeting.sh       # Main execution script
└── data/
    ├── state.json        # Execution state (auto-generated)
    └── install.json      # Install record (BOOT.md path)
```

## Requirements

- OpenClaw Gateway
- Bash 4.0+
- jq (for JSON parsing)

## License

MIT License - See LICENSE file for details.

## Contributing

Contributions welcome! Please open an issue or submit a PR.

## Support

For issues and questions, please open a GitHub issue.

---

## Star History

[![Star History](https://api.star-history.com/svg?repos=shz2050/daily-greeting&type=Timeline&theme=dark)](https://star-history.com/#shz2050/daily-greeting&type=Timeline)
