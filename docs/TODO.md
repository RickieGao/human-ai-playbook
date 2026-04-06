# TODO

> 项目待办事项。状态：`[ ]` 待做 / `[x]` 完成 / `[-]` 取消 / `[~]` 进行中

---

## 架构重构（当前阶段）

### Phase 0：过程文档 + 用户配置
- [x] 创建 `docs/PROGRESS.md`
- [x] 创建 `docs/TODO.md`
- [x] 更新 `~/.claude/CLAUDE.md` — 新增过程文档更新偏好

### Phase 1：结构重组
- [ ] `agents/` → `skills/`（git mv）
- [ ] `docs/zh/*.md` → `research/archive/methodology-v1/`（归档）
- [ ] `docs/superpowers/` → `research/superpowers/`
- [ ] 创建 `guide/zh/`（新精简内容）
- [ ] kickoff 内部子目录重组（detection/ interview/ output/ new-idea/）
- [ ] 创建 `.claude/skills/` 官方格式入口（迁移自 `.claude/commands/`）
- [ ] 重写 `skills/_skill-design-guide.md` — 对齐官方规范
- [ ] 更新所有交叉引用（CLAUDE.md、README）
- [ ] 验证：`/kickoff` 在新路径下正常工作

### Phase 2：个人 Profile 体系
- [ ] 创建 `skills/kickoff/profile/schema.md`
- [ ] 创建 `skills/kickoff/profile/template.md`
- [ ] 创建 `skills/kickoff/profile/profile-guide.md`
- [ ] 创建 `skills/kickoff/profile/examples/`
- [ ] 创建 `skills/kickoff/merge/merge-strategy.md`
- [ ] 创建 `skills/kickoff/merge/conflict-resolution.md`
- [ ] 重写 `skills/kickoff/SKILL.md` — 两层合并流程
- [ ] 更新 `interview-protocol.md` — 降级为 profile 创建 fallback
- [ ] 自测：有 profile / 无 profile 两种路径

### Phase 3：扩展 Harness 输出
- [ ] 创建 `skills/kickoff/output/settings-generator.md`
- [ ] 扩展 assembly-rules — 支持 settings/hooks/MCP 输出
- [ ] 扩展 staged-review — 覆盖所有输出文件类型
- [ ] 新增 hooks 和 MCP 配置模板片段
- [ ] 自测：solo/team/monorepo 三种场景完整输出

### Phase 4：三通道演化
- [ ] 重组 `evolution/` — 创建 channels/ 结构
- [ ] 创建 `evolution/channels/knowledge-intake/`
- [ ] 创建 `evolution/channels/feedback/`
- [ ] 创建 `.claude/skills/process-knowledge/`
- [ ] 创建 `.claude/skills/harness-feedback/`
- [ ] 编写 `evolution/merge-protocol.md`

### Phase 5：收尾
- [ ] 重写 `README.md` — 新定位
- [ ] 重写 `README_EN.md`
- [ ] 更新 `ROADMAP.md`
- [ ] 更新 `CLAUDE.md`（项目级）
- [ ] 英文 guide 翻译
- [ ] 更新 `CHANGELOG.md`

---

## 待讨论（不阻塞执行）

- [ ] Kickoff 默认值和推荐策略设计
- [ ] 模板体系改进方案
- [ ] Telegram bot 知识摄入工程实现
- [ ] TDD 理念融入项目的具体方式
- [ ] 已有配置检测和纳入 profile 的交互设计
