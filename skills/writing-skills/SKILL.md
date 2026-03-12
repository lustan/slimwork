---
name: writing-skills
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment
---

# 编写与维护技能文档

用于创建、重构和验证技能文档，确保可触发、可执行、可维护。

## 基本结构

- `SKILL.md`：必需，包含 frontmatter 与主体说明
- `scripts/`：可选，放可执行脚本
- `references/`：可选，放按需加载资料
- `assets/`：可选，放输出所需静态资源

## 编写原则

1. 触发条件优先：`description` 只写“何时使用”
2. 内容精简：避免冗长背景，强调执行步骤
3. 渐进披露：把重内容放到 references
4. 可验证：给出清晰检查与验收方式

## 常见错误

- 描述字段写成流程摘要（导致误触发）
- 技能正文过长且无结构
- 缺少明确输入输出与边界
- 没有验证闭环
