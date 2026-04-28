---
name: create-issue
description: 创建新的 GitHub issue 或本地 gh-issue-sync issue 草稿。用于用户要求新建 issue、创建 bug/task/chore/epic 草稿、按 GHPM 基础模板生成 issue body、通过 GitHub CLI 创建 issue 时；只负责创建，创建后交给 issue-triage、issue-evaluation 和 create-milestone 处理，不负责讨论、拆分决策、milestone 归属、开发实现或提交 PR。
---

# Create Issue

你只负责创建 issue。创建完成后停止，不做初筛、讨论、拆分判断或 milestone 划分。

## 读取顺序

1. 先读仓库根目录的 `AGENTS.md`，如果存在。
2. 读取 `references/issue-structure.md` 获取最小 issue 结构。
3. 使用 `templates/basic-issue.md` 创建普通 issue 草稿。

## 适用范围

可以创建：

- `kind/task`
- `kind/bug`
- `kind/chore`
- `kind/epic`
- 未判断类型的普通 issue

不要创建：

- Milestone Hub Issue，这由 `$create-milestone` 负责。
- 子 issue 拆分方案，这由 `$issue-evaluation` 讨论清楚后再交给本 skill 创建。
- PR、branch、worktree。

## 默认状态

新 issue 默认只进入初筛：

```text
status/needs-triage
```

不要在创建时设置讨论结论、milestone 归属或 `status/ready-for-dev`。

## 写回

默认先生成 issue 草稿。用户明确要求创建时，可以用：

```bash
gh issue create --title "<title>" --body-file "<body-file>" --label "status/needs-triage"
```

如果用户指定了初始 kind label，可一并添加。创建后执行 `gh-issue-sync sync --all`，然后停止。
