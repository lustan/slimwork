---
name: systematic-debugging
description: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes
---

# 系统化调试

先定位根因，再实施修复，避免“猜测式改动”。

## 核心原则

- 先稳定复现，再分析
- 证据驱动，不靠直觉
- 最小修复，最大验证
- 输出可复盘结论

## 建议流程

1. 明确现象、预期、实际
2. 构建可重复复现场景
3. 收集日志、堆栈、状态快照
4. 逐层缩小范围并定位根因
5. 设计最小修复并验证影响面
6. 补充回归测试，防止复发
