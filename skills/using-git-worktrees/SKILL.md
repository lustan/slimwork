---
name: using-git-worktrees
description: Use when starting feature work that needs isolation from current workspace or before executing implementation plans - creates isolated git worktrees with smart directory selection and safety verification
---

# 使用 Git Worktree

在不切换当前工作区的情况下，为并行任务创建隔离目录。

## 适用场景

- 同时处理多个特性/修复
- 需要保持主工作区稳定
- 计划执行需要独立上下文

## 基本流程

1. 基于目标分支创建 worktree
2. 在隔离目录开发与验证
3. 提交后清理 worktree
4. 回到主工作区继续其他任务
