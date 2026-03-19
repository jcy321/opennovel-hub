# 与 Oh My OpenCode 的渊源

## 架构借鉴的三个层次

OpenNovel 对 Oh My OpenCode 的借鉴不是简单的"复制粘贴"，而是三个层次的深入学习和改造。

---

## 第一层：概念映射

| Oh My OpenCode | OpenNovel | 核心职责 |
|----------------|-----------|---------|
| Hephaestus（执行专家） | 执笔（唯一写入者） | 内容生成、严格按照批注执行 |
| Librarian（资料专家） | 调研者（爆点分析） | 外部资料搜索、特征提取 |
| Metis（计划顾问） | 规划者（新书规划） | 需求澄清、计划生成 |
| Momus（质量评审） | 审阅（阅读体验评估） | 质量评估、问题发现 |
| Explore（代码探索） | 知识库检索工具 | 内部信息搜索 |
| Atlas（执行编排器） | 观察者（协作枢纽） | Todo 协调、并行验证 |
| — **OpenNovel 独创** — | **天道（剧情编排器）** | 通读知识库、推演剧情走向、多维分析、伏笔管理 |
| — **OpenNovel 独创** — | **刘和平（人物塑造）** | 人物知识库维护、声音特征管理、一致性检查 |
| — **OpenNovel 独创** — | **世界观守护者** | 世界观规则执行、一致性检查、违规预警 |

> **注**：天道 **不是** Sisyphus 的对应。Sisyphus 是任务分发器（意图分析 → 任务分解 → 委派执行），而天道是剧情编排器（通读知识库 → 推演剧情 → 多维分析 → 确定走向）。天道的核心职责是创造性推演，而非任务调度。

---

## 第二层：机制继承与改造

**IntentGate（意图门控）**：完整继承 4 阶段决策流程，调整分类维度。

**Delegation Protocol（委派协议）**：继承 6 字段结构，扩展 CONTEXT 字段。

**Session Continuity（会话连续性）**：通过 session_id 实现上下文传递。

---

## 第三层：领域适配

| 维度 | OMO | OpenNovel |
|------|-----|-----------|
| **任务性质** | 确定性任务 | 创造性任务 |
| **一致性要求** | 代码逻辑一致性 | 人物、世界观、时间线多维一致性 |
| **时间跨度** | 一次性任务 | 长期协作项目 |
| **Agent 主动性** | 被动响应 | 主动介入 |
| **冲突处理** | 编译错误 | 世界观冲突、人物 OOC |

---

## 关键创新：OMO 没有的东西

**阶段性锁定**：规划者、调研者在特定阶段锁定。

**主动介入 Hook**：Agent 根据内容主动加入讨论。

**剧情压力表**：监控剧情节奏，适时注入意外因素。

**唯一写入者**：只有执笔能输出章节内容。

---

## Hooks 层面对比

| 方面 | Oh My OpenCode | OpenNovel |
|------|---------------|-----------|
| **总数量** | 46 个 | ~12 个核心 |
| **层级结构** | 5 层 | 3 层 |
| **触发方式** | 事件驱动 | 事件驱动 + 内容检测 |
| **主动性** | 响应式 | 响应式 + 前瞻式 |

**OMO 独有的 Hooks**：
- `context-window-monitor`：上下文窗口监控
- `preemptive-compaction`：抢占式压缩
- `hashline-read-enhancer`：哈希行读取增强
- `comment-checker`：注释检查器

**OpenNovel 独有的 Hooks**：
- `phase-lock-check`：阶段锁定检查
- `proactive-intervention`：主动介入
- `foreshadowing-state-check`：伏笔状态检查
- `plot-pressure-check`：剧情压力检查

---

## LSP vs 知识库检索

| 方面 | OMO LSP | OpenNovel Knowledge |
|------|---------|---------------------|
| **数据结构** | AST | Knowledge Graph |
| **查询方式** | 结构化查询 | 向量检索 + 关键词匹配 |
| **精确性** | 编译器级别 | 语义匹配级别 |
| **动态性** | 静态 | 动态更新 |

**OMO 的 LSP 工具**：
- `lsp_goto_definition`：跳转到定义
- `lsp_find_references`：查找引用
- `lsp_symbols`：获取符号

**OpenNovel 的对应工具**：
- `knowledge_search`：知识库检索
- `character_lookup`：人物查询
- `worldview_check`：世界观检查

<!-- OMO_INTERNAL_INITIATOR -->
