# Daily Greeting Skill - Installation Guide

## Installing daily-greeting skill...

---

## Step 1: Install the Skill

```bash
openclaw skills install github.com/shz2050/daily-greeting
```

---

## Step 2: Configure BOOT.md for Auto-trigger

The skill is installed! Now configure it to run automatically on Gateway startup.

**Find your workspace directory:**
```bash
ls ~/.openclaw/workspace/
```

If the directory doesn't exist or is empty, create it:
```bash
mkdir -p ~/.openclaw/workspace
```

**Create/edit BOOT.md:**

```bash
nano ~/.openclaw/workspace/BOOT.md
```

**Add this content:**

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

Save and exit (nano: `Ctrl+X` then `Y` to confirm).

**Record install info for uninstall:**

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh install ~/.openclaw/workspace/BOOT.md
```

---

## Step 3: Verify Installation

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh status
```

---

## Done!

Now daily-greeting will run automatically when OpenClaw Gateway starts.

**Available commands:**
- `bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run` - Manual run
- `bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh status` - Check status
- `bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh reset` - Reset state
- `bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh uninstall` - Uninstall skill

---

## Uninstall

To completely remove daily-greeting skill:

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh uninstall
```

This will:
1. Read the recorded BOOT.md path and remove only the daily-greeting section
2. Delete the skill directory

---

**Skill info:**
- Name: daily-greeting
- Repo: https://github.com/shz2050/daily-greeting
