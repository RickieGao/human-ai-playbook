# human-ai-playbook — MVP 蓝图 v3（最终版）

> 一份持续进化的人机协作方法论，帮助人和 AI 建立高效的协作关系。
> A living methodology for productive human-AI collaboration.

---

## 一、项目定位

### Tagline
**给人看方法论，给 AI 看协议，让每个项目的人机协作从第一天就顺畅。**

### 三大产出
| # | 产出 | 服务对象 | 核心价值 |
|---|------|---------|---------|
| 1 | 方法论文档 | 人 | 建立系统认知：为什么、是什么、怎么做 |
| 2 | Agent 体系 | AI（及通过 AI 服务人） | 可执行的协作规范，引导人完成各阶段工作 |
| 3 | 自我进化机制 | 整个项目 | 让方法论和 Agent 持续跟上 AI 能力的演进 |

### 与竞品的差异
| 维度 | 现有项目 | human-ai-playbook |
|------|---------|-------------------|
| 内容定位 | 特定工具的使用技巧汇编 | 通用方法论 + 可落地的 Agent 系统 |
| 读者 | 只给人看 | 双向：人看方法论，AI 看协议 |
| 场景覆盖 | 仅编程 | 方法论通用，MVP 聚焦工程级编程 |
| 更新机制 | 人工手动 | 自我进化（AI 采集 → 提炼 → 建议更新 → 人审核） |
| 产出物 | 参考阅读 | 可执行（Agent 引导生成 CLAUDE.md + 项目结构） |

---

## 二、系统架构

### 三大产出的关系

```
┌────────────────────────────────────────────────────────────┐
│                  产出一：方法论文档（给人看）                    │
│            原则 · 工作流 · 上下文工程 · 实践指南                 │
│                     ↑ 理论基础                               │
│                     │                                       │
│                  产出二：Agent 体系（给 AI 看）                 │
│            元 Agent · 立项 Agent · [未来更多 Agent]            │
│                     ↑↓ 双向更新                              │
│                     │                                       │
│                  产出三：自我进化机制                            │
│            采集 → 提炼 → 评估 → 建议更新 → 人审核               │
└────────────────────────────────────────────────────────────┘
```

### Agent 体系的内部架构

```
┌─────────────────────────────────────────────────────────┐
│                    元 Agent（宪法层）                       │
│         定义人机沟通的底层原则、AI 行为规范、                    │
│         memory 策略、工具配置建议                             │
└────────────────────────┬────────────────────────────────┘
                         │ 约束与指导
        ┌────────────────┼─────────────────┐
        ▼                ▼                 ▼
┌──────────────┐ ┌───────────────┐ ┌──────────────┐
│  项目立项      │ │  异步沟通机制   │ │  经验沉淀与    │
│  Agent       │ │  搭建 Agent   │ │  迁移 Agent   │
│  (含模板库)   │ │               │ │              │
│  ★ MVP      │ │  ○ v2        │ │  ○ v2        │
└──────────────┘ └───────────────┘ └──────────────┘

★ = MVP 实现    ○ = 蓝图占位，v2+ 实现
```

### Agent 生命周期覆盖（完整愿景）

```
项目生命周期：  立项 → 日常协作 → 阶段回顾 → 项目结束/迁移
                │        │          │            │
对应 Agent：   立项     异步沟通     经验沉淀      人格迁移
              Agent    Agent      Agent        Agent
              ★ MVP   ○ v2      ○ v2         ○ v3

贯穿全程：     元 Agent（宪法层）★ MVP
              协作质量诊断 Agent ○ v3
              需求澄清 Agent ○ v2
```

---

## 三、MVP 仓库结构

```
human-ai-playbook/
│
├── README.md                              # 项目门面（中文）
├── README_EN.md                           # English version
├── LICENSE                                # CC-BY-SA-4.0
├── CHANGELOG.md
├── ROADMAP.md                             # 完整愿景与版本路线图
│
├── docs/                                  # ═══ 产出一：方法论文档 ═══
│   ├── zh/
│   │   ├── 00-overview.md                 # 总览
│   │   ├── 01-principles.md               # 核心原则（通用层）
│   │   ├── 02-workflow.md                 # 协作工作流框架
│   │   ├── 03-context-engineering.md      # 上下文工程
│   │   ├── 04-programming-guide.md        # 编程场景实践指南
│   │   └── 05-anti-patterns.md            # 反模式与常见陷阱
│   └── en/
│       └── ...
│
├── agents/                                # ═══ 产出二：Agent 体系 ═══
│   ├── meta/                              # 元 Agent（宪法层）★ MVP
│   │   ├── SKILL.md                       #   AI 沟通原则总纲
│   │   ├── communication-protocol.md      #   分场景沟通规范
│   │   ├── memory-strategy.md             #   Memory 策略
│   │   └── tool-config-guide.md           #   工具配置建议
│   │
│   ├── kickoff/                           # 项目立项 Agent ★ MVP
│   │   ├── SKILL.md                       #   立项引导流程
│   │   ├── interview-protocol.md          #   对话协议
│   │   ├── decision-tree.md               #   决策树
│   │   ├── templates/                     #   CLAUDE.md 模板片段库
│   │   │   ├── _assembly-rules.md
│   │   │   ├── base/
│   │   │   │   ├── project-identity.md
│   │   │   │   ├── collaboration-mode.md
│   │   │   │   ├── quality-standards.md
│   │   │   │   └── context-management.md
│   │   │   ├── workflow/
│   │   │   │   ├── tdd-workflow.md
│   │   │   │   ├── plan-first-workflow.md
│   │   │   │   ├── spec-driven-workflow.md
│   │   │   │   └── incremental-workflow.md
│   │   │   ├── scale/
│   │   │   │   ├── solo-developer.md
│   │   │   │   ├── small-team.md
│   │   │   │   └── monorepo.md
│   │   │   └── domain/
│   │   │       └── _placeholder.md
│   │   └── examples/
│   │       ├── fullstack-solo.md
│   │       └── team-monorepo.md
│   │
│   ├── async-comm/                        # ○ v2
│   │   └── _placeholder.md
│   ├── retrospective/                     # ○ v2
│   │   └── _placeholder.md
│   ├── persona-transfer/                  # ○ v3
│   │   └── _placeholder.md
│   └── _agent-design-guide.md             # Agent 贡献规范
│
├── evolution/                             # ═══ 产出三：自我进化机制 ═══
│   ├── collector/
│   │   ├── search-config.yaml
│   │   ├── collect-prompt.md
│   │   └── digest-template.md
│   ├── analyzer/
│   │   ├── analyze-prompt.md
│   │   └── relevance-criteria.md
│   ├── updater/
│   │   ├── update-prompt.md
│   │   ├── update-rules.md
│   │   └── review-template.md
│   ├── digests/
│   │   └── 2026-W12.md
│   └── insights/
│       └── _template.md
│
├── .github/workflows/
│   ├── weekly-collect.yml
│   └── weekly-analyze.yml
│
└── research/
    ├── competitive-analysis.md
    └── source-survey.md
```

