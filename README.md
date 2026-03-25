# human-ai-playbook

> 给人看方法论，给 AI 看协议，让每个项目的人机协作从第一天就顺畅。
>
> A living methodology for productive human-AI collaboration.

[English](README_EN.md)

---

## 这是什么？

一套实用的人机协作方法论 + 可执行的 Agent 系统，聚焦工程级编程场景。

### 三大产出

| # | 产出 | 服务对象 | 核心价值 |
|---|------|---------|---------|
| 1 | 方法论文档 | 人 | 建立系统认知：为什么、是什么、怎么做 |
| 2 | Agent 体系 | AI（及通过 AI 服务人） | 可执行的协作规范 |
| 3 | 自我进化机制 | 整个项目 | 持续跟上 AI 能力演进 |

### 与竞品的差异

| 维度 | 现有项目 | human-ai-playbook |
|------|---------|-------------------|
| 内容定位 | 特定工具的使用技巧 | 通用方法论 + Agent 系统 |
| 读者 | 只给人看 | 双向：人看方法论，AI 看协议 |
| 场景覆盖 | 仅编程 | 方法论通用，MVP 聚焦工程编程 |
| 更新机制 | 人工手动 | 自我进化（AI 采集 -> 提炼 -> 建议 -> 人审核） |
| 产出物 | 参考阅读 | 可执行（`/kickoff` 一键启动，从想法到方案） |

## 快速开始

1. **了解方法论**: 从 [`docs/zh/00-overview.md`](docs/zh/00-overview.md) 开始
2. **使用立项 Agent**: 在 Claude Code 中输入 `/kickoff` 启动立项流程
   - 有现有项目？自动扫描你的代码库，检测技术栈和配置
   - 只有一个想法？引导你澄清需求、调研现有方案、选择技术路线
   - 最终生成一份量身定制的 CLAUDE.md
   - 安装：将 [`.claude/commands/kickoff.md`](.claude/commands/kickoff.md) 复制到 `~/.claude/commands/` 即可全局使用
3. **遵循工作流**: Need -> Plan -> Execute -> Verify -> Document

## 项目结构

```
human-ai-playbook/
├── docs/                  # 产出一：方法论文档
│   ├── zh/                #   中文版
│   └── en/                #   英文版
├── agents/                # 产出二：Agent 体系
│   ├── meta/              #   元 Agent（宪法层）
│   ├── kickoff/           #   立项 Agent + 模板库
│   ├── async-comm/        #   (v2) 异步沟通 Agent
│   ├── retrospective/     #   (v2) 经验沉淀 Agent
│   └── persona-transfer/  #   (v3) 人格迁移 Agent
├── evolution/             # 产出三：自我进化机制
│   ├── collector/         #   信息采集
│   ├── analyzer/          #   分析提炼
│   ├── updater/           #   更新建议
│   ├── digests/           #   周报
│   └── insights/          #   洞察
├── research/              # 调研资料
└── .github/workflows/     # CI/CD 自动化
```

## 核心原则

1. **需求第一** - 需求不清晰时，AI 的执行力反而是灾难
2. **上下文工程优于提示工程** - 管理 AI"看到什么"比"怎么问"更重要
3. **先思考，再规划，再执行** - 强制分阶段，人确认后才进入下一阶段
4. **分治与增量** - 大任务拆小，每步可验证可回滚
5. **验证闭环不可省略** - AI 产出必须有验证机制
6. **人机分工清晰化** - 决策和审查归人，实现和重复归 AI
7. **渐进式信任** - 从小任务开始，逐步扩大 AI 自主权
8. **知识沉淀为资产** - 每次协作的经验都应可复用
9. **成本意识** - 不是所有任务都适合 AI，评估 ROI
10. **错误处理预案** - AI 会犯错，需要回滚和教训沉淀

详见 [`docs/zh/01-principles.md`](docs/zh/01-principles.md)

## 路线图

见 [ROADMAP.md](ROADMAP.md)

## 参与贡献

欢迎贡献！请先阅读 [`agents/_agent-design-guide.md`](agents/_agent-design-guide.md)。

## 许可证

[CC-BY-SA-4.0](LICENSE)
