# CLAUDE.md - human-ai-playbook

## Project Identity

A bilingual (Chinese/English) open-source tool for building personal AI collaboration harnesses. Helps users deploy a complete harness (CLAUDE.md, settings, hooks, commands, MCP config) to any new project with a single command.

- **Primary language**: Chinese for docs, English for code and skill protocols
- **License**: CC-BY-SA-4.0
- **Current phase**: Phase 1 restructure — repositioning from methodology docs to harness building tool

## Repository Structure

- `guide/zh/` - 极简人类指南 (Chinese, primary) — 3 docs max
- `guide/en/` - Minimal guide (English)
- `skills/` - Skill protocol library (meta/, kickoff/, async-comm/, retrospective/, persona-transfer/)
- `evolution/` - Three-channel evolution pipeline (periodic/, knowledge-intake/, feedback/)
- `research/` - Research materials, competitive analysis, archived methodology docs
- `.github/workflows/` - CI/CD automation
- `.claude/skills/` - Claude Code skill entry points (official format)
- `docs/` - Project process documents (PROGRESS.md, TODO.md)

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
- Guide docs: Minimal. Each doc ≤80 lines. If it can be done by AI, don't document it for humans.
- Skill protocols: Structured markdown with clear sections. Machine-readable where possible.
- Bilingual: Chinese is primary. English translations should be natural, not literal.
- Pipeline code: GitHub Actions workflows and automation scripts should be simple, well-commented, and easy to debug.

### Commit Convention
- Use conventional commits: `feat:`, `fix:`, `docs:`, `chore:`
- Keep commits atomic and focused
- **Commit granularity**: One commit = one describable, independent change. If the commit message needs "and" to connect unrelated things, split it.
- **When to commit**: After completing a logical unit of work (a protocol file, a doc, a bug fix), proactively remind the user to review and commit before moving on.
- **What not to mix**: Keep content changes, config/structure changes, and cross-file fixes in separate commits.

### Verification
- Core content (agent protocols, methodology docs, templates) must be verified: cross-reference checks, self-test runs, consistency validation.
- Supporting content (README updates, comments, minor formatting) can skip verification.
- Pipeline code: Workflows and scripts must be tested via `workflow_dispatch` manual trigger before merging.

## Guardrails and Pitfalls

### Key Decisions
- Meta skill defines communication principles that all other skills must follow
- Kickoff skill is the core — it deploys a complete harness (not just CLAUDE.md) using a two-layer merge: personal profile + project-specific config
- Evolution uses 3 channels: periodic automated / ad-hoc knowledge intake / usage feedback

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
