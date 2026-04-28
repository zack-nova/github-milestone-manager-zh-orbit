# Issue Triage Workflow

## 目标

把未分类或状态不清的 GitHub issue 转换成清晰的下一步状态。不要处理 milestone 归属。

## 初筛步骤

1. 确认 `.issues/` 已由 `gh-issue-sync` 同步。
2. 扫描 open issues，过滤已进入开发、已提交或已完成的 issue。
3. 对每个候选 issue 判断合理性、规模、是否需要拆分、需求清晰度和技术清晰度。
4. 判断候选 issue 之间是否存在明确 blocker 关系。
5. 给出分类表；如果用户要求执行，再写回 front matter。

## 分类规则

### 不合理或暂不可处理

无关、重复、缺少基本信息、明显不适合项目，或需要人工产品判断：

```text
status/not-actionable
```

说明原因，不自动关闭。

### 可直接准备进入 milestone

目标清楚、需求清楚、技术方向清楚、规模适中：

```text
status/ready-for-milestone
```

后续交给 `$create-milestone` 分组、排依赖和划批次。

### 特大 issue，需要拆分

范围过大、跨多个模块或无法作为单个开发任务：

```text
status/needs-breakdown
scope/needs-breakdown
```

后续交给 `$issue-evaluation` 讨论拆分。

### 需要需求讨论

缺少“做什么”“为什么做”或验收标准：

```text
status/needs-requirement-discussion
```

### 需要技术讨论

需求清楚，但实现路径、风险、边界或测试计划不清：

```text
status/needs-technical-discussion
```

### 需求和技术都需要讨论

需求和技术方案都不清：

```text
status/needs-requirement-and-technical-discussion
```

## 写回策略

只修改分类相关 labels、明确的 `blocked_by` / `blocks` 和必要说明。不要添加 milestone label，不要改 GitHub milestone 字段。

## Block 关系规则

可以建立：

```yaml
blocked_by:
  - 12
blocks:
  - 24
```

要求：

- 依赖方向必须明确。
- issue 编号必须明确。
- 双向字段要同步维护。
- 如果只是猜测，输出建议但不写回。

示例：

```text
#24 的 API 集成必须等 #12 认证基础完成
```

写入：

```yaml
#24
blocked_by:
  - 12

#12
blocks:
  - 24
```
