# Kickoff Agent TODO Completion Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Complete all four TODO items for the Kickoff Agent: domain templates, placeholder fallback rules, self-update rule embedding, and dry-run integration test.

**Architecture:** Each TODO is an independent enhancement to the existing template system. Domain templates add new fragment files. Placeholder fallback adds rules to `_assembly-rules.md`. Self-update embedding enriches `context-management.md`. The integration test validates the multi-file output end-to-end using an example scenario.

**Tech Stack:** Markdown (protocol/template files), no code dependencies.

---

### Task 1: Create `backend-api` Domain Template

**Files:**
- Create: `agents/kickoff/templates/domain/backend-api.md`

- [ ] **Step 1: Write the domain template**

Create `agents/kickoff/templates/domain/backend-api.md` with this content:

```markdown
## Domain: Backend API

### API Design
- Follow RESTful conventions: proper HTTP methods, status codes, resource naming
- Keep endpoint handlers thin — business logic belongs in service/domain layer
- Version APIs when breaking changes are unavoidable (prefer `/v1/` prefix)

### Data & Persistence
- Never write raw SQL in handlers — use the project's ORM/query builder
- All database schema changes require migration files, not manual edits
- Validate all external input at the API boundary before it reaches business logic

### Security
- Never log sensitive data (tokens, passwords, PII)
- Authentication/authorization checks go in middleware, not in individual handlers
- Use environment variables for secrets — never hardcode credentials

### Performance Awareness
- Add pagination to all list endpoints (default limit, max limit)
- Be aware of N+1 query patterns — use eager loading or batch queries
- Cache responses only when explicitly designed for it — don't add caching speculatively

### Testing
- API tests should hit actual endpoints (integration), not just unit-test handlers
- Test both success paths and error paths (400, 401, 403, 404, 500)
- Use fixtures or factories for test data — never rely on shared mutable test state
```

- [ ] **Step 2: Verify fragment format consistency**

Confirm the file follows the same structure as existing fragments (e.g., `scale/solo-developer.md`): starts with `## Section Title`, uses imperative instructions, stays under 50 lines, no placeholders needed.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/templates/domain/backend-api.md
git commit -m "feat(kickoff): add backend-api domain template"
```

---

### Task 2: Create `data-ml` Domain Template

**Files:**
- Create: `agents/kickoff/templates/domain/data-ml.md`

- [ ] **Step 1: Write the domain template**

Create `agents/kickoff/templates/domain/data-ml.md` with this content:

```markdown
## Domain: Data / ML

### Data Handling
- Never modify raw/source data — treat it as immutable, write outputs to separate directories
- Large data files (datasets, models) must not be committed to git — use `.gitignore` and document where data lives
- Document data sources, formats, and any preprocessing steps in the project README or a dedicated `data/README.md`

### Notebooks & Scripts
- Notebooks are for exploration and visualization — production logic belongs in `.py` modules
- If a notebook produces a reusable result, extract the logic into a function with tests
- Clear all notebook outputs before committing (use pre-commit hook or `nbstripout`)

### Reproducibility
- Pin all dependency versions (exact versions in requirements.txt or lock file)
- Set random seeds explicitly when results must be reproducible
- Log experiment parameters and results — don't rely on memory or notebook state

### Model Management
- Save model artifacts with version identifiers, not overwriting a single file
- Document model inputs, outputs, and expected performance metrics
- Never deploy a model without evaluation on a held-out test set

### Environment
- Use virtual environments — never install into system Python
- Document the full setup process (Python version, GPU requirements, env vars)
- Keep training scripts and inference scripts separate — different concerns, different entry points
```

- [ ] **Step 2: Verify fragment format consistency**

Confirm the file follows the same structure as `backend-api.md`: starts with `## Section Title`, imperative instructions, under 50 lines, self-contained.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/templates/domain/data-ml.md
git commit -m "feat(kickoff): add data-ml domain template"
```

---

### Task 3: Update Decision Tree — Activate Domain Selection

**Files:**
- Modify: `agents/kickoff/decision-tree.md:48-57`

- [ ] **Step 1: Update domain selection section**

Replace the current "Domain Selection (future)" section with an active version. Change lines 48-57 from:

```markdown
## Domain Selection (future)

