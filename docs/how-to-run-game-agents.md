# How To Run Game Agents

用于指导如何把一个真实游戏设计需求送入 `game-agents` 系统，并得到可汇总、可审议、可派发的结果。

## 使用原则

- 先从 `taizi` 入口进入，不直接跳过总控
- 大需求先经过 `zhongshu` -> `menxia` -> `shangshu`
- 11 司只处理自己的专项，不越权包办全案
- 需要审查时，再按需调用项目共用 audit skill
- 所有正式产物尽量遵循 `docs/output-templates.md`
- 需要判断当前卡在哪个节点、是否该回退时，查看 `docs/workflow-state-machine.md`

## 标准运行流程

1. `taizi`
- 接收原始需求
- 判断是闲聊、澄清还是正式立项
- 输出《立项旨意书》

2. `zhongshu`
- 把旨意拆成核心体验、系统树和任务包
- 输出《宏观规划大纲》

3. `menxia`
- 审核是否偏离目标、逻辑断裂或越权
- 输出《审议结论》

4. `shangshu`
- 将准奏方案拆成面向 11 司的任务包
- 输出《派工单》

5. 11 司并行执行
- 各司输出自己的专项方案
- 回传 `shangshu`

6. `shangshu` 汇总
- 整合、去重、处理冲突
- 输出《整合奏折》

7. 必要时复核
- 高风险方案可再过 `menxia`
- 专项风险可调用 audit skill

## 什么时候调用哪个 Agent

### 起步阶段
- 需求还乱：`taizi`
- 已经要做系统骨架：`zhongshu`
- 需要裁决和把关：`menxia`
- 需要分工与整合：`shangshu`

### 专项展开阶段
- 市场、受众、卖点：`positioning`
- 世界观、剧情、角色：`narrative`
- 战斗机制、敌兵行为：`combat`
- 地图拓扑、流程推进：`level`
- 非战斗玩法循环：`gameplay`
- 外围系统与模块边界：`systems`
- 界面层级与易用性：`ux`
- 公式、成长、概率：`balancing`
- 商业化结构：`monetization`
- 经济闭环与交易：`economy`
- 活动排期、促活留存：`liveops`

## 什么时候必须审查

以下情况建议进入审查流：

- 方案跨多个司且耦合复杂
- 涉及经济、付费、概率等高敏感内容
- 方案存在明显争议或体验风险
- 进入对外汇报或正式立项前

推荐调用：
- 系统边界：`system-audit`
- 文案与规则清晰度：`content-review`
- 玩家体验：`experience-review`
- 数值平衡：`balance-audit`
- 经济健康：`economy-audit`
- 商业化压力：`monetization-audit`
- 多审查汇总：`review-synthesis`

## 一个最小示例

```markdown
需求：做一款末日题材 SLG，要求长线经营、联盟协作、可做商业化。

1. `taizi` 输出《立项旨意书》
2. `zhongshu` 输出《宏观规划大纲》
3. `menxia` 判断是否准奏
4. `shangshu` 派给 `positioning` `gameplay` `systems` `economy` `monetization`
5. 各司回传专项方案
6. `shangshu` 输出《整合奏折》
7. 对经济与付费部分补 `economy-audit` / `monetization-audit`
```

## 常见误用

- 误用 1：直接让 `combat` 设计整个游戏框架
- 误用 2：让 `economy` 决定剧情和角色表达
- 误用 3：跳过 `menxia`，未经审议直接派发重大方案
- 误用 4：所有 skill 一次性全加载，违背渐进式披露
- 误用 5：不输出正式产物模板，只给散乱建议
