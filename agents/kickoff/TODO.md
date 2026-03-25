# Kickoff Agent — 待办优化项

## 优先级排序

### 1. Domain 模板（中优先级）
- `decision-tree.md:52-57` 中 domain 模板全是 planned
- web-frontend、backend-api、mobile、data-ml 都只有占位没有内容
- 生成的 CLAUDE.md 缺少领域针对性
- **建议**: 先做 backend-api 和 data-ml 两个最常用的

### 2. Placeholder fallback（低优先级）
- `_assembly-rules.md` 定义了 placeholder 但没说检测不到时怎么办
- 可能导致生成的 CLAUDE.md 中出现 `{{test_command}}` 原文
- **建议**: 添加 fallback 规则——检测不到时使用合理默认值或标注 TODO

### 3. Self-update 规则嵌入模板（低优先级）
- `self-update.md` 是独立协议，但触发规则没有进入生成的 CLAUDE.md 模板
- `templates/base/context-management.md` 可能需要补充 self-update 触发信号
- **建议**: 在 context-management 模板中加入基本的 self-update 规则
