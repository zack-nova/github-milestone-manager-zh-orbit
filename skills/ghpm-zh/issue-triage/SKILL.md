---
name: issue-triage
description: 初筛 GitHub issues，过滤不合理 issue，判断 blocker 关系，并判断下一步是可进入 milestone 准备、特大 issue 需要拆分、需要需求讨论、需要技术讨论、或需求和技术都需要讨论。用于用户要求初筛、整理、分类、过滤无效 issue、判断 block 关系、判断讨论类型或拆分需求时；不负责 milestone 归属、创建 milestone、讨论细节、开发实现或提交 PR。
---

# Issue Triage

你负责初筛现有 issue，只判断“下一步该做什么”。不要分配 milestone 归属。

## 读取顺序

1. 先读仓库根目录的 `AGENTS.md`，如果存在。
2. 读取 `references/workflow.md` 获取初筛规则。
3. 需要输出批量建议时使用 `templates/triage-report.md`。

## 输入

优先使用 `gh-issue-sync` 同步出的本地文件：

```text
.issues/open/*.md
.issues/closed/*.md
```

如果本地未同步，先建议或执行：

```bash
gh-issue-sync sync --all
```

## 分类目标

把 issue 分到以下类别之一：

- 不合理或暂不可处理：`status/not-actionable`
- 可直接准备进入 milestone：`status/ready-for-milestone`
- 特大 issue，需要拆分：`status/needs-breakdown`
- 需要需求讨论：`status/needs-requirement-discussion`
- 需要技术方案讨论：`status/needs-technical-discussion`
- 需求和技术都需要讨论：`status/needs-requirement-and-technical-discussion`

## 分类输出

对每个候选 issue 输出：

- issue 编号和标题
- 分类类别
- 建议 `kind/*`
- 建议 `type/*`、`size/*`、`scope/*`、`priority/*`、`risk/*`，如果可判断
- 建议唯一 `status/*`
- 建议 `blocked_by` / `blocks` 关系，如果能明确判断
- 需要的后续 skill：`$issue-evaluation` 或 `$create-milestone`
- 理由和拟修改摘要

## 不做的事

不要：

- 分配 milestone
- 写入 `milestone/<slug>`
- 创建或修改 Milestone Hub Issue
- 讨论需求或技术细节
- 拆分并创建子 issue
- 创建 PR

## Block 关系

初筛时可以识别明显依赖关系：

```yaml
blocked_by:
  - 12
blocks:
  - 24
```

判断原则：

- A 必须先完成，B 才能开始：B `blocked_by: [A]`，A `blocks: [B]`。
- 只有语义明确、编号明确、方向明确时才写入。
- 不确定时只输出“可能存在依赖”，不要写入 front matter。
- 写入时要维护双向关系：给被阻塞 issue 写 `blocked_by`，给前置 issue 写 `blocks`。

## 写回规则

默认只给建议。只有用户明确要求“执行”“应用”“写回”“同步”时才修改 issue 文件并 push。

写回时：

1. 保留现有有效内容。
2. 移除旧 `status/*`，只保留一个新 `status/*`。
3. 如果写入 block 关系，同时更新双方 issue。
4. 不自动关闭 issue。
5. push 前展示 diff 或修改摘要。
6. 写回后执行：

```bash
gh-issue-sync push
gh-issue-sync sync --all
```
