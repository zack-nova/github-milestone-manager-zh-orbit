# Submit PR Workflow

## Dry-run 输出

默认先输出：

- 扫描到的所有 worktree
- 每个 worktree 的当前 branch
- 发现的 `status/development-complete` issues
- 工作区是否干净
- branch 是否相对 base 有提交
- 将创建的 PR title
- PR body 摘要
- 将更新的 issue label
- 是否需要人工确认

## 提交前检查

必须确认：

```text
issue 有 status/development-complete
issue 不是 kind/milestone-hub 或 kind/epic
branch 不是默认分支
git status --porcelain 为空
branch 相对 base 有提交
PR body 包含每个 issue 的 Closes #<issue-number>
```

## 跨 worktree 提交

`$submit-pr` 不只扫描 `.ghpm.json` 记录的 worktree。它必须遍历 `git worktree list --porcelain` 返回的所有 worktree。

任意 worktree 下，只要发现 issue 文件包含 `status/development-complete`，就为该 worktree 的当前 branch 生成 PR 计划。

## 成功后状态

PR 创建成功且 issue sync 成功后，设置：

```text
status/submitted
```

设置 `status/submitted` 前移除旧 `status/development-complete`。不要设置 `status/done`。`done` 由 merge/review 后续流程处理。

## 清理

默认保留 worktree。清理必须额外确认：

- PR 已创建成功
- issue 已更新为 `status/submitted`
- issue sync 成功
- worktree 干净

不确定时保留 worktree。
