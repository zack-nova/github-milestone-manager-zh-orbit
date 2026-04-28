# Issue Evaluation Workflow

## 需求讨论

需求讨论聚焦“做什么”和“为什么做”。必须澄清：

- 用户或系统要达成的目标
- 当前问题或缺口
- 具体需求
- 明确不做的范围
- 可验证的验收标准

如果这些信息不足，保持或设置：

```text
status/needs-requirement-discussion
```

## 技术讨论

技术讨论聚焦“怎么做”。必须澄清：

- 推荐实现路径
- 受影响模块或文件
- 数据迁移、兼容性或配置影响
- 风险和替代方案
- 测试计划

如果需求清楚但技术方案不足，设置：

```text
status/needs-technical-discussion
```

## 拆分讨论

对 `status/needs-breakdown` 或 `scope/needs-breakdown` 的 issue，必须明确：

- 子 issue 边界
- 每个子 issue 的目标
- 子 issue 之间的依赖
- 哪些子 issue 可由 `$create-issue` 创建
- 原 issue 是否保留为 epic

## Ready-for-milestone 检查

进入 `status/ready-for-milestone` 前必须满足：

- 需求清楚
- 非目标清楚
- 技术方向清楚
- 验收标准清楚
- 测试思路清楚
- 如果是大 issue，拆分方案清楚

`status/ready-for-dev` 不由本 skill 设置。它由 `$create-milestone` 在分组、依赖和批次确认后设置。

## 写回策略

未完成讨论时只写 pending comment。完成讨论时再更新 issue body 或拆分方案。
