---
title: "[Milestone] {{ milestone_name }}"
labels:
  - kind/milestone-hub
  - {{ milestone_label }}
  - status/milestone-planning
milestone: "{{ milestone_name }}"
state: open
---

# [Milestone] {{ milestone_name }}

## GHPM 控制块

```yaml
ghpm_milestone_hub:
  name: "{{ milestone_name }}"
  milestone_label: "{{ milestone_label }}"
  included_issues:
{{ included_issues_yaml }}
  technical_debt_issue: {{ technical_debt_issue_number }}
  batches:
{{ batches_yaml }}
  development_order:
{{ development_order_yaml }}
  ready_policy: first_unblocked_ready_issue
  source_of_truth: milestone_hub_issue
```

## 目标

{{ goal }}

## 不包含范围

{{ non_goals }}

## Included Issues

| Issue | 标题 | 状态 | Batch | 依赖 |
|---|---|---|---|---|
{{ issues_table }}

## Development Batches

{{ batches_text }}

## 推荐开发顺序

{{ development_order_text }}

## 当前可开发 Issue

{{ current_developable_issues }}

## 技术债记录 Issue

{{ technical_debt_issue }}

## 依赖图摘要

{{ dependency_graph }}

## 风险

{{ risks }}

## 完成条件

- [ ] 所有 included issues 已完成或明确移出范围
- [ ] 所有已创建 PR 已进入后续 review/merge 流程
- [ ] 没有 remaining open blocker
- [ ] 阶段总结已写入本 issue

## 阶段总结

{{ summary }}
