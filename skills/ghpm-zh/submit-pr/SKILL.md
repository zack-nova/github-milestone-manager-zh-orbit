---
name: submit-pr
description: 跨所有 git worktrees 扫描 GHPM issue 工作，识别标记为 status/development-complete 的 GitHub issue，并为对应 worktree 当前分支创建 PR。用于用户要求提交 PR、扫描任意工作树、把完成 issue 推送成 PR、更新 issue 为 status/submitted 时；基于 gh-issue-sync、git worktree 和 GitHub CLI 工作。不会 review、修复、merge PR，也不会自动关闭 issue。
---

# Submit PR

你负责扫描所有本地 git worktrees，把已经完成开发且已提交代码的 issue 工作提交为 PR。

## 读取顺序

1. 先读仓库根目录的 `AGENTS.md`，如果存在。
2. 读取 `references/workflow.md` 获取提交检查。
3. 使用 `templates/pr-body.md` 生成 PR body 内容。
4. dry-run 时可使用 `templates/submit-report.md`。

## 输入

常见请求：

```text
$submit-pr
$submit-pr --dry-run
扫描所有 worktree，把完成的 issue 创建 PR
提交所有 status/development-complete 的 issue
```

## 必要条件

目标 issue 必须在某个 worktree 的 issue 文件中包含：

```text
status/development-complete
```

对应 worktree 必须满足：

- 当前分支不是默认分支
- 代码已提交
- 工作区干净
- branch 相对 base 有提交

## 扫描所有 worktree

使用：

```bash
git worktree list --porcelain
```

对每个 worktree：

1. 找 `$WORKTREE/.issues/open/*.md`。
2. 解析 front matter。
3. 找到 `status/development-complete` 的 issue。
4. 排除 `kind/milestone-hub`、`kind/epic` 和非开发 issue。
5. 读取该 worktree 当前 branch。
6. 确认 branch 不是默认分支。
7. 确认工作区干净。
8. 确认 branch 相对 base 有提交。
9. 为该 worktree 当前 branch 创建 PR。

`.ghpm.json` 只能作为辅助线索，不限制扫描范围。任意 worktree 下只要发现可提交状态的 issue，就应进入 dry-run 或提交计划。

## 创建 PR

按 worktree/branch 分组创建 PR。PR body 必须包含每个被提交 issue：

```text
Closes #<issue-number>
```

可以用临时文件传给 GitHub CLI：

```bash
PR_BODY_FILE="$(mktemp)"
gh pr create --title "<title>" --body-file "$PR_BODY_FILE" --base <base>
```

不要在仓库中创建 `.ghpm/submit/`。

## 多 issue 情况

如果同一个 worktree/branch 下发现多个 `status/development-complete` issue：

- 如果这些 issue 属于同一 branch 的提交范围，可以创建一个 PR，并在 PR body 中包含多个 `Closes #...`。
- 如果无法判断它们是否属于同一提交范围，dry-run 中标记为需要人工确认。

## 更新 issue 状态

PR 创建成功后：

1. 把已提交 issue 的唯一状态改为 `status/submitted`。
2. 在 issue body 或 comment 草稿中记录 PR 链接。
3. 执行：

```bash
GH_ISSUE_SYNC_DIR="$WORKTREE/.issues" gh-issue-sync push
GH_ISSUE_SYNC_DIR="$WORKTREE/.issues" gh-issue-sync sync --all
```

只要 issue 状态从 completed 进入 submitted，就必须切换 `status/*` label。

## 边界

不要 review PR、修复 PR、merge PR 或关闭 issue。
