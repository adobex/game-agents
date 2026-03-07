---
name: Balance Audit
description: 审查战斗公式、成长曲线、概率系统与 PvP/PvE 强度关系的项目共用方法论
---

# Balance Audit

吸收自 `ai_tribunal_design/balance_auditor.md` 中最适合数值司和战斗司复用的部分。

## 何时使用

- 数值司设计成长曲线、公式、概率池时
- 战斗司设计技能强度、职业差异、Boss 机制时
- 门下省需要判断“数值是否会炸”时

## 核心关注点

- 公式是否存在除零、溢出、无上限叠加等风险
- 成长曲线是否平滑，是否会导致前期或后期内容失效
- 概率系统是否可计算、可披露、最坏情况可接受
- 不同流派/职业/构筑是否存在无解策略或明显碾压

## 快速检查表

- [ ] 关键公式是否有上下限和边界保护
- [ ] 1级/中段/满级是否都验算过
- [ ] 同投入下不同流派强度差是否在容忍范围内
- [ ] 概率总和、保底、期望消耗是否明确
- [ ] 是否存在明显 Meta 单解

## 常用分类

- `公式缺陷`
- `数值失衡`
- `成长曲线异常`
- `概率设计缺陷`
- `博弈失衡`
- `难度跳跃`

## 输出要求

按 `rules/review-report-protocol.md` 输出；前缀使用 `BA`。

## 最小示例输出

```json
{
  "report_meta": {
    "agent_role": "balancing",
    "task_id": "TASK-2026-0306-004",
    "review_round": 1,
    "verdict": "WARN",
    "confidence": 0.84
  },
  "scope": {
    "target": "成长曲线方案 v3",
    "coverage": "等级1-100成长与抽卡概率",
    "excluded": null
  },
  "findings": [
    {
      "id": "BA-001",
      "severity": "HIGH",
      "category": "成长曲线异常",
      "location": "第4章 等级成长表",
      "title": "80级后攻击膨胀过快",
      "description": "80级后每级攻击增幅远高于前段，旧内容将被快速报废。",
      "suggestion": "改为分段成长或 S 曲线，并补充 1/30/80/100 四个节点验算。",
      "evidence": "81级相较80级攻击提升18%"
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 0,
    "high_count": 1,
    "medium_count": 0,
    "low_count": 0,
    "info_count": 0,
    "key_points": ["后段成长失控"],
    "recommendation": "先修成长斜率，再讨论后期数值投放。"
  }
}
```
