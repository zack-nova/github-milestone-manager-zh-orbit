# 04 — 初始化规则

## 初始化目标

让仓库可以通过 GHPM skills 管理 GitHub issues 和 milestones，同时保持本地状态极简。

## 必查项

1. 当前目录是 Git 仓库。
2. `gh` 已安装且已认证。
3. `gh-issue-sync` 可用。
4. `.issues/` 和 `.ghpm.json` 已加入 `.gitignore`。
5. `.ghpm.json` 存在或将在首次 prepare 时创建。
6. 最小 labels 已存在。
7. 现有 issues 已同步到 `.issues/`。
8. `.github/ISSUE_TEMPLATE/ghpm-issue.yml` 已创建。
9. `.github/pull_request_template.md` 已创建。

## 推荐命令

```bash
gh auth status
gh-issue-sync init
gh-issue-sync sync --all
```

## `.gitignore` 片段

```text
# GHPM / gh-issue-sync local state
.issues/
.ghpm.json
```

初始化可以修改 `.gitignore` 和创建空 `.ghpm.json`。远端 label、issue 或 milestone 修改仍需先展示计划。

## GitHub 模板

初始化时建议创建：

```text
.github/
  ISSUE_TEMPLATE/
    config.yml
    ghpm-issue.yml
  pull_request_template.md
```

这些模板让用户在 GitHub 网站上手动创建 issue 或 PR 时，也能保持 GHPM 所需的基础结构。

模板源文件位于：

```text
bootstrap/ghpm-zh/templates/github/ISSUE_TEMPLATE/config.yml
bootstrap/ghpm-zh/templates/github/ISSUE_TEMPLATE/ghpm-issue.yml
bootstrap/ghpm-zh/templates/github/pull_request_template.md
```

如果目标仓库已有模板，不要直接覆盖；先展示 diff 或合并计划。
