---
name: create-milestone
description: 创建和规划 GHPM milestone，把已初筛或已研判清楚的 issues 分组、划分 milestone 范围、建立依赖关系、安排批次和 development_order，并创建 Milestone Hub Issue、milestone 技术债记录 issue、GitHub 原生 milestone 与归属 label。用于用户要求新建 milestone、规划 milestone、把 ready-for-milestone issues 分组、划分开发批次或准备 milestone 开发计划时；不负责初筛、需求讨论、实际 worktree 准备、开发实现或提交 PR。
---

# Create Milestone

你负责把已经清楚的 issues 组织成一个或多个 milestone，并让这些 milestone 具备开发前的计划结构。

## 读取顺序

1. 先读仓库根目录的 `AGENTS.md`，如果存在。
2. 读取 `references/milestone-structure.md` 获取命名、范围、依赖和批次规则。
3. 使用 `templates/milestone-hub-issue.md` 创建 Milestone Hub Issue。
4. 使用 `templates/technical-debt-issue.md` 创建 milestone 技术债记录 issue。

## 输入

优先处理：

- `status/ready-for-milestone`
- `$issue-evaluation` 输出的拆分完成 issue
- 用户明确指定的一组 issue

不要接收仍处于需求讨论、技术讨论或拆分未完成状态的 issue，除非用户明确要求先做草案。

## 职责

创建或确认：

1. milestone 名称和范围。
2. GitHub 原生 milestone。
3. 归属 label：`milestone/<slug>`。
4. 唯一 Milestone Hub Issue。
5. milestone 技术债记录 issue。
6. included issues。
7. issue 之间的 `blocked_by` / `blocks` 依赖。
8. development batches。
9. `development_order`。
10. 哪些 included issues 可以设置为 `status/ready-for-dev`。

## 命名

使用：

```text
M-v<版本号>-<主题>
```

示例：

```text
M-v0.4-auth-core
```

对应 label：

```text
milestone/M-v0.4-auth-core
```

## 状态更新

对纳入 milestone 且已满足开发前条件的 issue：

```text
status/ready-for-dev
```

对仍缺信息或被阻塞的 issue，保留原状态或设置 `status/blocked`，并在 hub issue 里说明原因。

## 技术债记录 issue

每个 milestone 创建一个专用技术债 issue，用来记录开发该 milestone 过程中产生、发现或暂缓处理的技术债。

默认 labels：

```text
kind/chore
type/tech-debt
milestone/<slug>
status/technical-debt-tracking
```

这个 issue 不进入 `development_order`，也不作为普通开发任务提交 PR。milestone 结束时再由人工或后续流程整理其中条目。

## 写回

默认先输出分组计划、依赖图、批次计划和 hub issue 草稿。用户明确要求创建时再执行 GitHub 写操作。

创建后同步：

```bash
gh-issue-sync sync --all
```

## 边界

不要初筛、不要需求/技术讨论、不要创建 worktree、不要实际开发、不要创建 PR。
