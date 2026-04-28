# 03 — GHPM 技能入口

使用 `$skill-name` 触发具体流程：

```text
$create-issue          只创建普通 issue 或 issue 草稿
$issue-triage          初筛 issue，过滤不合理项并判断下一步
$issue-evaluation      讨论清楚或拆分清楚，使 issue 准备进入 milestone
$create-milestone      分组 issues、划依赖和批次、创建 milestone 计划
$prepare-development   为整个 milestone 准备 worktree、issue 同步和 .ghpm.json
$submit-pr             扫描完成开发的 issue 并创建 PR
```

自然语言请求应映射到最接近的 skill。不要在 AGENTS 中复制各 skill 的完整流程。

## 状态门槛

- `$issue-triage` 和 `$issue-evaluation` 都可以把已清楚的 issue 推进到 `status/ready-for-milestone`。
- `$create-milestone` 将可开发 issue 推进到 `status/ready-for-dev`。
- `$prepare-development` 为包含 `status/ready-for-dev` issues 的 milestone 准备上下文。
- `$submit-pr` 只处理 `status/development-complete`。
- PR 创建成功后由 `$submit-pr` 改为 `status/submitted`。

## 不属于 GHPM 的工作

GHPM 不负责：

- 写业务代码
- review PR
- 修复 PR
- merge PR
- 自动关闭 issue
