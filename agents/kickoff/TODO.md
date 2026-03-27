# Kickoff Agent — 待办优化项

## 已完成

### 1. Domain 模板 ✓
- 已创建 `backend-api.md` 和 `data-ml.md` 两个最常用的领域模板
- 决策树已更新，包含领域检测启发式规则
- Web frontend 和 Mobile 模板保留为 planned，按需创建

### 2. Placeholder fallback ✓
- `_assembly-rules.md` 中新增 Placeholder Fallback 章节
- 13 个 placeholder 全部定义了 fallback 策略
- 核心原则：绝不输出原始 placeholder、省略优于占位、标记待跟进

### 3. Self-update 规则嵌入模板 ✓
- `context-management.md` 的 Self-Update 章节已扩展
- 嵌入了 5 个具体的触发信号（新依赖、重复纠正、新 pitfall 等）
- 新增"在自然停顿点建议更新"的行为约束

### 4. Rules output 集成测试 ✓
- 基于 team-monorepo 示例完成 dry-run 验证
- 确认 domain 模板与 path-scoped rules 的合并策略
- 验证结果记录在 `self-test-log.md`

## 未来可选优化

- Web frontend domain 模板（按需创建）
- Mobile domain 模板（按需创建）
- DevOps/Infrastructure domain 模板（按需创建）
- 真实项目使用后的反馈收集与迭代
