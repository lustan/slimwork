---
name: verification-before-completion
description: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always
---

# 完成前验证

在宣称“完成/修复成功”前，必须用命令验证而非主观判断。

## 必做项

- 运行与改动相关的测试
- 执行必要的静态检查或构建
- 记录命令、结果与失败原因
- 失败则继续修复，不提前收工

## 交付要求

提交或 PR 描述中应包含关键验证证据。
