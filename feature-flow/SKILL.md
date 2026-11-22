---
name: feature-flow
description: >-
  结合 Matt Pocock 系列 Skills（grilling、to-spec、to-tickets、tdd、implement-spec、
  code-review、handoff）与多模型 Swarm 编排的端到端功能开发工作流。当用户要求开发新功能、
  或明确要求按标准 feature-flow 流程推进需求时使用。
---

# Feature Flow（Matt Pocock Skills + 多模型 Swarm 编排）

标准端到端研发工作流，明确拆分规划、实现与审查阶段的模型分工。

## 模型分工偏好

- **主模型（协调 / 规划）**：`Gemini 4 Neon`
- **具体任务执行（Swarm Worker）**：`Gemini 4 Hydrogen` 或 `Claude Sonnet 5.5`
- **代码审查（Review）**：`Gemini 4 Neon` 或 `Claude Opus 5.5`

在启动 Swarm Worker 之前，先调用 `swarm(action="models")` 确认可用模型的精确名称。

## 执行步骤

### 1. 需求对齐与规格拆解（主模型：`Gemini 4 Neon`）
- 除非用户明确说明需求已完全确定，否则先使用 **`grilling`**（若项目已有架构/业务文档，可使用 **`grill-with-docs`**），在写代码前通过提问对齐所有细节与边界条件。
- 对齐完成后，使用 **`to-spec`** 输出结构化的技术规格文档（例如 `docs/specs/<feature>.md`）。
- 若改动涉及多个模块或步骤，使用 **`to-tickets`** 将 Spec 拆解为独立、可验证的小任务（Tickets）。

### 2. 并行 TDD 实现（Swarm Worker：`Gemini 4 Hydrogen` / `Claude Sonnet 5.5`）
- 启动 **`swarm`**（并行修改代码时使用 `workspace: "share"` 隔离工作区），为实现 Worker 指定 `Gemini 4 Hydrogen` 或 `Claude Sonnet 5.5`。
- 在派发简报（brief）中明确要求 Worker 严格遵循 **`tdd`**（红-绿-重构）与 **`implement-spec`** 规范，并在汇报完成前跑通所有相关测试。
- 若任务较小（仅单个 Ticket）且无需并行，可在当前会话直接按 `tdd` 与 `implement-spec` 实现；如需新开会话或切换模型接力，使用 **`handoff`** 沉淀交接文档。

### 3. 代码审查与收尾（`Gemini 4 Neon` / `Claude Opus 5.5`）
- 所有实现改动合并后，由 `Gemini 4 Neon`（主模型）或独立审查 Worker（`Claude Opus 5.5`）对照 Spec 文档执行 **`code-review`**。
- 核查边界条件、安全性与测试通过情况，向用户汇总最终改动与验证结果。
