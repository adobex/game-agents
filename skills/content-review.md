---
name: Content Review
description: 审查规则描述、术语一致性、参数完整性与文案可开发性的项目共用方法论
---

# Content Review

吸收自 `ai_tribunal_design/content_reviewer.md`。保留其“逐条审查”的优点，但避免把冗长示例直接压进各司。

## 何时使用

- 叙事司编写世界观、角色、人设与文本时
- 玩法司/系统司撰写规则说明时
- 门下省检查方案是否“可读、可做、无歧义”时

## 核心关注点

- 文案是否通顺、无歧义、符合场景语气
- 规则描述是否前后一致，是否存在文字与公式冲突
- 参数是否完整，包括默认值、范围、单位、边界情况
- 核心术语是否统一，是否存在同一概念多种叫法

## 快速检查表

- [ ] 是否有关键参数缺失
- [ ] 概率、百分比、枚举是否自洽
- [ ] 同一机制在不同段落是否自相矛盾
- [ ] 术语是否统一且首次出现可理解
- [ ] 读者能否直接据此继续实现或评审

## 常用分类

- `规则矛盾`
- `参数缺失`
- `术语不一致`
- `歧义表述`
- `完整性缺失`
- `格式规范问题`

## 输出要求

按 `rules/review-report-protocol.md` 输出；前缀使用 `CR`。

## 最小示例输出

```json
{
  "report_meta": {
    "agent_role": "narrative",
    "task_id": "TASK-2026-0306-002",
    "review_round": 1,
    "verdict": "WARN",
    "confidence": 0.86
  },
  "scope": {
    "target": "世界观说明 v2",
    "coverage": "术语一致性与参数完整性",
    "excluded": null
  },
  "findings": [
    {
      "id": "CR-001",
      "severity": "MEDIUM",
      "category": "术语不一致",
      "location": "第2章 阵营设定",
      "title": "同一阵营出现两个名称",
      "description": "文档前文使用‘流亡车团’，后文使用‘荒原车团’，会造成设定混乱。",
      "suggestion": "统一术语，并在首次出现时补一行定义。",
      "evidence": "第2章与第5章使用了不同叫法"
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 0,
    "high_count": 0,
    "medium_count": 1,
    "low_count": 0,
    "info_count": 0,
    "key_points": ["核心术语未统一"],
    "recommendation": "先统一术语表，再扩写世界观正文。"
  }
}
```
