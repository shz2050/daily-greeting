# Daily Greeting Skill

<!-- Language Navigation -->
[English](../README.md) | [中文](README_zh.md)

---

## 简介

一个 OpenClaw 技能，在 Gateway 启动时自动触发所有绑定的 agent 发送每日问候消息。

**让你的 OpenClaw agent 自动发送个性化每日问候。**

## 功能特性

| 功能 | 描述 |
|------|------|
| 🎯 **自动触发** | Gateway 启动时自动执行（通过 BOOT.md） |
| 📊 **状态持久化** | 防止同一天内重复执行 |
| 🔌 **多平台支持** | 支持 Discord、飞书等其他平台 |
| ⏰ **工作日过滤** | 仅在工作日触发（可配置） |
| 🔄 **可重置** | 支持手动重置状态 |
| 🎨 **角色定制** | 每个 agent 以自己的风格发送消息 |
| 🧹 **干净卸载** | 仅删除技能相关内容，无残留文件 |

## 快速开始

### 一键安装（推荐）

将以下命令发送给 OpenClaw：

```
请执行 daily-greeting 安装指南：
https://raw.githubusercontent.com/shz2050/daily-greeting/main/guide.md
```

OpenClaw 将自动读取指南并完成整个安装（技能安装 + BOOT.md 配置 + 安装记录）。

### 手动安装

```bash
# 克隆仓库
git clone https://github.com/shz2050/daily-greeting.git

# 复制到 OpenClaw 技能目录
cp -r daily-greeting ~/.openclaw/skills/daily-greeting

# 赋予脚本执行权限
chmod +x ~/.openclaw/skills/daily-greeting/scripts/greeting.sh
```

### 自动触发配置

此技能通过 `BOOT.md` 在 Gateway 启动时自动触发。你需要在 OpenClaw 工作区中创建此文件。

**1. 找到你的工作区目录：**

```bash
ls ~/.openclaw/workspace/
```

**2. 创建或编辑 `BOOT.md`：**

```bash
nano ~/.openclaw/workspace/BOOT.md
```

**3. 添加以下内容：**

````markdown
# BOOT.md

<!-- daily-greeting:start -->
请执行每日问候：
```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run
```

执行后，仅回复：`NO_REPLY`。
<!-- daily-greeting:end -->
````

**4. 记录安装信息（用于干净卸载）：**

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh install ~/.openclaw/workspace/BOOT.md
```

现在，当 OpenClaw Gateway 启动时，它将自动执行此问候技能。

### 常用命令

```bash
# 手动执行问候
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh run

# 查看状态
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh status

# 重置状态（允许重新执行）
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh reset

# 卸载（删除技能并清理 BOOT.md）
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh uninstall
```

## 配置

编辑 `config.json` 自定义行为：

```json
{
  "enabled": true,
  "workingDaysOnly": true,
  "delayMs": 3000,
  "excludeAgents": ["main"],
  "triggerMessage": "请发送每日问候到你绑定的频道。要求：1) 根据你的人设和性格组织消息内容；2) 使用消息工具发送到绑定的频道；3) 发送后结束对话"
}
```

| 配置项 | 类型 | 默认值 | 描述 |
|--------|------|--------|------|
| `enabled` | boolean | `true` | 启用/禁用技能 |
| `workingDaysOnly` | boolean | `true` | 仅在工作日触发（周一至周五） |
| `delayMs` | number | `3000` | 执行前延迟（毫秒） |
| `excludeAgents` | array | `["main"]` | 排除的 agent |
| `triggerMessage` | string | (见上方) | 发送给每个 agent 的消息 |

## 工作原理

```
Gateway 启动
    ↓
BOOT.md 执行
    ↓
greeting.sh 运行
    ↓
读取配置 → 检查工作日 → 检查今日是否已执行
    ↓
对每个绑定的 agent：
    - 触发 agent 并发送提示
    - Agent 发送个性化问候到绑定频道
    ↓
状态保存到 data/state.json
```

## 卸载

完全移除 daily-greeting 技能：

```bash
bash ~/.openclaw/skills/daily-greeting/scripts/greeting.sh uninstall
```

此命令将：
1. 从 `data/install.json` 读取记录的 BOOT.md 路径
2. 仅移除标记的 daily-greeting 部分
3. 删除技能目录

## 目录结构

```
daily-greeting/
├── SKILL.md              # 技能定义
├── README.md             # 英文文档
├── docs/
│   └── README_zh.md      # 中文文档
├── guide.md              # 安装指南（用于 OpenClaw 自动安装）
├── LICENSE               # MIT 许可证
├── config.json           # 配置文件
├── scripts/
│   └── greeting.sh       # 主执行脚本
└── data/
    ├── state.json        # 执行状态（自动生成）
    └── install.json      # 安装记录（BOOT.md 路径）
```

## 环境要求

- OpenClaw Gateway
- Bash 4.0+
- jq（JSON 解析）

## 许可证

MIT 许可证 - 详见 LICENSE 文件。

## 贡献

欢迎贡献！请提交 issue 或 PR。

## 支持

如有问题，请提交 GitHub issue。
