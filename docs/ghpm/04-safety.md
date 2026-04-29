# 04 — 安全与修改规则

## 默认 dry-run

以下操作默认先展示计划：

- 批量修改 labels
- 创建或重写 Milestone Hub Issue
- 修改多个 issue 的依赖或父子关系
- 创建或切换 worktree
- 修改 `.ghpm.json`
- push issue 变更
- 创建 PR
- 清理 worktree 或 branch

用户明确说“执行”“应用”“创建”“提交”后才进行写操作。

## 禁止事项

不要：

- 把 `.issues/` 加入 git
- 把 `.ghpm.json` 加入 git
- 在业务 PR 中提交 issue 镜像文件
- 自动关闭 issue
- 自动 merge PR
- 替代 PR review
- 忽略 open blocker
- 让 `kind/milestone-hub` 或 `kind/epic` 进入开发准备
- 清理有未提交更改的 worktree

## 修改 issue 前

1. 读取当前 issue 文件。
2. 保留现有有效内容。
3. 只修改必要字段。
4. 确保只有一个 `status/*`。
5. push 前展示 diff 或摘要。

## submit 前

必须确认：

- issue 文件有 `status/development-complete`
- 当前分支不是默认分支
- 代码已提交
- 工作区干净
- branch 相对 base 有提交
- PR body 包含 `Closes #<issue-number>`

不确定时停止，不要猜测提交。