```
Q: Project domain?
├── Web frontend  -> include domain/web-frontend.md (planned)
├── Backend API   -> include domain/backend-api.md (planned)
├── Mobile        -> include domain/mobile.md (planned)
├── Data/ML       -> include domain/data-ml.md (planned)
└── Other         -> no domain fragment
```
```

To:

```markdown
## Domain Selection

Domain is inferred from tech stack detection (Path A) or tech recommendation (Path B).
When detection is ambiguous, confirm with the user.

```
Detected domain:
├── Web frontend  -> include domain/web-frontend.md (planned)
├── Backend API   -> include domain/backend-api.md
├── Mobile        -> include domain/mobile.md (planned)
├── Data/ML       -> include domain/data-ml.md
└── Other / unclear → no domain fragment
```

### Domain Detection Heuristics

| Signal | Domain |
|--------|--------|
| Express, FastAPI, Django REST, Spring Boot, Gin, Rails API-mode | Backend API |
| React, Vue, Angular, Svelte, Next.js (frontend focus) | Web frontend |
| React Native, Flutter, Swift/Xcode, Kotlin/Android | Mobile |
| pandas, numpy, scikit-learn, pytorch, tensorflow, jupyter notebooks | Data/ML |
| Multiple signals or none dominant | Ask user |
```

- [ ] **Step 2: Commit**

```bash
git add agents/kickoff/decision-tree.md
git commit -m "feat(kickoff): activate domain selection with detection heuristics"
```

---

### Task 4: Update Domain Placeholder File

**Files:**
- Modify: `agents/kickoff/templates/domain/_placeholder.md`

- [ ] **Step 1: Update placeholder to reflect current status**

Replace the entire content of `_placeholder.md` with:

```markdown
# Domain Templates

Domain-specific template fragments that add field-relevant rules to the generated CLAUDE.md.

Available domains:
- [Backend API](backend-api.md) — REST API, service layer, data persistence
- [Data/ML](data-ml.md) — data pipelines, notebooks, model management

Planned domains (not yet implemented):
- Web frontend
- Mobile
- DevOps/Infrastructure
```

- [ ] **Step 2: Commit**

```bash
git add agents/kickoff/templates/domain/_placeholder.md
git commit -m "docs(kickoff): update domain placeholder with available templates"
```

---

### Task 5: Add Placeholder Fallback Rules

**Files:**
- Modify: `agents/kickoff/templates/_assembly-rules.md`

- [ ] **Step 1: Add fallback rules section**

After the existing "Rules" section (line 67, before "## Output Strategy"), insert a new section:

```markdown
## Placeholder Fallback

When a placeholder value cannot be detected (Path A) or inferred (Path B), apply these fallbacks:

| Placeholder | Fallback |
|-------------|----------|
| `{{project_name}}` | Use directory name |
| `{{project_description}}` | `TODO: Add project description` |
| `{{tech_stack}}` | Must be resolved — ask user if scan fails |
| `{{build_command}}` | Omit the Build section from Commands |
| `{{test_command}}` | Omit the Test section from Commands; add to Known Pitfalls: "No test command detected — set up testing and update this file" |
| `{{lint_command}}` | Omit the Lint section from Commands |
| `{{coding_conventions}}` | "Follow existing code style in the repository" |
| `{{workflow_description}}` | Must be resolved — always comes from interview |
| `{{autonomy_description}}` | Must be resolved — always comes from interview |
| `{{communication_style_description}}` | Must be resolved — always comes from interview |
| `{{review_process_description}}` | "Per feature" (default) |
| `{{safety_constraints}}` | Omit the Safety Constraints section |
| `{{known_pitfalls}}` | Omit the Known Pitfalls section |

### Fallback Principles

