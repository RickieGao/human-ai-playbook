# 项目进展记录

> 记录重要方案、决策和讨论结论。过程性内容，不用于对外发布。

---

## 2026-04-06 | 架构重构：重新定位为 Harness 搭建工具

### 背景

经与用户讨论，项目从"方法论文档 + kickoff agent"重新定位为**个人 AI 协作 Harness 搭建工具**。

### 目标

用户在任意新项目中，一个命令即可迁移部署完整 harness 配置（CLAUDE.md + settings + hooks + commands + MCP）。

### 关键决策

| 决策 | 选择 | 理由 |
|------|------|------|
| 架构模式 | 方案 A（扩展 kickoff 为 harness 部署器） | 单入口更符合"一键迁移"的用户体验目标 |
| Kickoff 设计 | 两层分离（个人 profile + 项目特异配置） | 跨项目配置不变，项目差异最小化提问 |
| retrospective | 保留为独立 skill placeholder | 与 feedback channel 定位不同（主动复盘 vs 被动反馈） |
| Skill 规范 | 对齐 Anthropic 官方标准 | 减少认知摩擦，遵循 Agent Skills 开放标准 |
| 目录结构 | 双层 skill（协议库 `skills/` + 平台入口 `.claude/skills/`） | 知识资产与平台绑定分离，便于未来迁移 |
| 过程文档 | 新增 PROGRESS.md + TODO.md | 统一记录项目决策，保持上下文干净 |

### 三大支柱

1. **极简人类指南** (`guide/`) — 最少阅读量，6 篇文档精简为 2 篇
2. **Skills 体系** (`skills/`) — 核心是 kickoff 一键 harness 部署；async-comm/retrospective/persona-transfer 保留 placeholder
3. **三通道演化** (`evolution/`) — 定期自动 / 临时知识摄入 / 使用反馈

### 待讨论事项（不阻塞当前执行）

1. Kickoff 默认值和推荐策略
2. 模板体系改进
3. Telegram bot 知识摄入的工程实现
4. TDD 理念如何融入项目
5. 已有配置检测和纳入 profile 的交互设计

### 实施阶段

- **Phase 0**（当前）：过程文档建立 + 用户配置更新 ✅
- **Phase 1**：结构重组（目录重命名、文件移动、交叉引用更新）
- **Phase 2**：个人 Profile 体系
- **Phase 3**：扩展 Harness 输出
- **Phase 4**：三通道演化
- **Phase 5**：收尾（README/ROADMAP 重写、英文翻译）

---
