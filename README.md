# Game Agents

该项目用于规划和设计游戏开发中的各类 Agent。我们旨在通过不同类型的智能代理（Agents）来协助、增强甚至自动化游戏设计与开发流程。

本项目基于“三省六部制”理念，构建了一个**制度化、可控、有审核机制**的多 Agent 协作游戏策划系统。

## 目录结构

- `docs/` - 存放架构设计、规划文档以及研究记录。
  - [架构规划文档 (architecture-plan.md)](./docs/architecture-plan.md)
  - [AI Tribunal 吸收记录 (ai-tribunal-integration.md)](./docs/ai-tribunal-integration.md)
  - [Agent 规格总览 (agent-spec-map.md)](./docs/agent-spec-map.md)
  - [输出模板 (output-templates.md)](./docs/output-templates.md)
  - [功能设计模板 (feature-design-template.md)](./docs/feature-design-template.md)
  - [状态机协议 (workflow-state-machine.md)](./docs/workflow-state-machine.md)
  - [审查修复闭环 (review-repair-loop.md)](./docs/review-repair-loop.md)
  - [运行入口 (how-to-run-game-agents.md)](./docs/how-to-run-game-agents.md)
  - [轻量入口提示词 (quickstart-prompt.md)](./docs/quickstart-prompt.md)
- `skills/` - **(项目共用)** 存放当前项目内跨 Agent 复用的具体业务 Skill。
  - 基础检索与计算：`explore.md`、`librarian.md`、`oracle.md`
  - 审查方法论：`system-audit.md`、`content-review.md`、`experience-review.md`、`balance-audit.md`、`economy-audit.md`、`monetization-audit.md`、`review-synthesis.md`
  - 业务执行 skill 已按各 Agent 能力补齐，详见 [技能索引 (skills/README.md)](./skills/README.md)
  - 技能索引已重构为基础能力层 / 业务执行层 / 审查裁决层，便于渐进式披露
  - 已补充配置表设计专项 skill：`config-table-design.md`
  - 已吸收 H5 原型相关能力：`mobile-control-selection.md`、`h5-prototype-architecture.md`
  - 已补充发行复盘相关能力：`aso-analysis.md`、`media-buying-pace-analysis.md`、`creative-strategy-analysis.md`、`bidding-strategy-analysis.md`、`competitive-differentiation-analysis.md`
- `rules/` - **(项目共用)** 存放当前游戏项目的具体设计规则、编码标准等。
  - 现已包含：`review-report-protocol.md`（统一审查上报协议）、`progressive-disclosure.md`（渐进式披露规则）、`agent-spec-contract.md`（Agent 规格契约）
  - 审查协议已增强：支持轮次追踪、争议标记、过期报告剔除与优先修复动作
  - 已补充 H5 原型边界规则：`h5-prototype-boundary.md`
  - 已补充市场情报协议：`market-intelligence-protocol.md`
- `agents/` - 存放具体各类 Agent 的设计草案、Prompt 模板和专有规则。
  - **总控入口**：`taizi/` (太子)
  - **三省大脑**：`zhongshu/` (中书省), `menxia/` (门下省), `shangshu/` (尚书省)
  - **市场情报支持**：`analyst/` (发行复盘 / 市场情报)
  - **11司执行层**：
    - `positioning/` (定位司)
    - `narrative/` (叙事司)
    - `combat/` (战斗司)
    - `level/` (关卡司)
    - `gameplay/` (玩法司)
    - `systems/` (系统司)
    - `ux/` (UX 司)
    - `balancing/` (数值司)
    - `monetization/` (付费司)
    - `economy/` (经济司)
    - `liveops/` (运营司)
- `scripts/` - 存放用于测试或辅助运行的脚本工具。

## 目标与愿景

探索在游戏设计的不同阶段（如世界观构建、关卡设计、NPC行为逻辑规划、数值平衡等）如何应用各种专用的 Agent，利用意图分拣 $\rightarrow$ 方案起草 $\rightarrow$ 质量审核 $\rightarrow$ 派发调度 $\rightarrow$ 专职并行执行的工作流，大幅提升游戏设计的效率和质量。
