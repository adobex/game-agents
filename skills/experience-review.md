---
name: Experience Review
description: 审查玩家旅程、心流曲线、交互路径与认知负荷的项目共用方法论
---

# Experience Review

吸收自 `ai_tribunal_design/experience_validator.md`。适合在玩法、关卡、UX、运营方案中复用。

## 何时使用

- 玩法司定义核心循环与新手期体验时
- 关卡司设计节奏与区域推进时
- UX 司设计高频路径和信息密度时
- 运营司设计长期目标感与活动节奏时
- 门下省判断方案是否“玩家真能玩下去”时

## 核心关注点

- 玩家旅程是否完整，从新手到成熟期是否断层
- 难度和奖励是否形成心流，而不是无聊或焦虑
- 高频操作路径是否过长，是否存在认知过载
- 边界场景下是否会让玩家卡死、迷失或挫败

## 快速检查表

- [ ] 前 5 分钟能否理解核心玩法
- [ ] 前 30 分钟是否有稳定正反馈
- [ ] 高频操作能否在 3 步内完成
- [ ] 是否存在明显的难度断崖或长平台期
- [ ] 界面/玩法信息是否超过玩家单次可处理范围

## 常用分类

- `玩家旅程断裂`
- `心流曲线异常`
- `新手引导缺陷`
- `交互流程繁琐`
- `认知负荷过载`
- `目标感缺失`

## 输出要求

按 `rules/review-report-protocol.md` 输出；前缀使用 `EV`。

## 最小示例输出

```json
{
  "report_meta": {
    "agent_role": "ux",
    "task_id": "TASK-2026-0306-003",
    "review_round": 1,
    "verdict": "FAIL",
    "confidence": 0.89
  },
  "scope": {
    "target": "新手引导流程 v1",
    "coverage": "前10分钟玩家旅程",
    "excluded": null
  },
  "findings": [
    {
      "id": "EV-001",
      "severity": "HIGH",
      "category": "目标感缺失",
      "location": "第1章 开场流程",
      "title": "第一个5分钟没有明确短期目标",
      "description": "玩家只是在点击建筑与收资源，但没有被明确引导去完成一个可见目标。",
      "suggestion": "增加一个3分钟内可完成的短目标，并给出明确奖励反馈。",
      "evidence": "流程图中没有首个可见任务节点"
    }
  ],
  "summary": {
    "total_findings": 1,
    "critical_count": 0,
    "high_count": 1,
    "medium_count": 0,
    "low_count": 0,
    "info_count": 0,
    "key_points": ["新手前期缺少目标牵引"],
    "recommendation": "补足首个短目标与即时反馈后再继续铺教学。"
  }
}
```
