---
name: writing-plans
description: 当你已经有一个多步骤任务的规格或需求、并且还没开始动代码时使用
---

# 编写计划

## 概述

编写完整的实现计划，假设执行该计划的工程师对我们的代码库完全没有上下文，而且品味也值得怀疑。把他们需要知道的一切都记录下来：每个任务要改哪些文件、所需代码、可能需要查看的测试和文档、以及如何测试。把完整计划拆成易处理的小任务。DRY。YAGNI。TDD。频繁提交。

假设他们是熟练的开发者，但对我们的工具链或问题领域几乎一无所知。假设他们也不太懂良好的测试设计。

**开始时要声明：** "我正在使用 writing-plans skill 来创建实现计划。"

**上下文：** 这应当在一个专用 worktree 中运行（由 brainstorming skill 创建）。

**计划保存到：** `docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md`
- （如果用户对计划位置有偏好，则以用户偏好覆盖该默认值）

## 范围检查

如果规格涵盖多个相互独立的子系统，那么它本应在 brainstorming 阶段被拆分成多个子项目规格。如果没有，就建议把它拆成多个独立计划 - 每个子系统一个。每个计划都应当能够单独产出可工作的、可测试的软件。

## 文件结构

在定义任务之前，先梳理将要创建或修改哪些文件，以及每个文件各自负责什么。这一步会把拆分决策固定下来。

- 设计具有清晰边界和明确接口的单元。每个文件都应只有一个明确职责。
- 你最擅长推理那些你能一次放进上下文里的代码；当文件更聚焦时，你的修改也更可靠。优先选择更小、更聚焦的文件，而不是那些承担过多职责的大文件。
- 一起变化的文件应该放在一起。按职责拆分，而不是按技术层拆分。
- 在现有代码库中，要遵循既有模式。如果代码库本来就使用大文件，不要单方面重构结构 - 但如果你正在修改的某个文件已经变得难以维护，那么把拆分纳入计划是合理的。

这个结构会决定任务如何拆分。每个任务都应当产出自洽的改动，并且能够独立成立。

## 细粒度任务拆分

**每一步都是一个动作（2-5 分钟）：**
- “写出失败的测试” - 一步
- “运行它以确认它会失败” - 一步
- “编写最小实现让测试通过” - 一步
- “运行测试并确认通过” - 一步
- “提交” - 一步

## 计划文档头部

**每个计划都必须以这个头部开始：**

```markdown
# [功能名称]实现计划

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** [一句话描述这个计划要构建什么]

**Architecture:** [用 2-3 句话说明方案]

**Tech Stack:** [关键技术/库]

---
```

## 任务结构

````markdown
### Task N: [组件名称]

**Files:**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`
- Test: `tests/exact/path/to/test.py`

- [ ] **Step 1: Write the failing test**

```python
def test_specific_behavior():
    result = function(input)
    assert result == expected
```

- [ ] **Step 2: Run test to verify it fails**

Run: `pytest tests/path/test.py::test_name -v`
Expected: FAIL with "function not defined"

- [ ] **Step 3: Write minimal implementation**

```python
def function(input):
    return expected
```

- [ ] **Step 4: Run test to verify it passes**

Run: `pytest tests/path/test.py::test_name -v`
Expected: PASS

- [ ] **Step 5: Commit**

```bash
git add tests/path/test.py src/path/file.py
git commit -m "feat: add specific feature"
```
````

## 记住
- 始终给出精确文件路径
- 计划里给出完整代码（不要只写“添加校验”）
- 给出精确命令和预期输出
- 用 @ 语法引用相关技能
- DRY、YAGNI、TDD、频繁提交

## 计划评审循环

在完成计划的每个 chunk 之后：

1. 为当前 chunk 派发 `plan-document-reviewer` 子代理（见 `plan-document-reviewer-prompt.md`）
   - 提供：chunk 内容、spec 文档路径
2. 如果发现问题：
   - 修复该 chunk 中的问题
   - 为该 chunk 重新派发评审者
   - 重复，直到获得批准
3. 如果已批准：继续下一个 chunk（或者如果这是最后一个 chunk，则移交执行）

**Chunk 边界：** 使用 `## Chunk N: <name>` 标题来划分 chunk。每个 chunk 应当 <= 1000 行，并且在逻辑上自洽。

**评审循环指导：**
- 编写计划的同一个 agent 负责修复它（这样能保留上下文）
- 如果循环超过 5 次迭代，则提交给人工寻求指导
- 评审者只提供建议 - 如果你认为反馈不正确，应当解释你的分歧

## 执行移交

保存计划之后：

**"计划已完成并保存到 `docs/superpowers/plans/<filename>.md`。准备执行吗？"**

**执行路径取决于 harness 能力：**

**如果 harness 具有子代理能力（Claude Code 等）：**
- **必需：** 使用 `superpowers:subagent-driven-development`
- 不要提供选项 - subagent-driven 是标准方式
- 每个任务一个全新的子代理 + 两阶段评审

**如果 harness 没有子代理：**
- 在当前会话中使用 `superpowers:executing-plans` 执行计划
- 分批执行，并设置检查点进行评审
