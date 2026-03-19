# OpenNovel

> **像AI编程一样AI协作写小说**
>
> 一个由8个专业Agent组成的多智能体小说创作系统，通过群聊协作模式，让AI像真人创作团队一样共同编织精彩的故事。

---

## 项目简介

OpenNovel 是一个创新的多 Agent 小说创作协作系统。它借鉴了 AI 编程工具（如 Oh My OpenCode）的成功经验，将"专业分工"理念引入小说创作领域。

### 核心理念

> **小说是由世界观、人物、剧情等要素动态驱动的小世界，命运在其中交汇、编织。**

---

## 🌐 多客户端支持

OpenNovel 支持三种客户端接入方式：

### 使用方式

| 模式 | 命令 | 端口 | 客户端 |
|------|------|------|--------|
| **IDE 模式** (默认) | `opennovel` | 6688 | OpenNovel IDE 桌面客户端 |
| **Web 模式** | `opennovel --web` 或 `opennovel -w` | 80 | 浏览器 |
| **扩展模式** | `opennovel --ext` 或 `opennovel -e` | 6689 | VS Code + opennovel 插件 |

### 架构示意

```
┌─────────────────────────────────────────────────────────────┐
│                    部署机 (后端 opencore)                    │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐  │
│   │              opennovel 后端服务                      │  │
│   │  ┌─────────┐  ┌─────────┐  ┌─────────────────────┐  │  │
│   │  │ IDE端口 │  │ Web端口 │  │ Extension端口       │  │  │
│   │  │  :6688  │  │  :80    │  │  :6689              │  │  │
│   │  └────┬────┘  └────┬────┘  └─────────┬───────────┘  │  │
│   └───────┼────────────┼─────────────────┼──────────────┘  │
│           │            │                 │                  │
└───────────┼────────────┼─────────────────┼──────────────────┘
            │            │                 │
   ┌────────┴───┐  ┌─────┴─────┐   ┌──────┴──────┐
   │ opennovel  │  │  浏览器   │   │ VS Code +   │
   │ -ide 客户端│  │  (Web)    │   │ opennovel   │
   │ (Electron) │  │           │   │ 插件        │
   └────────────┘  └───────────┘   └─────────────┘
```

---

## 📦 仓库结构

| 仓库 | 说明 | 语言/框架 |
|------|------|----------|
| [opennovel-core](https://github.com/jcy321/opennovel-core) | 后端服务 | Rust + Axum |
| [opennovel-web](https://github.com/jcy321/opennovel-web) | Web 前端 | SvelteKit |
| [opennovel-ide](https://github.com/jcy321/opennovel-ide) | 桌面客户端 | VS Code (Electron) |
| [opennovel-hub](https://github.com/jcy321/opennovel-hub) | 项目主页 (本仓库) | - |

---

## 🤖 八大 Agent 设计

| Agent | 职责 | 可用阶段 |
|-------|------|---------|
| **规划者** | 新书规划、头脑风暴 | 构思中 |
| **天道** | 剧情推演、伏笔管理 | 撰写中 |
| **刘和平** | 人物塑造、一致性维护 | 撰写中 |
| **世界观守护者** | 规则检查、一致性验证 | 撰写中 |
| **执笔** | 内容撰写、批注执行 | 撰写中 |
| **审阅** | 质量评估、阅读体验 | 撰写中 |
| **观察者** | 知识库管理、Agent协调 | 全阶段 |
| **调研者** | 市场研究、爆点分析 | 知识库建立 |

---

## ✨ 核心特性

### 群聊协作模式

每本书 = 一个群聊，所有交互在群内完成：
- **透明性**：所有 Agent 的思考过程对用户可见
- **实时性**：SSE 流式输出，用户能看到 Agent "正在思考"
- **可追溯**：完整的对话历史，方便回顾和调试

### 阶段性锁定

创作分为三个阶段，某些 Agent 只在特定阶段可用：
- **阶段一（构思）**：规划者与用户私密对话
- **阶段二（知识库建立）**：调研者分析爆点，观察者建立知识库
- **阶段三（撰写）**：天道编排剧情，执笔撰写内容

### 唯一写入者

只有一个 Agent（执笔）能输出章节内容，其他 Agent 只能提供批注，确保：
- 风格统一
- 责任清晰
- 冲突可追溯

### 主动介入 Hook

Agent 可以根据内容主动加入讨论，例如：
- 世界观守护者检测到设定冲突时主动预警
- 天道检测到伏笔压力过高时建议触发
- 刘和平检测到人物 OOC 时提出修正建议

---

## 🚀 快速开始

### 1. 安装后端

```bash
# 克隆仓库
git clone https://github.com/jcy321/opennovel-core.git
cd opennovel-core

# 构建
cargo build

# 运行 (IDE 模式，端口 6688)
cargo run -p opennovel-web
```

### 2. 选择客户端

**方式一：Web 模式**

```bash
# 启动后端 (Web 模式)
cargo run -p opennovel-web -- --web

# 浏览器访问 http://localhost:80
```

**方式二：IDE 模式**

```bash
# 启动后端 (IDE 模式)
cargo run -p opennovel-web

# 启动 opennovel-ide 客户端并连接
```

**方式三：扩展模式**

```bash
# 启动后端 (扩展模式)
cargo run -p opennovel-web -- --ext

# 在 VS Code 中安装 opennovel 插件并连接
```

---

## 致谢

本项目的架构设计和实现思路深受以下两个开源项目的启发：

### [@OpenCode](https://github.com/opencode-ai/opencode)

OpenCode 是一个强大的 AI 编程助手，其 Agent 系统设计、工具链集成和会话管理机制为本项目提供了宝贵参考。

### [@Oh My OpenCode](https://github.com/code-yeongyu/oh-my-openagent)

Oh My OpenCode 是一个功能丰富的 AI 开发环境，其 Hooks 系统、Skills 架构、Intent Gate 决策流程和 Session Continuity 机制为 OpenNovel 提供了核心架构灵感。

---

## 📄 许可证

本项目采用 **AGPL-3.0** 许可证开源。

```
Copyright (C) 2024-2026 OpenNovel Team

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.
```

详见 [LICENSE](LICENSE) 文件。