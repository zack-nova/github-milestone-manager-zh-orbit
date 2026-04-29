# 01 — GHPM 最小模型

## 事实源顺序

1. GitHub 远端 issues 是最终远端事实源。
2. `gh-issue-sync` 同步出的 `.issues/open/*.md` 和 `.issues/closed/*.md` 是本地 issue 工作副本。
3. GitHub issues 保存 milestone 计划、需求、技术方案、验收标准和测试计划。
4. `.ghpm.json` 只保存本地运行态，不作为远端事实源。

## 本地文件

```text
.issues/
  open/
  closed/
  .sync/

.ghpm.json
```

## `.ghpm.json`

`.ghpm.json` 只保存必要信息。推荐形态：

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

不要在 `.ghpm.json` 中保存 issue 正文、milestone 正文、PR body、handoff 全文或缓存。

## Worktree

worktree 路径由 `.ghpm.json` 记录。默认建议放在仓库外部，避免为了本地 worktree 再创建仓库内状态目录：

```text
../ghpm-worktrees/<repo>/<milestone-slug>
```

handoff 默认在对话中输出。只有用户明确要求文件时，才生成临时文件或用户指定文件。
