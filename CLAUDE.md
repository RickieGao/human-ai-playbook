# CLAUDE.md - human-ai-playbook

## Project Identity

A bilingual (Chinese/English) open-source project providing human-AI collaboration methodology and executable agent systems.

- **Primary language**: Chinese for docs, English for code and agent protocols
- **License**: CC-BY-SA-4.0
- **Current phase**: Phase 2 — Kickoff Agent complete, evolution pipeline planned

## Repository Structure

- `docs/zh/` - 方法论文档 (Chinese, primary)
- `docs/en/` - Methodology docs (English)
- `docs/superpowers/` - Plans and specs for superpowers skills
- `agents/` - Agent system (meta/, kickoff/, async-comm/, retrospective/, persona-transfer/)
- `evolution/` - Self-evolution pipeline (collector/, analyzer/, updater/)
- `research/` - Research materials and competitive analysis
- `.github/workflows/` - CI/CD automation (weekly collect & analyze)
- `.claude/` - Claude Code integration (commands, settings)

## Collaboration Mode

### Workflow
- **Plan-first**: Always present a plan before making changes. Wait for approval before executing.
- **Scope discipline**: If you discover issues outside the current task, report them and ask — don't fix silently.

### Communication
- **Detailed reporting**: After completing work, explain what was done, why, and what alternatives were considered.
- **Bilingual awareness**: All user-facing content must work for both Chinese and English readers. Use bilingual headings, examples, or parallel docs as appropriate.
- **One question at a time**: Don't overwhelm with multiple questions in a single message.

### Autonomy
- AI proposes, human decides. Never commit, push, or make irreversible changes without explicit approval.

## Quality Standards

### Writing Style
- Methodology docs: Clear, concise, actionable. Use tables for structured comparisons.
- Agent protocols: Structured markdown with clear sections. Machine-readable where possible.
- Bilingual: Chinese is primary. English translations should be natural, not literal.

### Commit Convention
- Use conventional commits: `feat:`, `fix:`, `docs:`, `chore:`
- Keep commits atomic and focused
- **Commit granularity**: One commit = one describable, independent change. If the commit message needs "and" to connect unrelated things, split it.
- **When to commit**: After completing a logical unit of work (a protocol file, a doc, a bug fix), proactively remind the user to review and commit before moving on.
- **What not to mix**: Keep content changes, config/structure changes, and cross-file fixes in separate commits.

### Verification
- Core content (agent protocols, methodology docs, templates) must be verified: cross-reference checks, self-test runs, consistency validation.
- Supporting content (README updates, comments, minor formatting) can skip verification.

## Guardrails and Pitfalls

### Key Decisions
- Meta Agent defines communication principles that all other agents must follow
- Kickoff Agent is the MVP priority — it generates CLAUDE.md for other projects
- Self-evolution uses a 4-step pipeline: collect → analyze → suggest updates → human review

### Safety Red Lines
- Do NOT modify environment variables or environment configuration
- Do NOT commit, push, or make irreversible changes without explicit approval

### Known Pitfalls
- Do not over-engineer agent protocols — start simple, iterate based on real usage
- Do not add features beyond the current phase scope
- Always consider both Chinese and English users — avoid content that only works in one language

## Context Management

### CLAUDE.md Maintenance
- This is a living document — update it when project structure, conventions, or phase changes.
- AI may suggest updates when it notices discrepancies between CLAUDE.md and actual project state.
- All updates require human approval before applying.

### Session Management
- At session start, read CLAUDE.md to establish project context.
- For large tasks, break into small verifiable steps and maintain rollback capability.
- When context grows long, summarize key decisions before continuing.
