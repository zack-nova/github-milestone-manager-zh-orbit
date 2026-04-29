# Issue Structure

## 最小 Front Matter

推荐字段：

```yaml
number: null
title: "{{ title }}"
labels:
  - status/needs-triage
assignees: []
state: open
blocked_by: []
blocks: []
```

如果用户明确指定类型，可以添加一个 `kind/*`：

```text
kind/task
kind/bug
kind/chore
kind/epic
```

## 创建阶段不写入

创建 issue 时不要写入：

- milestone 归属
- Milestone Hub Issue 信息
- 开发顺序
- 讨论结论
- `status/ready-for-dev`

这些由后续 `$issue-triage`、`$issue-evaluation` 和 `$create-milestone` 处理。

## 推荐正文

新 issue 只需要足够进入初筛：

- 背景
- 问题或目标
- 期望结果
- 细节和上下文
- 验收想法
