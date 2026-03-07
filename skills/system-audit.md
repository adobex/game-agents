---
name: System Audit
description: 审查系统边界、依赖关系、数据归属与扩展性的项目共用方法论
---

# System Audit

吸收自 `ai_tribunal_design/system_architect.md`，但只保留项目内高频复用的审查骨架。

## 何时使用

- 系统司设计外围系统时
- 战斗司设计战斗/技能/AI 关系时
- 关卡司涉及事件驱动与状态流转时
- 门下省需要检查“结构是否站得住”时

## 核心关注点

- 模块边界是否清晰，是否出现“上帝系统”
- 系统间是否存在循环依赖、越层调用、数据竞写
- 是否支持数据驱动扩展，而不是硬编码堆逻辑
- 核心数据的归属权、生命周期、同步路径是否明确

## 快速检查表

- [ ] 输入/输出接口是否明确
- [ ] 是否存在 A 依赖 B、B 又依赖 A
- [ ] 表现层是否越权直接改核心数据
- [ ] 新增内容接入是否需要修改核心逻辑
- [ ] 是否缺少必要状态机或事件流说明

## 常用分类

- `循环依赖`
- `层级违规`
- `上帝系统`
- `数据归属冲突`
- `扩展性缺陷`
- `状态机缺陷`

## 输出要求

按 `rules/review-report-protocol.md` 输出；前缀使用 `SA`。

## 最小示例输出

```json
{
  "report_meta": {
    "agent_role": "systems",
    "task_id": "TASK-2026-0306-001",
    "review_round": 1,
    "verdict": "WARN",
    "confidence": 0.81
  },
  "scope": {
    "target": "公会系统方案 v1",
    "coverage": "模块边界与数据归属",
    "excluded": null
  },
  "findings": [
    {
      "id": "SA-001",
      "severity": "HIGH",
      "category": "数据归属冲突",
      "location": "第3章 公会资金流",
      "title": "公会资金同时由公会系统和邮件系统写入",
      "description": "同一资金池被两个模块直接写入，后续对账与回滚会变复杂。",
      "suggestion": "统一由公会钱包模块持有写权限，邮件系统只发事件。",
      "evidence": "文档同时写明‘邮件直接加钱’与‘公会系统统一记账’"
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 0,
    "high_count": 1,
    "medium_count": 0,
    "low_count": 0,
    "info_count": 0,
    "key_points": ["存在核心数据归属冲突"],
    "recommendation": "先统一数据写入边界，再继续细化接口。"
  }
}
```
