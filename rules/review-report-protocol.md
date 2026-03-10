# 审查上报协议

用于 `game-agents` 项目内所有“审查型输出”的统一结构规范。该协议吸收了 `参考2/reporting_protocol.md` 与合议闭环机制的优点，但仍保持项目内可渐进加载的最小必要版本。

## 适用范围

- 门下省的审议结论与汇总结论
- 各司提交的专项审查意见
- 项目共用审查 skill 的标准输出
- 修复后重审时的轮次追踪

## 协议版本

- 当前版本：`1.1.0`
- 兼容原则：
  - `PATCH`: 说明补充，不影响现有字段
  - `MINOR`: 新增可选字段，旧报告仍可解析
  - `MAJOR`: 结构变更，相关 skill 与门下省规则必须同步更新

## 统一裁决

- `PASS`: 未发现阻塞问题，可继续推进
- `WARN`: 存在需要修正的问题，但不必阻塞整体方向
- `FAIL`: 存在阻塞问题，必须返工或重审
- `SKIP`: 信息不足、超出范围、超时或本轮未参与

### 裁决传播规则

- 任一有效审查结果为 `FAIL`，门下省默认按阻塞项处理
- 若无 `FAIL` 但存在 `WARN`，门下省按保守原则决定是“带注准奏”还是“封驳回修”
- 若所有有效审查均为 `PASS`，可进入 `准奏`
- 若全部为 `SKIP`，不得做强结论，必须说明“信息不足 / 审查未完成”

## 统一严重性

- `CRITICAL`: 立即阻塞，如核心循环断裂、公式崩溃、经济可刷穿
- `HIGH`: 当前迭代必须修正，如成长失衡、路径死锁、严重体验断层
- `MEDIUM`: 应尽快修正，如规则描述不清、局部节奏问题
- `LOW`: 建议修正，如格式、术语、小幅可读性问题
- `INFO`: 观察项或优化建议

### 严重性升级与争议处理

- 两个及以上独立审查源指向同一高风险问题时，可升级严重性
- 乐趣 vs 平衡、完整性 vs 简洁性、创新性 vs 可行性等冲突，允许标记为 `DISPUTED`
- `DISPUTED` 不自动等于 `FAIL`，但若争议触及核心目标、商业风险或基础可行性，门下省应按更保守结论处理

## 成员报告标准结构

```json
{
  "report_meta": {
    "agent_id": "balance-auditor-01",
    "agent_role": "balancing",
    "task_id": "TASK-2026-0306-001",
    "review_round": 1,
    "verdict": "WARN",
    "confidence": 0.84,
    "protocol_version": "1.1.0"
  },
  "scope": {
    "target": "某功能方案",
    "coverage": "成长曲线与概率池",
    "excluded": null
  },
  "findings": [
    {
      "id": "BA-001",
      "severity": "HIGH",
      "category": "成长曲线异常",
      "location": "第4章 成长表",
      "title": "中后期膨胀过快",
      "description": "80级后属性倍率跃升过大，导致前序养成线快速失效。",
      "suggestion": "改为分段成长或 S 曲线，并补充 1/30/80/满级四个关键节点验算。",
      "evidence": "Lv80->Lv81 攻击提升 18%，远高于前段 3%~5%",
      "disputed": false
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 0,
    "high_count": 1,
    "medium_count": 0,
    "low_count": 0,
    "info_count": 0,
    "key_points": [
      "成长曲线在后段出现不可控膨胀"
    ],
    "recommendation": "先修正成长曲线，再继续扩展后期内容。"
  }
}
```

## 汇总结论扩展字段

门下省或汇总型 skill 在合并多司结果时，可在标准结构上附加以下字段：

```json
{
  "summary": {
    "deduplicated_count": 2,
    "disputed_count": 1,
    "priority_actions": [
      "先修正经济套利闭环",
      "再统一成长曲线与文案描述"
    ]
  },
  "aggregate_meta": {
    "agents_participated": ["economy", "balancing", "ux"],
    "agents_skipped": ["combat"],
    "stale_reports_dropped": 1,
    "max_review_rounds": 3
  }
}
```

## 轮次与过期报告规则

- 所有审查报告必须带 `review_round`
- 当前轮次之外的旧报告视为 `stale report`，不得混入本轮裁决
- 若某 Agent 超时、失败或本轮未参与，使用 `SKIP` 并在 `scope.excluded` 或汇总元数据中说明原因
- 默认最大修复-重审轮次：`3`

## 前缀约定

- `SA`: 系统/结构审查
- `CR`: 内容/规则/术语审查
- `EV`: 体验/流程/心流审查
- `BA`: 数值/平衡审查
- `EA`: 经济系统审查
- `MR`: 商业化/付费公平性审查
- `MX`: 门下省汇总结论
- `DF`: 修复动作或修复报告

## 使用规则

1. 审查型技能只输出结构化结果，不在协议层塞入长篇解释。
2. `HIGH` 及以上问题应尽量附 `evidence`；无证据时必须降低置信度或说明前提。
3. 门下省汇总多司意见时，先去重，再按最保守结论输出。
4. 若只是项目内部快速评审，可省略部分计数字段，但字段命名保持一致。
5. 当进入修复闭环时，必须保留 `review_round`、`agents_participated`、`agents_skipped` 和 `priority_actions`。
