# Agent Spec Map

用于快速查看各 Agent 的上游输入、标准输出、核心交付物与主要技能。

| Agent | 上游输入 | 标准输出 | 核心交付物 | 主要 Skills |
|---|---|---|---|---|
| `taizi` | 原始需求、闲聊、约束 | 《立项旨意书》或直回 | 意图分类、旨意书、澄清问题 | `intent-recognition` `message-triage` |
| `zhongshu` | 太子旨意书 | 《宏观规划大纲》 | 核心体验、系统树、任务拆解 | `game-decomposition` `macro-system-planning` |
| `menxia` | 旨意书 + 规划大纲 | 《审议结论》 | 准奏/封驳、阻塞问题、回修建议 | `standards-gatekeeping` `logical-gap-review` |
| `shangshu` | 准奏方案 + 批注 | 《派工单》/《整合奏折》 | 任务包、依赖表、整合稿 | `parallel-dispatch` `content-integration` |
| `positioning` | 市场与题材任务包 | 《定位报告》 | 用户画像、竞品对照、卖点 | `librarian` `market-audience-analysis` |
| `analyst` | 情报任务包 | 《发行复盘报告》 | ASO、渠道节奏、素材、出价、差异化 | `aso-analysis` `media-buying-pace-analysis` |
| `narrative` | 叙事任务包 | 《叙事方案》 | 世界观、剧情、角色卡 | `explore` `scriptwriting` |
| `combat` | 战斗任务包 | 《战斗机制方案》 | 战斗闭环、行为树、风险 | `behavior-tree-design` `combat-feel-design` |
| `level` | 关卡任务包 | 《关卡方案》 | 地图拓扑、资源分布、节奏 | `librarian` `spatial-flow-design` |
| `gameplay` | 玩法任务包 | 《玩法方案》 | 规则集、反馈闭环、变体 | `rules-design` `feedback-design` |
| `systems` | 系统任务包 | 《系统设计方案》 | 模块边界、状态机、耦合风险 | `system-coupling-analysis` `system-audit` |
| `ux` | UX 任务包 | 《交互与界面方案》 | 界面层级、关键路径、易用性建议 | `interaction-hierarchy-design` `usability-analysis` |
| `balancing` | 数值任务包 | 《数值模型方案》 | 公式、成长曲线、验算 | `formula-design` `growth-curve-simulation` |
| `monetization` | 商业化任务包 | 《商业化方案》 | 付费矩阵、抽卡/通行证、收益假设 | `arpu-ltv-planning` `gacha-probability-design` |
| `economy` | 经济任务包 | 《经济循环方案》 | 货币闭环、交易规则、通胀预警 | `production-consumption-analysis` `trading-mechanism-design` |
| `liveops` | 运营任务包 | 《运营排期方案》 | 活动日历、留存方案、KPI 假设 | `schedule-planning` `retention-design` |

## 使用方式

- 立项阶段：先看 `taizi`、`zhongshu`、`menxia`、`shangshu`
- 专项展开：按具体议题选择对应 11 司
- 文档维护：更新 `SOUL.md` 时同步检查本表与 `skills/README.md`
