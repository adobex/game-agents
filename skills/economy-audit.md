---
name: Economy Audit
description: 审查资源产消闭环、通胀风险、交易机制与长线经济健康度的项目共用方法论
---

# Economy Audit

吸收自 `ai_tribunal_design/balance_auditor.md` 中经济系统相关部分，单独拆出给经济司与相关角色复用。

## 何时使用

- 经济司设计货币、资源、交易与回收系统时
- 数值司需要从宏观经济角度验证成长与产出时
- 运营司规划活动投放时

## 核心关注点

- 资源产出、库存、消耗是否构成闭环
- 长线运营下是否出现通胀、通缩、套利漏洞
- 活动投放是否冲击常态经济
- 多货币体系是否有明确汇率、沉淀池与单向流向

## 快速检查表

- [ ] 核心货币是否有稳定消耗出口
- [ ] 是否存在跨货币套利或无限刷取路径
- [ ] 高价值资源是否有沉淀池
- [ ] 交易行/拍卖/兑换是否有税率或限制
- [ ] 按月或赛季看，经济是否仍可控

## 常用分类

- `经济漏洞`
- `通胀/通缩风险`
- `资源投放失控`
- `兑换闭环异常`
- `交易机制缺陷`

## 输出要求

按 `rules/review-report-protocol.md` 输出；前缀使用 `EA`。

## 最小示例输出

```json
{
  "report_meta": {
    "agent_role": "economy",
    "task_id": "TASK-2026-0306-005",
    "review_round": 1,
    "verdict": "FAIL",
    "confidence": 0.88
  },
  "scope": {
    "target": "货币循环方案 v2",
    "coverage": "资源闭环与兑换系统",
    "excluded": null
  },
  "findings": [
    {
      "id": "EA-001",
      "severity": "CRITICAL",
      "category": "经济漏洞",
      "location": "第5章 兑换规则",
      "title": "跨货币兑换存在套利闭环",
      "description": "玩家可通过A币兑换B币后再回售道具，形成净增资源。",
      "suggestion": "取消回售、增加税率，或直接切断回兑链路。",
      "evidence": "100 A币可循环变成 130 A币"
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 1,
    "high_count": 0,
    "medium_count": 0,
    "low_count": 0,
    "info_count": 0,
    "key_points": ["存在可重复套利路径"],
    "recommendation": "立即修复兑换闭环，再继续活动投放设计。"
  }
}
```
