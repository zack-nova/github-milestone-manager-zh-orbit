---
title: "[Tech Debt] {{ milestone_name }}"
labels:
  - kind/chore
  - type/tech-debt
  - {{ milestone_label }}
  - status/technical-debt-tracking
milestone: "{{ milestone_name }}"
state: open
---

# [Tech Debt] {{ milestone_name }}

本 issue 专门记录开发 `{{ milestone_name }}` 过程中产生、发现或暂缓处理的技术债。

## 使用规则

- 只记录与本 milestone 相关的技术债。
- 记录时说明背景、影响、建议处理方式和是否阻塞当前 milestone。
- 不把本 issue 当作普通开发任务提交 PR。
- milestone 收尾时整理本 issue，并决定转成后续 issue、纳入后续 milestone，或关闭已解决条目。

## 技术债条目

| 来源 Issue/PR | 描述 | 影响 | 建议处理 | 是否阻塞 |
|---|---|---|---|---|
{{ debt_rows }}

## 阶段收尾

{{ closeout_notes }}
