# Workflow State Machine

用于把 `game-agents` 的三省六部流程从“描述性文档”进一步收敛成“可执行协作协议”。

默认遵循两条总原则：

- 重大方案不得绕过 `menxia`
- 11 司不得彼此直接派工，只能通过 `shangshu` 调度

## 1. 状态总览

```text
draft_request
  -> triaged
  -> planning
  -> under_review
  -> approved
  -> dispatched
  -> in_execution
  -> integrating
  -> completed

under_review -> rejected -> planning
dispatched / in_execution / integrating -> blocked -> dispatched / in_execution / under_review
```

## 2. 状态定义

### `draft_request`

- 含义：原始需求刚进入系统，尚未被分拣
- 责任 Agent：`taizi`
- 典型输入：用户口头需求、模糊想法、多个诉求混在一起
- 退出条件：被识别为闲聊、澄清请求或正式需求

### `triaged`

- 含义：`taizi` 已完成分拣，形成可继续流转的最小输入包
- 责任 Agent：`taizi`
- 标准产物：`《立项旨意书》`
- 下一状态：
  - 正式需求 -> `planning`
  - 非正式需求 -> 直接结束，不进入状态机后续环节

### `planning`

- 含义：`zhongshu` 正在把旨意扩展为宏观规划
- 责任 Agent：`zhongshu`
- 标准产物：`《宏观规划大纲》`
- 退出条件：形成系统树、模块边界、司局分工与风险摘要
- 下一状态：`under_review`

### `under_review`

- 含义：`menxia` 正在进行准奏 / 封驳审议
- 责任 Agent：`menxia`
- 标准产物：`《审议结论》`
- 可能结果：
  - `approved`
  - `rejected`

### `approved`

- 含义：`menxia` 已准奏，方案被允许进入执行调度
- 责任 Agent：`menxia` -> `shangshu`
- 进入条件：不存在阻塞级逻辑断裂、重大偏题、明显越权
- 下一状态：`dispatched`

### `rejected`

- 含义：方案被 `menxia` 封驳，必须回修
- 责任 Agent：`menxia`
- 必须附带：
  - 阻塞问题
  - 修订建议
  - 回退目标
- 若进入修复闭环：
  - 需标注 `review_round`
  - 默认遵循 `docs/review-repair-loop.md`
- 下一状态：回到 `planning`

### `dispatched`

- 含义：`shangshu` 已把准奏方案拆成面向各司的任务包
- 责任 Agent：`shangshu`
- 标准产物：`《派工单》`
- 退出条件：至少一个 11 司已拿到明确任务、输入包和回收标准
- 下一状态：`in_execution`

### `in_execution`

- 含义：一个或多个 11 司正在并行执行专项任务
- 责任 Agent：各 11 司，统一向 `shangshu` 回传
- 标准产物：专项方案、审查报告或风险备注
- 下一状态：
  - 所有关键专项齐备 -> `integrating`
  - 发生阻塞 -> `blocked`

### `integrating`

- 含义：`shangshu` 正在汇总、去重、处理冲突
- 责任 Agent：`shangshu`
- 标准产物：`《整合奏折》`
- 下一状态：
  - 可直接成稿 -> `completed`
  - 出现重大冲突或新增高风险 -> `blocked` 或回 `under_review`

### `blocked`

- 含义：流程暂时无法继续，需要补信息、消除冲突或重新审议
- 责任 Agent：触发阻塞的当前责任方发起，`shangshu` 负责追踪
- 常见原因：
  - 输入信息缺失
  - 多司产出互相冲突
  - 数值 / 经济 / 付费风险过高
  - 发现某项内容本应先过 `menxia`
- 恢复路径：
  - 补信息后回 `dispatched` 或 `in_execution`
  - 若已影响方案根基，则回 `under_review` 或 `planning`

### `completed`

- 含义：本轮方案已经整合完成，可回呈上游或结束
- 责任 Agent：`shangshu`
- 标准产物：成稿版 `《整合奏折》` 或上游要求的正式文档

## 3. 合法状态迁移

