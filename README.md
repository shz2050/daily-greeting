# Daily Greeting Skill

A OpenClaw skill that automatically triggers all bound agents to send daily greeting messages when the Gateway starts.

## Overview

This skill executes on Gateway startup and triggers each configured agent to send their own personalized daily greeting to their bound channels. Each agent organizes their message based on their own persona and character.

## Features

- 🎯 **Auto-trigger**: Executes automatically on Gateway startup (via BOOT.md)
- 📊 **State persistence**: Prevents duplicate executions within the same day
- 🔌 **Multi-platform support**: Works with Discord, Feishu, and other channels
- ⏰ **Working days filter**: Only triggers on weekdays (configurable)
- 🔄 **Resettable**: Manual reset available for re-execution
- 🎨 **Persona-based**: Each agent sends messages in their own style

## Quick Start

### One-Click Install (Recommended)

**Step 1: Install the skill**

```bash
openclaw skills install github.com/shz2050/daily-greeting
```

**Step 2: Let OpenClaw auto-configure BOOT.md**

Send OpenClaw this command to automatically set up auto-trigger:

```
Please read and execute the installation guide:
https://raw.githubusercontent.com/shz2050/daily-greeting/main/guide.md
```

That's it! OpenClaw will read the guide and automatically complete the BOOT.md setup.

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

This skill auto-triggers on Gateway startup via `BOOT.md`. You need to create this file in your OpenClaw workspace.

**1. Find your workspace directory:**

```bash
# Usually ~/.openclaw/workspace/ or the directory where you run openclaw
ls ~/.openclaw/workspace/
```

**2. Create or edit `BOOT.md` in your workspace:**

```bash
nano ~/.openclaw/workspace/BOOT.md
```

**3. Add this content:**

```markdown
# BOOT.md

Please execute daily greeting:
```
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run
```

After execution, reply ONLY: `NO_REPLY`.
```

Now when OpenClaw Gateway starts, it will automatically execute this greeting skill.

### Manual Execution

```bash
# Run greeting
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run

# Check status
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh status

# Reset (allow re-execution)
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh reset
```

## Configuration

Edit `config.json`:

```json
{
  "enabled": true,
  "workingDaysOnly": true,
  "delayMs": 3000,
  "excludeAgents": ["main"],
  "triggerMessage": "Please send a daily greeting to your bound channel. Requirements: 1) Organize message content based on your persona and character; 2) Use message tool to send to your bound channel; 3) End conversation after sending"
}
```

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `enabled` | boolean | true | Enable/disable the skill |
| `workingDaysOnly` | boolean | true | Only trigger on weekdays (Mon-Fri) |
| `delayMs` | number | 3000 | Delay before execution (milliseconds) |
| `excludeAgents` | array | ["main"] | Agents to exclude from greeting |
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

## Directory Structure

```
daily-greeting/
├── SKILL.md           # Skill definition
├── README.md          # This file
├── LICENSE            # MIT License
├── config.json        # Configuration
├── scripts/
│   └── greeting.sh    # Main execution script
└── data/
    └── state.json     # Execution state (auto-generated)
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