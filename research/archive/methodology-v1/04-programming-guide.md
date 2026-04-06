# 编程场景实践指南

工程级编程的人机协作实践，基于多个信源的共识提炼。

---

## 工作流: Research -> Plan -> Execute -> Review -> Ship

### 1. Research (探索)

让 AI 先了解代码库再动手。

```
"Read the relevant source files and understand the current architecture
before making any changes."
```

- 使用 agentic search (grep/find/glob)，而非语义搜索
- 先理解现有代码，再提改动方案

### 2. Plan (规划)

进入 Plan Mode，让 AI 提出方案。

- 大多数 session 以 Plan Mode 开始（Shift+Tab x2）
- AI 产出计划后，人审查、调整、确认
- 满意后切 auto-accept 进入执行

### 3. Execute (执行)

AI 按计划实现，每步 commit。

- 每次只做一个 feature
- 用 git worktree 实现多实例并行（进阶）
- 遇到计划外问题，停下来讨论

### 4. Review (审查)

人审查 AI 产出的代码。

- AI 生成代码需要不同的 review 方式
- 关注：逻辑正确性、边界情况、安全性、是否符合项目约定
- "Challenge Claude": 让它证明代码能用，然后才提 PR

### 5. Ship (发布)

合并代码、更新文档、沉淀经验。

- 每个错误变成 CLAUDE.md 中的一条规则
- 用 slash commands 封装高频操作

---

## TDD 与 AI 协作

TDD 在 AI 协作中变得更强大：

```
1. 人写测试用例（定义"正确"是什么）
2. 运行测试，确认失败
3. AI 写实现代码
4. 运行测试，确认通过
5. AI 重构（保持测试通过）
```

为什么 TDD 特别适合 AI 协作：
- 测试定义了明确的验收标准
- AI 的实现有自动化验证
- 避免了"AI 觉得对但实际不对"的问题

## 并行工作模式（进阶）

使用 git worktree 同时运行多个 AI 实例：

- 每个 worktree 处理一个独立任务
- 任务之间无代码依赖
- Boris Cherny: 同时运行 5 个终端实例

## Slash Commands 最佳实践

封装高频工作流，但不要过度：

- 好的: `/commit-push-pr`（高频、流程固定）
- 不好的: 过多复杂的自定义 commands（Claude 本就理解自然语言）

## 模型选择建议

- Opus: 规划、架构决策、复杂推理
- Sonnet: 日常编码、实现
- 安全相关: 使用最强推理能力的模型
