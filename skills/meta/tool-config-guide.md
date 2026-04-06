# Tool Configuration Guide

Recommendations for configuring AI coding tools to support effective collaboration.

---

## Context Window Management

The 200K token context window fills up fast. All configuration should minimize waste.

### Recommendations
- Remove unused MCP tools (each can consume 8-30% of context)
- Use `/compact` proactively when context exceeds 50%
- Use `/context` to monitor consumption
- Prefer agentic search (grep/find/glob) over semantic search (RAG)

## Permission Configuration

### Principle
Security permissions are programmable safety boundaries, not friction.

### Recommendations
- Use `/permissions` to pre-authorize safe, frequent commands
- Never use `--dangerously-skip-permissions`
- Authorize specific commands rather than broad categories

### Example Safe Permissions
```
# Build and test commands
npm run build
npm run test
pytest
go test ./...

# Git read operations
git status
git log
git diff
```

## Hooks

### PostToolUse
- Auto-format code after edits (e.g., prettier, black)
- Run linters after file changes

### PreCompact
- Save important state before context compression
- Write progress summary to a file

### SessionStart / SessionEnd
- Auto-load/save cross-session memory
- Update progress tracking files

## Slash Commands

### When to Create
- High-frequency, fixed-process operations (e.g., `/commit-push-pr`)
- Multi-step workflows that benefit from consistency

### When NOT to Create
- One-time operations
- Tasks easily described in natural language
- Overly complex commands (Claude understands natural language)

## Git Worktree for Parallelism

For advanced users running multiple AI instances:
```bash
git worktree add ../feature-branch feature-branch
```
- Each worktree gets its own AI instance
- Tasks must be independent (no shared file edits)
- Merge results back to main branch when done
