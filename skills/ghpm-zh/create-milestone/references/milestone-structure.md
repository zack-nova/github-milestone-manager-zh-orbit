# Milestone Structure

## 输入要求

优先纳入：

```text
status/ready-for-milestone
```

这些 issue 应已经由 `$issue-triage` 或 `$issue-evaluation` 判断清楚。

## Milestone Hub Issue

每个 milestone 必须有且只有一个 open Milestone Hub Issue。

必备 labels：

```text
kind/milestone-hub
milestone/<slug>
status/milestone-planning
```

## Hub Body

Hub Issue body 应包含：

- GHPM 控制块
- 目标
- 不包含范围
- included issues
- development batches
- recommended development order
- 当前可开发 issue
- 技术债记录 issue
- 依赖图摘要
- 风险
- 完成条件
- 阶段总结

## GHPM 控制块

```yaml
ghpm_milestone_hub:
  name: "M-v0.4-auth-core"
  milestone_label: "milestone/M-v0.4-auth-core"
  included_issues:
    - 18
    - 19
  technical_debt_issue: 20
  batches:
    batch-1:
      - 18
    batch-2:
      - 19
  development_order:
    - 18
    - 19
  ready_policy: first_unblocked_ready_issue
  source_of_truth: milestone_hub_issue
```

## 子 issue 归属

纳入 milestone 的 issue 使用相同 label：

```text
milestone/M-v0.4-auth-core
```

可以同时设置 GitHub 原生 milestone 字段：

```yaml
milestone: "M-v0.4-auth-core"
```

## 技术债记录 issue

每个 milestone 创建一个技术债记录 issue。

推荐标题：

```text
[Tech Debt] M-v0.4-auth-core
```

推荐 labels：

```text
kind/chore
type/tech-debt
milestone/M-v0.4-auth-core
status/technical-debt-tracking
```

它用于记录开发过程中产生、发现或暂缓处理的技术债，不默认进入 `development_order`。

## 依赖关系

使用：

```yaml
blocked_by:
  - 12
blocks:
  - 24
```

依赖关系应反映在 hub issue 的 dependency graph 和 batches 中。

## Ready-for-dev 检查

纳入 milestone 的 issue 进入 `status/ready-for-dev` 前必须满足：

- 需求清楚
- 非目标清楚
- 技术方向清楚
- 验收标准清楚
- 测试思路清楚
- 不需要继续拆分
- blocker 已记录

如果 blocker 未完成，issue 可以留在 milestone 中，但不要把它列为当前可开发。
