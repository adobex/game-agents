# 审查上报协议

用于 `game-agents` 项目内所有“审查型输出”的统一结构规范。该协议吸收了 `ai_tribunal_design/reporting_protocol.md` 的优点，但按渐进式披露压缩为项目内可复用的最小必要版本。

## 适用范围

- 门下省的审核结论
- 各司提交的专项审查意见
- 项目共用审查 skill 的标准输出

## 统一裁决

- `PASS`: 未发现阻塞问题，可继续推进
- `WARN`: 存在需要修正的问题，但不必阻塞整体方向
- `FAIL`: 存在阻塞问题，必须返工或重审
- `SKIP`: 信息不足或超出当前审查范围

## 统一严重性

- `CRITICAL`: 立即阻塞，如核心循环断裂、公式崩溃、经济可刷穿
- `HIGH`: 当前迭代必须修正，如成长失衡、路径死锁、严重体验断层
- `MEDIUM`: 应尽快修正，如规则描述不清、局部节奏问题
- `LOW`: 建议修正，如格式、术语、小幅可读性问题
- `INFO`: 观察项或优化建议

## 标准输出结构

```json
{
  "report_meta": {
    "agent_role": "balancing",
    "task_id": "TASK-2026-0306-001",
    "review_round": 1,
    "verdict": "WARN",
    "confidence": 0.84
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
      "evidence": "Lv80->Lv81 攻击提升 18%，远高于前段 3%~5%"
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

## 前缀约定

- `SA`: 系统/结构审查
- `CR`: 内容/规则/术语审查
- `EV`: 体验/流程/心流审查
- `BA`: 数值/平衡审查
- `EA`: 经济系统审查
- `MR`: 商业化/付费公平性审查
- `MX`: 门下省汇总结论

## 使用规则

1. 审查型技能只需输出结构化结果，不要在协议层塞入长篇解释。
2. 高等级问题必须尽量附 `evidence`。
3. 门下省在汇总多司意见时，先去重，再按最保守结论输出。
4. 若只是项目内部快速评审，可省略部分计数字段，但字段命名保持一致。
