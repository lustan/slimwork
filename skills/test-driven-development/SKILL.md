---
name: test-driven-development
description: Use when implementing any feature or bugfix, before writing implementation code
---

# 测试驱动开发（TDD）

通过“先测试、后实现”确保需求被可执行规范约束。

## 三步循环

1. Red：先写失败测试，明确行为预期
2. Green：写最小实现让测试通过
3. Refactor：在测试保护下重构代码

## 实践要求

- 测试描述业务行为，不绑定实现细节
- 优先覆盖关键路径与边界条件
- 每次循环保持改动最小
- 失败信息要可诊断
