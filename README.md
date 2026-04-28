# GHPM 中文 GitHub Milestone Manager Orbit

这是一个 Harness Yard source orbit，用中文规则和本地 Codex skills 管理 GitHub issues、milestones、Milestone Hub Issue、开发准备和 PR 提交流程。

## 内容

- `.harness/orbits/ghpm-zh.yaml`：orbit authored truth。
- `AGENTS.md`：极简 agent 入口，由 orbit guidance 生成。
- `docs/ghpm/`：长期规则和流程说明。
- `bootstrap/ghpm-zh/`：仓库初始化说明和 GitHub 网站模板。
- `skills/ghpm-zh/`：相关 skills。

## 相关 skills

- `create-issue`
- `issue-triage`
- `issue-evaluation`
- `create-milestone`
- `prepare-development`
- `submit-pr`

## 作者检查

检查这个 source orbit：

```bash
hyard orbit validate
hyard orbit prepare ghpm-zh --check
```

不要提交 `.issues/` 或 `.ghpm.json`。`.issues/` 是本地 issue 镜像，`.ghpm.json` 是最小 GHPM 运行态。
