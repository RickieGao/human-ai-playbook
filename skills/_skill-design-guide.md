# Skill Design Guide

How to contribute new skills to the human-ai-playbook system.

This project follows the [Agent Skills open standard](https://agentskills.io) as used by Claude Code.

---

## Skill Structure

Each skill lives in its own directory under `skills/`:

```
skills/
  my-skill/
    SKILL.md              # Main entry point (required)
    [supporting files]    # Protocols, templates, examples, scripts
```

The corresponding Claude Code entry point lives at:

```
.claude/skills/my-skill/
  SKILL.md                # Official format with YAML frontmatter
```

The `skills/` directory is the protocol library (platform-agnostic). The `.claude/skills/` directory is the platform binding (Claude Code specific).

---

## SKILL.md Format

### Claude Code entry point (`.claude/skills/<name>/SKILL.md`)

Uses official YAML frontmatter:

```yaml
---
name: skill-name
description: What the skill does and when to use it. Front-load the key use case. Max 250 chars.
disable-model-invocation: true   # Set true for workflow skills you trigger manually
user-invocable: true             # Set false for background knowledge skills
allowed-tools: Read Grep Glob    # Restrict tool access when needed
context: fork                    # Set to run in isolated subagent
agent: Explore                   # Subagent type when context: fork (Explore/Plan/general-purpose)
---

Skill instructions...

Reference supporting files from skills/<name>/ so Claude knows what to load:
- For detection logic, see [skills/my-skill/detection.md](../../../skills/my-skill/detection.md)
```

### Protocol library entry point (`skills/<name>/SKILL.md`)

Plain markdown, no frontmatter required. Sections:

```markdown
# [Skill Name]

## Overview
What this skill does and when to use it.

## Flow
Step-by-step process (ASCII diagram for complex flows).

## Protocols
Table of supporting protocol files and their purpose.

## Design Principles
Skill-specific rules beyond the Meta Skill principles.
```

---

## Frontmatter Field Reference

| Field | Use when |
|-------|----------|
| `disable-model-invocation: true` | Workflow skills with side effects (deploy, commit, kickoff) |
| `user-invocable: false` | Background knowledge Claude loads automatically |
| `allowed-tools` | Need to restrict Claude to specific tools |
| `context: fork` | Skill should run in isolated context (no conversation history) |
| `agent: Explore` | Research tasks; use `Plan` for design tasks |

---

## Requirements

1. **SKILL.md required** in both `skills/<name>/` and `.claude/skills/<name>/`
2. **Inherit Meta Skill principles**: All skills follow `skills/meta/SKILL.md`
3. **Human-reviewable outputs**: Never apply changes without human confirmation
4. **Keep SKILL.md under 500 lines**: Move detailed reference to supporting files

---

## Naming Conventions

- Directory: lowercase, hyphenated (`async-comm`, `persona-transfer`)
- Files: `SKILL.md` uppercase, supporting files lowercase-hyphenated
- Slash command: matches directory name (`/kickoff`, `/async-comm`)

---

## Testing

Before submitting a new skill:
- [ ] Run through the full flow at least 3 times with different scenarios
- [ ] Test both automatic invocation (if enabled) and manual `/skill-name`
- [ ] Verify all path references to protocol files are correct
- [ ] Check Meta Skill principles are followed
- [ ] Verify outputs are human-reviewable before application
