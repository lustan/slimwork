---
name: requesting-code-review
description: 当任务完成、实现了主要功能，或在合并前需要验证工作是否满足要求时使用
---

# 请求代码评审

派发 `superpowers:code-reviewer` 子代理，在问题扩散之前先把它们抓出来。

**核心原则：** 及早评审，经常评审。

## 何时请求评审

**强制：**
- 在子代理驱动开发中，每个任务之后
- 完成主要功能之后
- 合并到 main 之前

**可选但很有价值：**
- 卡住时（引入新视角）
- 重构前（先做基线检查）
- 修复复杂 bug 之后

## 如何请求

**1. 获取 git SHA：**
```bash
BASE_SHA=$(git rev-parse HEAD~1)  # 或 origin/main
HEAD_SHA=$(git rev-parse HEAD)
```

**2. 派发 code-reviewer 子代理：**

使用 Task 工具，类型为 `superpowers:code-reviewer`，并填写 `code-reviewer.md` 中的模板。

**占位符：**
- `{WHAT_WAS_IMPLEMENTED}` - 你刚刚构建了什么
- `{PLAN_OR_REQUIREMENTS}` - 它应该做什么
- `{BASE_SHA}` - 起始提交
- `{HEAD_SHA}` - 结束提交
- `{DESCRIPTION}` - 简短总结

**3. 根据反馈采取行动：**
- 立即修复 Critical 问题
- 在继续前修复 Important 问题
- 把 Minor 问题记下来以后处理
- 如果评审者错了，就用理由反驳

## 示例

```
[刚完成任务 2：添加验证函数]

你：在继续之前，我先请求代码评审。

BASE_SHA=$(git log --oneline | grep "Task 1" | head -1 | awk '{print $1}')
HEAD_SHA=$(git rev-parse HEAD)

[派发 superpowers:code-reviewer 子代理]
  WHAT_WAS_IMPLEMENTED: 为 conversation index 添加验证和修复函数
  PLAN_OR_REQUIREMENTS: docs/superpowers/plans/deployment-plan.md 中的任务 2
  BASE_SHA: a7981ec
  HEAD_SHA: 3df7661
  DESCRIPTION: 添加了 verifyIndex() 和 repairIndex()，支持 4 类问题

[子代理返回：]
  Strengths: 架构干净，测试真实
  Issues:
    Important: 缺少进度指示
    Minor: 用于汇报间隔的魔法数字（100）
  Assessment: 可以继续

你：[修复进度指示]
[继续任务 3]
```

## 与工作流的集成

**子代理驱动开发：**
- 每个任务之后评审
- 在问题累积之前就抓出来
- 修完再进入下一个任务

**执行计划：**
- 每个批次（3 个任务）之后评审
- 获取反馈，应用，再继续

**临时开发：**
- 合并前评审
- 卡住时评审

## 红旗

**绝不要：**
- 因为“这很简单”而跳过评审
- 忽略 Critical 问题
- 带着未修复的 Important 问题继续推进
- 对有效的技术反馈争辩不休

**如果评审者错了：**
- 用技术理由反驳
- 展示能证明其正确性的代码/测试
- 请求澄清

模板见：`requesting-code-review/code-reviewer.md`
