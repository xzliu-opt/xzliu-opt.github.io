---
title: 'Claude Code 实战：开启 Vibe Coding 的全能助手'
date: 2026-02-03
tags:
  - Claude Code
  - Vibe Coding
  - AI Tooling
---

最近我开始深入学习 Anthropic 官方的 [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) 课程。Claude Code 不仅仅是一个 CLI 工具，它更像是 Vibe Coding 流程中的“大脑”，能够深度接入本地开发环境并理解工程语境。

## 🚀 快速起步：`/init` 的奥秘

在任何新项目中，第一步应当运行 `/init`。这个指令会让 Claude 深度扫描整个代码库，从而理解：
* **项目愿景与架构**：它是干什么的？模块之间如何交互？
* **核心指令与关键文件**：如何运行、测试以及哪些是核心配置？
* **编码范式与风格**：现有的代码是如何组织的？

分析完成后，Claude 会自动生成并维护一个 `CLAUDE.md` 文件。

---

## 📂 层次化的上下文管理

Claude Code 通过三个不同层级的 Markdown 文件来构建“记忆”，这对于保持开发风格的一致性至关重要：

| 文件名 | 作用范围 | 共享与协作 |
| :--- | :--- | :--- |
| **`CLAUDE.md`** | 项目级 | **推荐提交到 Git**。作为项目的“AI 说明书”，让团队成员的 AI 步调一致。 |
| **`CLAUDE.local.md`** | 本地级 | **忽略不提交**。用于存放个人偏好、私有 API 或临时调试指令。 |
| **`~/.claude/CLAUDE.md`** | 全局级 | **跨项目通用**。定义 Claude 在你所有项目中必须遵循的全局准则（如：永远使用 TypeScript）。 |

> **💡 高级技巧：Memory Mode**
> 使用 `#` 命令进入“记忆模式”。你可以像对话一样智能编辑这些文件，例如：`# 注释要简练，只针对复杂逻辑写注释`。

---

## 🧠 深度思考与规划 (Planning Mode)

当你面对跨文件的大规模重构时，连按两次 `Shift + Tab` 即可进入 **Planning Mode**。

### 规划模式 vs 思考模式
* **Planning Mode (规划模式)**：专注于**广度**。它会阅读更多文件、制定详细实施计划，在你批准后才动工。适用于多组件协作任务。
* **Thinking Mode (思考模式)**：专注于**深度**。适用于攻克复杂的逻辑算法、疑难 Debug 或深层的架构设计。

**思考等级 (Reasoning Levels)：**
从基础的 `Think` 到极限的 `Ultrathink`，你可以根据问题的复杂度灵活调整 Claude 的“脑力”投入。

---

## 🛠 开发环境避坑与实战 Tips

### 1. 安全与配置：`.env` 管理
在使用 Anthropic API 时，API Key 是你的核心资产。
* **获取 Key**：前往 [Anthropic Console](https://console.anthropic.com)，Key 只显示一次，务必妥善保存。
* **隐藏文件**：`.env` 在 Mac 下默认隐藏，使用快捷键 `Cmd + Shift + .` 即可切换显示。
* **⚠️ 安全第一**：务必在 `.gitignore` 中添加 `.env`，防止 Key 被推送到公开仓库！

### 2. 常用操作指令
* **退出进程**：运行 `npm run dev` 等持续任务时，使用 `Ctrl + C` 中断。
* **精准引用**：在对话中使用 `@文件名` 快速指引 Claude 查看特定上下文。
* **截图通讯（避坑点）**：
  - 在终端内粘贴截图可以为 Claude 提供视觉参考（如 UI 报错）。
  - **注意：** 在 macOS 上，即使系统快捷键是 Cmd，在 Claude Code 终端内粘贴截图通常需要使用 **`Ctrl + V`**。

### 3. 标准 Git 初始化流程
如果你从零开始建立项目仓库，请遵循以下标准流：

```bash
git init                    # 初始化本地仓库
git status                  # 检查当前文件状态
git add .                   # 将所有更改加入暂存区
git commit -m "Initial"     # 提交第一次快照
git branch -M main          # 强制重命名主分支为 main
git remote add origin <URL>    # 关联远端仓库
git push -u origin main     # 推送并建立跟踪关系
```
