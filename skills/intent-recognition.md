---
name: Intent Recognition
description: 识别输入是闲聊、需求、评审还是追问，并给出最小分类结论
---

# Intent Recognition

识别输入是闲聊、需求、评审还是追问，并给出最小分类结论

## 何时使用

- 太子立项分拣
- 门下省判断请求性质

## 核心关注点

- 先判类型，再决定是否继续流转
- 只输出最小必要分类，不提前展开方案

## 输出要求

- 优先输出结论、关键判断与下一步动作
- 若需要结构化审查结果，遵循 `rules/review-report-protocol.md`
