# 02 — 最小状态

AGENTS 只保留跨流程必须共享的开发状态。初筛、讨论、拆分、milestone 归属、issue 类型和优先级等 label 细节由对应 skill 负责。

## 开发状态

```text
status/ready-for-milestone
status/ready-for-dev
status/in-development
status/development-complete
status/submitted
status/done
status/blocked
```

同一 issue 同一时间只保留一个有效的 `status/*`。

## 状态切换规则

任何流程改变 issue 状态时，必须同时切换 `status/*` label。设置新 `status/*` 前先移除旧 `status/*`。

## 状态门槛

- `status/ready-for-milestone`：可以进入 `$create-milestone`。
- `status/ready-for-dev`：可以进入 `$prepare-development`。
- `status/development-complete`：开发完成，可以进入 `$submit-pr`。
- `status/submitted`：PR 已创建，等待 review/merge 后续流程。