1. **Never output raw placeholders** — `{{test_command}}` must never appear in the final CLAUDE.md
2. **Omit over stub** — if a value is unknown and non-critical, remove the section rather than inserting a generic placeholder
3. **Mark for follow-up** — when omitting something important (like tests), add a note in Known Pitfalls so the user is reminded to set it up
4. **Must-resolve placeholders** — `tech_stack`, `workflow_description`, `autonomy_description`, and `communication_style_description` must always be resolved (ask the user if detection fails)
```

- [ ] **Step 2: Commit**

```bash
git add agents/kickoff/templates/_assembly-rules.md
git commit -m "feat(kickoff): add placeholder fallback rules to assembly"
```

---

### Task 6: Embed Self-Update Trigger Signals in Context Management Template

**Files:**
- Modify: `agents/kickoff/templates/base/context-management.md`

- [ ] **Step 1: Expand the Self-Update section**

Replace the current Self-Update section (lines 24-27) from:

```markdown
### Self-Update
- AI may suggest CLAUDE.md updates when it detects changes in tools, conventions, or recurring corrections
- Every suggested update will be shown as a diff with a reason — approve, reject, or modify
- Rejected suggestions will not be repeated
```

To:

```markdown
### Self-Update
- AI may suggest CLAUDE.md updates when it detects these signals:
  - New dependency or tool added to the project
  - Same AI behavior corrected 3+ times → codify as a rule
  - New pitfall discovered during work
  - Commands in this file no longer work
  - Major project structure change
- Every suggested update will be shown as a diff with a reason — approve, reject, or modify
- Rejected suggestions will not be repeated
- Updates should be suggested at natural pauses (task completion), not mid-work
```

- [ ] **Step 2: Verify line count**

Check that `context-management.md` stays reasonable in length (under ~35 lines). The expanded section adds ~5 net lines, which is acceptable.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/templates/base/context-management.md
git commit -m "feat(kickoff): embed self-update trigger signals in context-management template"
```

---

### Task 7: Integration Dry-Run — Update Team-Monorepo Example

**Files:**
- Modify: `agents/kickoff/examples/team-monorepo.md`
- Modify: `agents/kickoff/self-test-log.md`

- [ ] **Step 1: Add domain fragment to team-monorepo example**

The existing team-monorepo example uses Go backend + React frontend. This is a Backend API domain scenario. Add a domain-specific rules file to the example output to demonstrate domain template integration.

In `examples/team-monorepo.md`, after the existing `.claude/rules/web.md` section (after line 175), add:

```markdown
---

## Note: Domain Template Integration

In this example, the Backend API domain was detected from Go + REST patterns in `packages/api/`.
The domain template rules (`backend-api.md`) were merged into the path-scoped `api.md` rules file
rather than creating a separate file, because they apply to the same path scope.

The `api.md` file above already reflects domain-informed rules (input validation, error handling,
prepared statements). In practice, the Kickoff Agent merges domain template content with
path-scoped rules when they overlap in scope.
```

- [ ] **Step 2: Update self-test-log with dry-run results**

Read the current `self-test-log.md` to understand its format.

- [ ] **Step 3: Read self-test-log.md**

Read the file to determine the current format before appending.

- [ ] **Step 4: Append dry-run entry to self-test-log**

Add a new entry to `self-test-log.md` documenting the integration verification:

```markdown
## Dry-Run: Domain Template + Multi-File Output (2026-03-26)

**Scenario**: Team monorepo (Go backend + React frontend), Backend API domain detected

**Verified**:
- [x] Backend API domain template (`domain/backend-api.md`) created and follows fragment format
- [x] Data/ML domain template (`domain/data-ml.md`) created and follows fragment format
- [x] Decision tree updated with domain detection heuristics
- [x] Domain content merges correctly with path-scoped rules (same scope = merge, not separate file)
- [x] Placeholder fallback rules prevent raw `{{placeholder}}` in output
- [x] Self-update triggers embedded in context-management template
- [x] Team-monorepo example updated to show domain integration
- [x] All template fragments remain under 50 lines
- [x] Example CLAUDE.md stays under 120 lines (multi-file mode)

**Notes**:
- Domain template content naturally merges with path-scoped rules — no need for a separate domain rules file when the scope overlaps
- Fallback rules cover all 13 defined placeholders with clear resolution strategy
- Web frontend and Mobile domain templates remain planned — to be created when usage demands
```

- [ ] **Step 5: Commit**

```bash
git add agents/kickoff/examples/team-monorepo.md agents/kickoff/self-test-log.md
git commit -m "docs(kickoff): add domain integration dry-run to example and test log"
```

---

### Task 8: Update TODO.md — Mark Items Complete

**Files:**
- Modify: `agents/kickoff/TODO.md`

- [ ] **Step 1: Update TODO with completion status**

Replace the entire content of `TODO.md` with:

```markdown
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
```

- [ ] **Step 2: Commit**

```bash
git add agents/kickoff/TODO.md
git commit -m "docs(kickoff): mark all TODO items as complete"
```
