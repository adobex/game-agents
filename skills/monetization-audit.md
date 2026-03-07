---
name: Monetization Audit
description: 审查付费公平性、抽卡概率、保底机制与商业化包装边界的项目共用方法论
---

# Monetization Audit

吸收自 `ai_tribunal_design/balance_auditor.md` 中“付费公平性 + 概率系统”相关部分，供付费司、经济司、数值司复用。

## 何时使用

- 付费司设计首充、礼包、通行证、抽卡时
- 经济司检查商业化是否冲击经济闭环时
- 数值司验证付费成长与免费成长差距时

## 核心关注点

- 付费是否只是加速，还是直接突破上限
- 抽卡概率、保底、最坏情况消耗是否透明合理
- 商业化是否破坏 PvP/PvE 公平和长期留存
- 是否存在隐性付费墙、概率陷阱或过度负面舆情风险

## 快速检查表

- [ ] 是否存在不可弥合的付费碾压
- [ ] SSR/稀有物的概率、软硬保底是否明示
- [ ] 免费玩家是否有长期但可达的追赶路径
- [ ] 商业化活动是否破坏核心玩法节奏
- [ ] 用户心理预期与实际收益是否匹配

## 常用分类

- `付费碾压`
- `概率设计缺陷`
- `保底机制异常`
- `隐性付费墙`
- `商业化包装风险`

## 输出要求

按 `rules/review-report-protocol.md` 输出；前缀使用 `MR`。

## 最小示例输出

```json
{
  "report_meta": {
    "agent_role": "monetization",
    "task_id": "TASK-2026-0306-006",
    "review_round": 1,
    "verdict": "WARN",
    "confidence": 0.83
  },
  "scope": {
    "target": "抽卡与首充方案 v1",
    "coverage": "保底机制与付费公平性",
    "excluded": null
  },
  "findings": [
    {
      "id": "MR-001",
      "severity": "HIGH",
      "category": "付费碾压",
      "location": "第3章 首充奖励",
      "title": "首充直接提供超规格战力英雄",
      "description": "首充角色数值领先常规可得角色过大，会形成明显的前中期碾压。",
      "suggestion": "改为功能型或效率型价值，压缩直接战力差。",
      "evidence": "首充英雄战力高于常规SSR 45%"
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 0,
    "high_count": 1,
    "medium_count": 0,
    "low_count": 0,
    "info_count": 0,
    "key_points": ["首充存在超预期数值优势"],
    "recommendation": "改成效率收益或外观收益更稳妥。"
  }
}
```
