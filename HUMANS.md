<!-- orbit:begin orbit_id="ghpm-zh" -->
# GHPM Orbit 使用说明

这个 orbit 帮助开发者把 GitHub issue 从“想法”推进到 milestone 计划、开发准备和 PR 提交。开发者负责判断、确认和授权；skill 负责按固定流程读文件、生成草案、同步状态和执行明确批准的写操作。

```

## 工作流程

1. 收集新需求或缺陷：用 `$create-issue` 创建普通 issue 或 issue 草稿。创建后停下，不直接规划 milestone。
2. 整理待处理 issues：用 `$issue-triage` 初筛、分类、识别 blocker，并决定下一步是进入 milestone、继续讨论，还是拆分。
3. 澄清或拆分 issue：用 `$issue-evaluation` 补全需求、技术方案、验收标准，或把过大的 issue 拆成可执行子 issue。
4. 规划 milestone：用 `$create-milestone` 把 `status/ready-for-milestone` 的 issues 分组，创建 Milestone Hub Issue、技术债记录 issue、依赖关系、批次和开发顺序。
5. 准备开发上下文：用 `$prepare-development` 为整个 milestone 创建或复用 worktree，同步 `.issues/`，更新 `.ghpm.json`，输出开发交接摘要。
6. 开发由人或其他开发 agent 完成。GHPM 不写业务代码、不 review、不 merge。开发完成后，把对应 issue 更新为 `status/development-complete`。
7. 提交 PR：用 `$submit-pr` 扫描所有 worktree，为已完成且已提交代码的 issue 创建 PR，并把 issue 推进到 `status/submitted`。

## 开发者确认点

读取、分析和生成建议可以直接让 skill 做。批量改 labels、改 issue body、创建 milestone、切换 worktree、修改 `.ghpm.json`、push issue、创建 PR 前，先看 dry-run 或计划；确认无误后再明确说“执行”“应用”“创建”或“提交”。
<!-- orbit:end orbit_id="ghpm-zh" -->
```
