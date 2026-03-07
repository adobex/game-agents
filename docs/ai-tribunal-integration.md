# AI Tribunal Design 吸收记录

本文记录 `Downloads/ai_tribunal_design` 中哪些内容被 `game-agents` 学习与借鉴，以及如何按渐进式披露落地。

## 已吸收的部分

### 1. 文档结构写法

以下结构被采纳为参考模板：

- 角色身份
- 核心职责
- 不负责什么
- 检查清单
- 严重性分级
- 统一输出协议

这些结构适合做“方法论文档”或“项目共用 skill”，因为可读性强、边界清楚、便于多人协作。

### 2. 方法论骨架

- `system_architect.md` → 系统边界、耦合、状态机、扩展性
- `content_reviewer.md` → 规则一致性、参数完整性、术语统一
- `experience_validator.md` → 玩家旅程、心流、认知负荷、目标感
- `balance_auditor.md` → 公式边界、成长曲线、概率、经济、付费公平
- `orchestrator.md` / `aggregator_judge.md` / `design_fixer.md`
  → 门下省的多维汇总、保守裁决、有限轮次重审

### 3. 协议意识

已转化为项目共用规则：

- `rules/review-report-protocol.md`

它统一了：

- verdict
- severity
- findings 结构
- 审查前缀

## 没有直接照搬的部分

### 1. 没有新增一套平行 Agent 组织

`game-agents` 仍然使用：

- 太子
- 三省
- 11 司

`ai_tribunal_design` 被当成“专业审查镜头”，而不是一套替代组织。

### 2. 没有把长文塞进单个 SOUL

为了遵循渐进式披露：

- `SOUL.md` 只保留角色最需要知道的调用关系
- 冗长的检查表与协议，统一下沉到 `skills/` 与 `rules/`
- 需要时再按需加载，而不是默认全部注入上下文

### 3. 没有照搬其全部示例与字段

原始文档示例很丰富，但对当前项目来说过长。  
因此仅保留“高频、必要、能落地”的字段与流程。

## 当前映射结果

| 来源文档 | 当前落点 |
|---|---|
| `system_architect.md` | `skills/system-audit.md`，并接入系统司/战斗司 |
| `content_reviewer.md` | `skills/content-review.md`，并接入叙事司/玩法司 |
| `experience_validator.md` | `skills/experience-review.md`，并接入玩法司/关卡司/UX司/运营司 |
| `balance_auditor.md` | `skills/balance-audit.md`、`skills/economy-audit.md`、`skills/monetization-audit.md` |
| `reporting_protocol.md` | `rules/review-report-protocol.md` |
| `orchestrator.md` + `aggregator_judge.md` + `design_fixer.md` | `skills/review-synthesis.md`，并接入门下省 |

## 各 Agent 的吸收方向

| Agent | 吸收方向 |
|---|---|
| 太子 | 参考内容审查的“需求表述清晰度”，但只保留立项清洗能力 |
| 中书省 | 参考系统审查的“模块边界与依赖意识”，用于提升规划质量 |
| 门下省 | 重点吸收编排、汇总、保守裁决、有限重审思想 |
| 尚书省 | 参考编排与汇总逻辑，强化多司整合与冲突协调 |
| 定位司 | 参考体验与内容视角，提升用户画像与卖点论证清晰度 |
| 叙事司 | 参考内容审查，强化术语统一、设定一致性 |
| 战斗司 | 参考系统审查 + 平衡审计，强化状态机、公式和流派平衡 |
| 关卡司 | 参考体验验证，强化路径引导与节奏结构 |
| 玩法司 | 参考内容审查 + 体验验证，强化规则闭环和玩家旅程 |
| 系统司 | 重点吸收系统审查的边界、数据归属、扩展性检查 |
| UX司 | 重点吸收体验验证的流程、负荷、可用性检查 |
| 数值司 | 重点吸收平衡审计的公式、成长、概率与边界验算 |
| 付费司 | 吸收平衡审计中的付费公平性与保底概率部分 |
| 经济司 | 吸收平衡审计中的经济闭环、通胀和套利部分 |
| 运营司 | 吸收体验验证中的长期目标感、留存与节奏校验 |

## 后续可继续吸收的方向

1. 为门下省补一份“重审轮次控制”规则。
2. 给尚书省增加“多司意见冲突整合”的轻量版协议。
3. 给各审查 skill 补一份最小示例输出。
