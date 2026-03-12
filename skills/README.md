# Game Agents Skills Index

项目内真实存在的共用 skill 索引。`agents/*/SOUL.md` 的 `Skills` 段应只引用这里或 `~/Project/Agents/skills/` 中真实存在的 skill。

## 分层原则

为了遵守渐进式披露，优先按下面顺序加载 skill：

1. 基础能力层：检索、参考、计算
2. 业务执行层：按具体专项调用对应设计 skill
3. 审查裁决层：仅在需要审查、复核、汇总时调用

## 1. 基础能力层

- `explore`
- `librarian`
- `oracle`

## 2. 业务执行层

### 规划与调度
- `intent-recognition`
- `message-triage`
- `chit-chat-handling`
- `game-decomposition`
- `macro-system-planning`
- `task-allocation-strategy`
- `progress-tracking`
- `parallel-dispatch`
- `content-integration`
- `conflict-resolution`

### 市场与叙事
- `market-audience-analysis`
- `selling-point-extraction`
- `aso-analysis`
- `media-buying-pace-analysis`
- `creative-strategy-analysis`
- `bidding-strategy-analysis`
- `competitive-differentiation-analysis`
- `scriptwriting`
- `character-design`

### 战斗 / 关卡 / 玩法 / 系统 / UX
- `behavior-tree-design`
- `combat-feel-design`
- `spatial-flow-design`
- `pacing-design`
- `rules-design`
- `feedback-design`
- `mobile-control-selection`
- `h5-prototype-architecture`
- `system-coupling-analysis`
- `interaction-hierarchy-design`
- `usability-analysis`

### 数值 / 商业化 / 经济 / 运营
- `formula-design`
- `growth-curve-simulation`
- `arpu-ltv-planning`
- `gacha-probability-design`
- `config-table-design`
- `production-consumption-analysis`
- `trading-mechanism-design`
- `schedule-planning`
- `retention-design`

## 3. 审查裁决层

- `standards-gatekeeping`
- `logical-gap-review`
- `risk-identification`
- `system-audit`
- `content-review`
- `experience-review`
- `balance-audit`
- `economy-audit`
- `monetization-audit`
- `review-synthesis`

说明：
- 上述核心审查 skill 已统一补充 `严重级别参考`、`示例发现`、`不要这样报`
- 调用顺序建议为：先看检查表，再看判级参考，最后在需要写结论时参考示例发现

## 使用建议

- 默认不要一次性加载全量 skill，先按任务选最小集合
- 需要事实参考时，先用基础能力层
- 进入专项设计时，再加载对应业务执行层
- 只有当方案要审议、验算、复核、汇总时，才进入审查裁决层
- 若任务目标是“快速做可试玩 H5 手游原型”，可额外加载 `rules/h5-prototype-boundary.md`
