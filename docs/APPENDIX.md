# 附录：技术实现细节

## 一、Intent Gate 完整实现

Intent Gate 是 OpenNovel 的核心决策机制，继承自 Oh My OpenCode 的四阶段决策模型。

### 四阶段决策

1. **Phase 0: 意图口语化**：将用户输入转化为结构化的意图表示
2. **Phase 1: 请求分类**：将请求分为 Trivial/Explicit/Exploratory/OpenEnded/Ambiguous
3. **Phase 2: 模糊检查**：检测是否存在多种解释
4. **Phase 3: 验证**：验证假设和条件

### 关键规则

- 多种解释、工作量差异 < 2x → 使用合理默认值
- 多种解释、工作量差异 ≥ 2x → **必须询问用户**
- 缺少关键信息 → **必须询问用户**

---

## 二、Delegation Protocol 完整规范

委派协议是 Agent 之间协作的核心机制。每次委派必须包含完整的 6 个字段。

### 6 字段结构

| 字段 | 说明 |
|------|------|
| **TASK** | 任务描述：原子化、具体目标 |
| **EXPECTED OUTCOME** | 预期输出：可量化的验收标准 |
| **REQUIRED TOOLS** | 必需工具：工具白名单 |
| **MUST DO** | 必须执行：穷尽要求 |
| **MUST NOT DO** | 禁止执行：预判可能的越界 |
| **CONTEXT** | 上下文：决策所需的所有信息 |

---

## 三、知识库系统详解

OpenNovel 维护七个知识库：

| 知识库 | 用途 | 主要维护者 |
|--------|------|-----------|
| 世界观知识库 | 世界规则、概念、地点 | 世界观守护者 |
| 历史情节知识库 | 已完成章节摘要 | 观察者 |
| 本章知识库 | 当前章节规划 | 天道 |
| 人物信息知识库 | 人物属性、关系、声音 | 刘和平 |
| 阵营派系势力库 | 势力关系 | 观察者 |
| 地图知识库 | 地理信息 | 观察者 |
| 伏笔知识库 | 伏笔状态、压力表 | 天道 |

---

## 四、权限矩阵

### 权限级别

- **None**：无权限
- **Read**：只读
- **Write**：读写
- **Manage**：管理（创建/更新/删除）

### 关键权限规则

- 天道：读写世界观、伏笔
- 刘和平：读写人物
- 世界观守护者：读写世界观
- 执笔：只读所有知识库
- 观察者：管理所有知识库

---

## 五、Session Continuity 实现细节

### 会话管理器

```rust
pub struct SessionContinuityManager {
    sessions: HashMap<SessionId, SessionState>,
    parent_child_map: HashMap<SessionId, Vec<SessionId>>,
}
```

### 继续规则

| 场景 | 处理方式 |
|------|---------|
| 任务失败/不完整 | 使用 session_id 继续 |
| 对结果有后续问题 | 使用 session_id 继续 |
| 与同一 Agent 多轮对话 | 永远不要重新开始新会话 |
| 验证失败 | 使用 session_id 修复 |
```