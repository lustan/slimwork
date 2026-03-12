---
name: subagent-driven-development
description: Use when executing implementation plans with independent tasks in the current session
---

# 子 Agent 驱动开发

把独立任务分配给子 Agent 并在主流程统一集成。

## 何时使用

- 计划中存在多个独立任务
- 可以通过清晰接口/边界拆分
- 需要提升吞吐并降低上下文干扰

## 流程

1. 任务拆分与边界定义
2. 分派子 Agent（输入、输出、验收标准）
3. 收敛结果并处理冲突
4. 统一验证与质量门禁
5. 形成可提交产出
