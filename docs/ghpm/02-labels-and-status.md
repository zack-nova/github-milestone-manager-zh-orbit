# 02 — Labels 与状态

AGENTS 只保留跨流程必须共享的 `status/*` 状态。issue 类型、优先级、范围、风险、milestone 归属等非状态 label 细节由对应 skill 负责。

## 全部状态

```text
status/needs-triage
status/not-actionable
status/needs-requirement-discussion
status/needs-technical-discussion
status/needs-requirement-and-technical-discussion
status/needs-breakdown
status/ready-for-milestone
status/milestone-planning
status/ready-for-dev
status/in-development
status/development-complete
status/submitted
status/done
status/blocked
status/technical-debt-tracking
```

同一 issue 同一时间只保留一个有效的 `status/*`。

## 状态含义

- `status/needs-triage`：新建或新同步 issue，等待 `$issue-triage` 初筛。
- `status/not-actionable`：不合理、信息不足到无法推进，或暂不处理。
- `status/needs-requirement-discussion`：需求边界未明确，需要 `$issue-evaluation` 继续讨论。
- `status/needs-technical-discussion`：技术方案未明确，需要 `$issue-evaluation` 继续讨论。
- `status/needs-requirement-and-technical-discussion`：需求和技术方案都未明确。
- `status/needs-breakdown`：issue 太大，需要先拆分。
- `status/ready-for-milestone`：已经清楚，可以进入 `$create-milestone`。
- `status/milestone-planning`：Milestone Hub Issue 正在承载 milestone 计划。
- `status/ready-for-dev`：已纳入 milestone 且满足开发前条件，可以进入 `$prepare-development`。
- `status/in-development`：正在开发中。
- `status/development-complete`：开发完成且代码已准备好进入 `$submit-pr`。
- `status/submitted`：PR 已创建，等待 review、merge 或后续人工处理。
- `status/done`：issue 已完成，通常对应 PR 已合并或无需继续处理。
- `status/blocked`：被外部依赖、未解决 blocker 或缺失决策阻塞。
- `status/technical-debt-tracking`：milestone 专用技术债记录 issue，不进入普通开发队列。

## 状态切换规则

任何流程改变 issue 状态时，必须同时切换 `status/*` label。设置新 `status/*` 前先移除旧 `status/*`。

## 状态门槛

- `status/ready-for-milestone`：可以进入 `$create-milestone`。
- `status/ready-for-dev`：可以进入 `$prepare-development`。
- `status/development-complete`：开发完成，可以进入 `$submit-pr`。
- `status/submitted`：PR 已创建，等待 review/merge 后续流程。
