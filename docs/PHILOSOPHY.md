# 设计哲学：小说是一个小世界

## 核心信条

> **小说是由世界观、人物、剧情等要素动态驱动的小世界，命运在其中交汇、编织。**

这句话不是文学修辞，而是技术设计的核心指导思想。它决定了 OpenNovel 的每一个架构决策。

---

## 世界观：规则引擎，而非静态设定

在传统 AI 写作工具中，世界观只是一段文本描述。AI 可能会阅读它，也可能忘记它。当 AI 生成内容时，世界观只是"背景信息"，没有强制的约束力。

在 OpenNovel 中，世界观是一个**规则引擎**：

```rust
pub struct WorldviewRule {
    pub rule_id: String,
    pub description: String,
    pub scope: RuleScope,
    pub violation_action: ViolationAction,
    pub examples: Vec<RuleExample>,
}
```

当执笔 Agent 尝试让古代人物说网络流行语时，世界观守护者会检测到违规，并在群内发出警告。这不是简单的"提醒"，而是系统级的规则执行。

---

## 人物：智能体，而非纸片人

在 OpenNovel 中，每个人物是一个**智能体**，有持续维护的状态：

```rust
pub struct Character {
    pub id: String,
    pub name: String,
    pub attributes: HashMap<String, serde_json::Value>,
    pub relationships: Vec<CharacterRelationship>,
    pub voice_profile: Option<VoiceProfile>,
    pub timeline_states: HashMap<String, CharacterState>,
}
```

刘和平 Agent 维护这个 `CharacterDB`，确保每个人物在不同阶段有连贯的行为逻辑。

---

## 剧情：确定性框架内的随机性

在 OpenNovel 中，剧情是**确定性和随机性的平衡**：

```rust
pub struct PlotPressureGauge {
    pub pressure: f32,  // 0-100
    pub foreshadowing_priority: Vec<ForeshadowingId>,
}
```

天道 Agent 管理这个"剧情压力表"。当连续多章没有意外因素时，压力会累积，最终触发一个伏笔或生成一个意外事件。

---

## 设计原则总结

| 原则 | 说明 |
|------|------|
| **世界观即规则** | 不是静态文本，而是可执行的规则引擎 |
| **人物即智能体** | 每个人物有独立的状态和行为逻辑 |
| **剧情即平衡** | 在确定性和随机性之间保持张力 |
| **协作即对话** | Agent 通过群聊协作，过程透明 |
| **介入即主动** | Agent 可以主动发现问题并提出建议 |
