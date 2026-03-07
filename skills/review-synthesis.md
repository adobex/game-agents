---
name: Review Synthesis
description: 门下省使用的项目共用汇总方法论，用于合并多司审查意见、输出封驳/准奏结论并控制重审轮次
---

# Review Synthesis

吸收自 `orchestrator.md`、`aggregator_judge.md`、`design_fixer.md` 的核心思想，但压缩为门下省可直接调用的项目级方法论。

## 何时使用

- 门下省对中书省大纲进行综合审核时
- 门下省对多个司的回传意见进行归并时
- 尚书省需要对跨司冲突进行整理时

## 核心流程

1. 按维度并行收集意见：结构、内容、体验、数值/经济
2. 对重复问题去重，保留更高严重性
3. 若任一阻塞问题为 `FAIL`，默认输出保守结论
4. 只在影响范围明确时建议局部重审，避免全量重跑
5. 超过约定轮次后停止循环，转人工裁定

## 快速检查表

- [ ] 是否已覆盖关键维度，而不是只看单点
- [ ] 是否把重复问题合并了
- [ ] 是否明确哪些问题阻塞、哪些问题可后置
- [ ] 是否给出下一步动作，而不是只给结论
- [ ] 是否控制了返工轮次

## 输出要求

- 门下省汇总结论前缀使用 `MX`
- 结构遵循 `rules/review-report-protocol.md`
- 最终只输出三种动作：`准奏`、`封驳`、`需人工裁定`

## 最小示例输出

```json
{
  "report_meta": {
    "agent_role": "menxia",
    "task_id": "TASK-2026-0306-007",
    "review_round": 1,
    "verdict": "FAIL",
    "confidence": 0.87
  },
  "scope": {
    "target": "战斗系统总方案",
    "coverage": "结构、体验、数值汇总结论",
    "excluded": null
  },
  "findings": [
    {
      "id": "MX-001",
      "severity": "HIGH",
      "category": "综合阻塞",
      "location": "门下省汇总结论",
      "title": "成长曲线与新手旅程同时存在阻塞问题",
      "description": "数值侧存在后段膨胀，体验侧存在前5分钟目标缺失，当前方案不宜直接准奏。",
      "suggestion": "先修正前期目标牵引与成长斜率，再重新提交审议。",
      "evidence": "汇总 BA-001 与 EV-001"
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 0,
    "high_count": 1,
    "medium_count": 0,
    "low_count": 0,
    "info_count": 0,
    "key_points": ["存在跨维度阻塞问题"],
    "recommendation": "封驳，并要求局部返工后重审。"
  }
}
```
