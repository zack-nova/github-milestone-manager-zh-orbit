# Prepare Development Workflow

## Milestone 准备条件

目标 milestone 应满足：

- 有 Milestone Hub Issue
- 有 included issues
- 有 batches 或 development_order
- 至少有一个 issue 为 `status/ready-for-dev`，或明确说明为什么暂时没有
- 依赖和 blocker 已记录

## Worktree 检查

1. 如果 `.ghpm.json` 已记录 worktree，先验证路径存在。
2. 如果 worktree 不存在，创建 milestone worktree。
3. 检查当前 branch 是否符合 milestone 分支：

```text
ghpm/<milestone-slug>
```

4. 检查工作区是否干净。
5. 同步 issues。

## `.ghpm.json`

只写必要运行态：

```json
{
  "version": 1,
  "current_milestone": "<milestone-slug>",
  "worktrees": {
    "<milestone-slug>": {
      "worktree": "../ghpm-worktrees/<repo>/<milestone-slug>",
      "branch": "ghpm/<milestone-slug>",
      "owner": "local"
    }
  }
}
```

不要把 issue 正文、handoff 正文、PR body 或缓存写入 `.ghpm.json`。

## Handoff 内容

handoff 在回复中输出，应包含：

- milestone 目标和非目标
- included issues
- batches
- development_order
- 当前可开发 issue
- blocker 和依赖关系
- 本地 worktree 和 branch
- 完成指令

完成指令必须说明：每个 issue 开发完成并提交后，将 issue label 改为 `status/development-complete`。
