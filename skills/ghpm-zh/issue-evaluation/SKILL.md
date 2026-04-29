---
name: issue-evaluation
description: 讨论清楚或拆分清楚 GitHub issue，使其准备进入 milestone planning。用于用户要求澄清需求、确认技术方案、拆分特大 issue、完善验收标准、处理 status/needs-requirement-discussion、status/needs-technical-discussion、status/needs-requirement-and-technical-discussion 或 status/needs-breakdown 时；不负责划分 milestone、创建 milestone、准备 worktree、开发实现或提交 PR。
---

# Issue Evaluation

你负责把 issue 讨论清楚或拆分清楚，使其可以交给 `$create-milestone` 分组、排依赖和划批次。

## 读取顺序

1. 先读仓库根目录的 `AGENTS.md`，如果存在。
2. 读取 `references/workflow.md` 获取研判流程。
3. 需要写 pending comment 时使用 `templates/evaluation-comment.md`。
4. 需要重写 issue body 时使用 `templates/evaluated-issue-body.md`。

## 输入

通常输入为：

```text
$issue-evaluation #18
讨论 #18
补全 #18 的需求
确认 #18 的技术方案
拆分 #18
这个 issue 可以进入 milestone 规划了
```

优先读取：

- `.issues/open/<issue>.md`
- `parent` 指向的真实父 issue，如果存在
- `blocked_by` 中的 blocker issue
- 已存在的 pending comment 草稿

## 研判目标

普通 issue 最终应包含：

- 背景
- 问题
- 需求
- 不包含范围
- 技术方案
- 验收标准
- 测试计划
- 风险
- 开发备注

特大 issue 最终应包含：

- 拆分边界
- 子 issue 草案
- 依赖关系
- 哪些子 issue 可以交给 `$create-issue` 创建

## 状态更新

- 需求未明确：`status/needs-requirement-discussion`
- 技术未明确：`status/needs-technical-discussion`
- 需求和技术都未明确：`status/needs-requirement-and-technical-discussion`
- 需要拆分：`status/needs-breakdown`
- 已讨论或拆分清楚，可进入 milestone planning：`status/ready-for-milestone`

写入新状态前移除旧 `status/*`。

## 未讨论完

不要重写完整 issue body。创建或更新：

```text
.issues/open/<number>.comment.md
```

pending comment 记录已确认、未确认、当前建议和下次问题。

## 讨论完成

用户明确确认需求、技术方案或拆分方案完整后：

1. 更新 issue body 或写入拆分方案。
2. 确认后续不再需要需求/技术讨论。
3. 如果需要创建子 issue，输出给 `$create-issue` 的子 issue 草案。
4. 如果已可纳入 milestone planning，设置 `status/ready-for-milestone`。
5. push 前展示 diff 或摘要。
6. 执行：

```bash
gh-issue-sync push
gh-issue-sync sync --all
```

## 边界

不要创建 milestone、分配 milestone、准备 worktree、实现代码、创建 PR、review、merge 或自动关闭 issue。
