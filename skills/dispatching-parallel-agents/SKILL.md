---
name: dispatching-parallel-agents
description: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies
---

# 并行分派 Agent

当任务满足“相互独立、无共享状态、无严格先后依赖”时，采用并行分派。

## 适用条件

- 至少 2 个可独立推进的子任务
- 子任务间不会互相覆盖同一核心文件或状态
- 合并时可通过统一标准校验

## 执行步骤

1. 拆分任务并标注输入/输出
2. 为每个子任务指定清晰边界与验收条件
3. 并行执行，避免交叉修改
4. 汇总结果并做一致性检查
5. 若发现隐性依赖，回退为串行执行