| 当前状态 | 允许发起方 | 可迁移到 | 条件 |
|---|---|---|---|
| `draft_request` | `taizi` | `triaged` | 完成意图分拣 |
| `triaged` | `taizi` | `planning` | 已形成《立项旨意书》 |
| `planning` | `zhongshu` | `under_review` | 已形成《宏观规划大纲》 |
| `under_review` | `menxia` | `approved` | 通过审议 |
| `under_review` | `menxia` | `rejected` | 存在阻塞问题 |
| `rejected` | `menxia` | `planning` | 中书省接回修订 |
| `approved` | `shangshu` | `dispatched` | 已拆成任务包 |
| `dispatched` | `shangshu` | `in_execution` | 至少一个专项开始执行 |
| `dispatched` | `shangshu` | `blocked` | 输入包或依赖缺失 |
| `in_execution` | `11司` / `shangshu` | `integrating` | 关键专项已回收 |
| `in_execution` | `11司` / `shangshu` | `blocked` | 出现冲突或阻塞 |
| `integrating` | `shangshu` | `completed` | 已完成整合 |
| `integrating` | `shangshu` | `blocked` | 出现重大冲突 |
| `integrating` | `shangshu` / `menxia` | `under_review` | 需要重新审议 |

## 4. 权限约束

### 必经节点

- 所有重大需求必须经过：`taizi -> zhongshu -> menxia -> shangshu`
- 任意 11 司的正式执行任务，必须由 `shangshu` 派发
- 高风险整合结果可以回到 `menxia` 再审，但不能让 11 司直接向 `menxia` 发起裁决请求

### 禁止迁移

- 禁止 `taizi -> 11司`
- 禁止 `zhongshu -> 11司`
- 禁止 `11司 -> 11司` 直接派工
- 禁止 `11司 -> menxia` 直接请求准奏
- 禁止 `shangshu` 在未准奏时进入 `dispatched`

## 5. 强制审议规则

以下情况不得跳过 `under_review`：

- 新立项或大改核心循环
- 涉及多个 11 司协同的跨系统方案
- 涉及 `economy` / `monetization` / `balancing` 的高敏感内容
- 将进入正式汇报、立项或对外评审的方案

以下情况建议二次审议：

- `integrating` 阶段出现重大冲突
- 审查 skill 给出 Critical / High 风险
- 本轮改动已经改变原始旨意中的关键假设

## 6. 阻塞处理协议

当进入 `blocked` 时，责任方必须输出最小阻塞包：

```markdown
# 阻塞通知

## 当前状态
- blocked

## 阻塞原因
- [缺信息 / 冲突 / 风险 / 权限问题]

## 影响范围
- [影响哪个司、哪个产物、哪个节点]

## 建议恢复路径
- [补什么信息 / 回到哪个状态 / 谁来处理]
```

## 7. 最小消息包

### 立项包

- 来源：`taizi`
- 必含：
  - 目标
  - 关键约束
  - 成功标准
  - 是否立项

### 规划包

- 来源：`zhongshu`
- 必含：
  - 核心体验
  - 系统树
  - 需参与司局
  - 风险摘要

### 派工包

- 来源：`shangshu`
- 必含：
  - 专项目标
  - 输入上下文
  - 回收标准
  - 依赖关系

### 回收包

- 来源：11 司
- 必含：
  - 专项结论
  - 与其他司接口
  - 风险与边界
  - 建议下一步

### 修复包

- 来源：`shangshu` / 对应 11 司
- 必含：
  - `review_round`
  - 待修问题列表
  - 修复边界
  - 是否建议重审

## 8. 推荐使用方式

- 需要快速理解流程：先读 `docs/how-to-run-game-agents.md`
- 需要知道输出格式：再读 `docs/output-templates.md`
- 需要跑“审查 -> 修复 -> 重审”闭环：读 `docs/review-repair-loop.md`
- 需要判断“当前卡在哪个状态、该往哪走”：读本文件

本文件回答的是“流程怎么跑、何时回退、谁能推动状态变化”。
