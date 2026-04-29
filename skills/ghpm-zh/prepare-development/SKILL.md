---
name: prepare-development
description: 为一整个 GHPM milestone 准备开发上下文、worktree、issue 同步和 .ghpm.json 状态。用于用户要求准备某个 milestone 开发、创建或复用 milestone worktree、同步 issues、读取当前工作树、同步 GHPM 状态、输出 milestone 开发交接上下文时；基于 gh-issue-sync、Milestone Hub Issue、GitHub issues 和 git worktree 工作。不会选择并实现单个 issue、创建 PR、review、merge 或关闭 issue。
---

# Prepare Development

你负责为一整个 milestone 准备开发上下文。不要在这个流程里实现 issue，也不要默认挑单个 issue 开发。

## 读取顺序

1. 先读仓库根目录的 `AGENTS.md`，如果存在。
2. 读取 `references/workflow.md` 获取 milestone 准备流程。
3. 使用 `templates/prepare-handoff.md` 在回复中生成 milestone 交接摘要。

## 输入

常见请求：

```text
$prepare-development M-v0.4-auth-core
准备当前 milestone 的开发上下文
同步 milestone 工作树和 GHPM 状态
```

## 职责

1. 确认目标 milestone 和 Milestone Hub Issue。
2. 读取 hub issue 的 included issues、batches、development_order、dependency graph。
3. 创建或复用 milestone worktree。
4. 读取当前 worktree 状态，确认分支、base、是否干净。
5. 在 worktree 内同步 `.issues/`。
6. 更新 `.ghpm.json` 中该 milestone 的 worktree、branch 和 current_milestone。
7. 输出 milestone 级开发交接上下文。

## Worktree 与 `.ghpm.json`

worktree 路径记录在仓库根目录 `.ghpm.json`。

默认 worktree 建议放到仓库外部：

```text
../ghpm-worktrees/<repo>/<milestone-slug>
```

`.ghpm.json` 推荐记录：

```json
{
  "version": 1,
  "current_milestone": "M-v0.4-auth-core",
  "worktrees": {
    "M-v0.4-auth-core": {
      "worktree": "../ghpm-worktrees/<repo>/M-v0.4-auth-core",
      "branch": "ghpm/M-v0.4-auth-core",
      "owner": "local"
    }
  }
}
```

## 同步 issue

在 worktree 内同步 issue：

```bash
GH_ISSUE_SYNC_DIR="$WORKTREE/.issues" gh-issue-sync sync --all
```

## 输出

向用户输出：

- milestone
- worktree path
- branch name
- Milestone Hub Issue file path
- included issues
- batches
- development_order
- 当前可开发 issue
- blocker 摘要
- 测试/验证提示
- 开发完成后 issue 需改为 `status/development-complete`

## 边界

不要写业务代码，不要创建 PR，不要 review，不要 merge。