---

## 四、核心内容设计

### 产出一：方法论文档

#### 核心原则（01-principles.md）

| # | 原则 | 一句话 |
|---|------|-------|
| 1 | 需求第一 | 需求不清晰时，AI 的执行力反而是灾难 |
| 2 | 上下文工程优于提示工程 | 管理 AI"看到什么"比"怎么问"更重要 |
| 3 | 先思考，再规划，再执行 | 强制分阶段，人确认后才进入下一阶段 |
| 4 | 分治与增量 | 大任务拆小，每步可验证可回滚 |
| 5 | 验证闭环不可省略 | AI 产出必须有验证机制 |
| 6 | 人机分工清晰化 | 决策和审查归人，实现和重复归 AI |
| 7 | 渐进式信任 | 从小任务开始，逐步扩大 AI 自主权 |
| 8 | 知识沉淀为资产 | 每次协作的经验都应可复用 |
| 9 | 成本意识 | 不是所有任务都适合 AI，评估 ROI |
| 10 | 错误处理预案 | AI 会犯错，需要回滚和教训沉淀 |

#### 其余文档
- 00-overview：为什么需要方法论 + METR 研究启示 + 快速开始
- 02-workflow：Need → Plan → Execute → Verify → Document 循环
- 03-context-engineering：窗口管理、CLAUDE.md 设计、外部记忆
- 04-programming-guide：工程级编程的 Research → Plan → Execute → Review → Ship
- 05-anti-patterns：六大常见陷阱

### 产出二：Agent 体系

#### 元 Agent — 五大沟通原则
1. 透明性：坦诚能力边界，不确定时说"我不确定"
2. 主动性与边界：授权内主动推进，越界时停下请示
3. 沟通效率：长度匹配复杂度，提问给选项，不明确先澄清
4. 知识管理：识别值得沉淀的信息，关键节点自动总结
5. 错误处理：承认→分析→修复，不重复同类错误

#### 元 Agent — Memory 策略
- 应记：协作偏好、核心约定、反复指令、踩坑记录
- 不记：临时调试信息、一次性上下文、可能过时的信息

#### 元 Agent — 分场景沟通协议
五个典型场景：收到任务、遇到问题、任务完成、异步恢复、发现需求问题

#### 立项 Agent — 三轮引导 + 生成
项目基本面 → 协作偏好 → 环境配置 → 组装 CLAUDE.md + 项目结构 + memory 建议

### 产出三：自我进化机制

#### 四步流水线
采集（collector/）→ 分析（analyzer/）→ 更新建议（updater/）→ 人审核

#### 更新紧迫度
- 高（1 周内）：现有内容含已证伪信息或导致风险
- 中（1 月内）：有更好实践或需补充新特性
- 低（季度评审）：措辞优化、示例更新

---

## 五、开发阶段

不设硬期限，按节奏推进。

### Phase 1：地基
README + ROADMAP + 核心原则 + 元 Agent 宪法 + 调研资料入库
→ 完成标志：读完后能理解项目定位和方法论

### Phase 2：核心能力
立项 Agent 全套 + 模板片段库 + 自测 3+ 次
→ 完成标志：30 分钟内生成可用 CLAUDE.md

### Phase 3：进化引擎
进化机制全套 + GitHub Action + 前 2 期周报
→ 完成标志：每周自动产出周报 + 更新建议

### Phase 4：内容与打磨
方法论全部 6 篇 + 英文版 + 3-5 人用户测试
→ 完成标志：3+ 外部用户正面反馈

### Phase 5：发布
发布文章 + 多平台推广 + Contributing 指南

---

## 六、成功标准

**MVP**：30 分钟生成可用 CLAUDE.md · 方法论建立系统认知 · 进化流水线运行 · 3+ 用户验证
**6 个月**：500+ Stars · 3+ 工作类型 · v2 Agent 上线 · 10+ 贡献者
**12 个月**：标准参考项目 · Agent 覆盖全生命周期 · 社区更新 > 维护者更新
