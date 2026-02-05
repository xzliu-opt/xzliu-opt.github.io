---
title: 'Claude Code 进阶：会话深度控制与 MCP 扩展'
date: 2026-02-04
tags:
  - Claude Code
  - Vibe Coding
  - AI Tooling
  - MCP
---

在掌握了 Claude Code 的基础起步后，如何在高强度的开发中保持 AI 的状态“不掉线”？本篇将深入探讨 Claude Code 的进阶操控技巧，包括会话管理、自定义指令以及赋予 AI 外部能力的 MCP 协议。

---

## ⚡️ 精准会话控制：拒绝上下文迷失

在长会话中，AI 可能会因为过多的历史信息而变得迟钝或出现理解偏差。学会这几招可以极大提升协作效率：

### 1. 即时干预快捷键
* **`Esc`**：立即停止当前的响应。当你发现 Claude 的方向偏离预期时，果断按 Esc 止损。
* **双击 `Esc`**：在特定状态下快速重置输入或响应 UI 切换。
* **`#` 快捷键**：进入 **Memory Mode**。你可以直接输入对开发规范的修正（例如：`# 永远使用 Tailwind 代替 CSS`），Claude 会智能更新对应的配置文件。

### 2. 会话管理指令
* **`/compact`**：**上下文重整**。它会总结对话至今的核心信息，保留 Claude 学到的知识并释放 Token 空间。
    * *适用场景：* 对话已经很长，感觉 Claude 反应变慢时。
* **`/clear`**：**彻底重置**。删除所有对话历史。
    * *适用场景：* 准备切换到一个完全不相关的新任务，防止旧的上下文干扰。

---

## 🛠 自定义指令：构建你的 AI 工作流

Claude Code 允许你为项目量身定制“斜杠指令”。只需通过简单的 Markdown 文件即可定义复杂的任务流。

### 配置流程
1. 在项目根目录找到 `.claude/` 文件夹。
2. 在其中创建 `commands` 文件夹。
3. 新建一个 `.md` 文件（文件名即为指令名）。

**项目结构示例：**
```text
.claude/
└── commands/
    └── audit.md  <-- 此时你就可以在 Claude 中输入 /audit
在 audit.md 中，你可以用自然语言描述该指令的行为，例如：“检查当前修改的代码是否符合团队的 Lint 规范，并生成一份简要报告”。
```

## 🔌 MCP：赋予 Claude “感知与行动”
MCP (Model Context Protocol) 是 Claude Code 的核心扩展机制。它像插件一样，允许 Claude 调用你本地或远程的工具，例如访问数据库或操作浏览器。

实战：安装 Playwright 浏览器扩展
如果你希望 Claude 能够自动打开浏览器、截图并分析页面 UI，可以安装 Playwright MCP 服务器。

在系统终端运行（注意：不是在 Claude 内部）：

Bash
claude mcp add playwright npx @playwright/mcp@latest
安装完成后，你可以直接指挥 Claude：“打开本地 3000 端口，看看登录页面的布局是否有误”，它会调用浏览器并基于视觉渲染结果进行分析。

## 🌿 结语
从基础的代码补全到深度的环境接入，Claude Code 正在重新定义我们与代码库交互的方式。合理利用 /compact 保持清醒，通过 MCP 扩展能力边界，这才是 Vibe Coding 的完全体形态。