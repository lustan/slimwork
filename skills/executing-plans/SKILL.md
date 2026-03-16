---
name: executing-plans
description: 当你有一个书面的实现计划，并且要在单独会话中带着评审检查点去执行它时使用
---

# 执行计划

## 概述

加载计划，进行批判性审查，执行所有任务，并在完成时汇报。

**开始时要声明：** "我正在使用 executing-plans skill 来实现这个计划。"

**注意：** 告诉你的人类搭档，Superpowers 在能够使用子代理时效果会好得多。如果在支持子代理的平台上运行（例如 Claude Code 或 Codex），它的工作质量会显著更高。如果子代理可用，使用 `superpowers:subagent-driven-development` 而不是这个 skill。

## 过程

### 第 1 步：加载并审查计划
1. 读取计划文件
2. 进行批判性审查 - 找出你对该计划的任何问题或担忧
3. 如果有顾虑：在开始之前向你的人类搭档提出
4. 如果没有顾虑：创建 TodoWrite 并继续

### 第 2 步：执行任务

对于每个任务：
1. 标记为 `in_progress`
2. 严格遵循每一步（计划中已经拆成细粒度步骤）
3. 按指定方式运行验证
4. 标记为 `completed`

### 第 3 步：完成开发

在所有任务都完成并验证之后：
- 宣布："我正在使用 finishing-a-development-branch skill 来完成这项工作。"
- **REQUIRED SUB-SKILL:** 使用 `superpowers:finishing-a-development-branch`
- 按照该 skill 进行验证测试、展示选项、执行选择

## 何时停止并寻求帮助

**在以下情况下立即停止执行：**
- 遇到阻塞（缺少依赖、测试失败、指令不清）
- 计划存在关键缺口，导致无法开始
- 你不理解某条指令
- 验证反复失败

**请求澄清，而不是猜测。**

## 何时回到更早的步骤

**在以下情况下返回审查阶段（第 1 步）：**
- 搭档根据你的反馈更新了计划
- 基本方案需要重新思考

**不要强行顶着阻塞继续推进** - 停下来并提问。

## 记住
- 先批判性审查计划
- 严格按照计划步骤执行
- 不要跳过验证
- 计划要求引用 skill 时就去引用
- 被阻塞时停下，不要猜
- 未经用户明确同意，绝不要在 `main`/`master` 分支上开始实现

## 集成

**必需的工作流 skill：**
- **`superpowers:using-git-worktrees`** - 必需：开始前设置隔离的工作区
- **`superpowers:writing-plans`** - 创建由本 skill 执行的计划
- **`superpowers:finishing-a-development-branch`** - 在所有任务完成后结束开发
