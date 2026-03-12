---
name: brainstorming
description: "You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation."
---

# 头脑风暴：把想法变成设计

在任何实现动作之前，先通过对话把需求澄清为可执行设计。

## 强制规则

- 未完成设计并得到用户确认前，禁止进入实现。
- 无论需求大小，都必须产出设计（可长可短）。
- 本技能结束时，仅允许切换到 `writing-plans`，不直接编码。

## 标准流程

1. 了解项目上下文（代码、文档、近期变更）
2. 如将涉及视觉讨论，先单独发送视觉协作提示
3. 逐条澄清（每次只问一个问题）
4. 提供 2-3 个方案并给出推荐与取舍
5. 分章节输出设计并逐段确认
6. 落盘设计文档到 `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`
7. 进行规范审查循环，直至通过
8. 请用户审阅文档并确认
9. 切换到 `writing-plans` 生成实施计划

## 设计内容建议

- 架构与边界
- 组件与职责
- 数据流与状态变化
- 错误处理与降级
- 测试策略与验收条件

## 反模式

- “需求太简单，不需要设计”
- 一次性抛出多个问题
- 方案没有比较与推荐
- 未获确认就进入实现
