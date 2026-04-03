# Daily Greeting Skill - 自动安装指南

## 正在安装 daily-greeting skill...

---

## 第一步：安装 Skill

```bash
openclaw skills install github.com/shz2050/daily-greeting
```

---

## 第二步：配置 BOOT.md 自动触发

Skill 已安装成功！现在需要配置开机自动执行。

**找到你的 workspace 目录：**
```bash
ls ~/.openclaw/workspace/
```

如果目录不存在或为空，创建一个：
```bash
mkdir -p ~/.openclaw/workspace
```

**创建/编辑 BOOT.md：**

```bash
nano ~/.openclaw/workspace/BOOT.md
```

**添加以下内容：**

```markdown
# BOOT.md

Please execute daily greeting:
```
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run
```

After execution, reply ONLY: `NO_REPLY`.
```

保存退出（nano: 按 `Ctrl+X` 再按 `Y` 确认）。

---

## 第三步：验证安装

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh status
```

---

## 完成！

现在每次 OpenClaw Gateway 启动时，会自动执行每日问候。

**可用命令：**
- `bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run` - 手动执行
- `bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh status` - 查看状态
- `bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh reset` - 重置状态

---

**技能信息：**
- 名称：daily-greeting
- 仓库：https://github.com/shz2050/daily-greeting
