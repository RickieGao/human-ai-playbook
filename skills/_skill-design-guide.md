# Agent Design Guide

How to contribute new agents to the human-ai-playbook system.

## Agent Structure

Each agent lives in its own directory under `agents/`:

```
agents/
  my-agent/
    SKILL.md           # Main entry point (required)
    [supporting files]  # Protocols, configs, templates
```

## Requirements

1. **SKILL.md is required**: This is the agent's main definition file
2. **Follow Meta Agent principles**: All agents inherit from `agents/meta/SKILL.md`
3. **Self-contained**: Each agent should work independently
4. **Human-reviewable outputs**: Never apply changes without human confirmation

## SKILL.md Template

```markdown
# [Agent Name] - [One-line Description]

## Overview
[What this agent does and when to use it]

## Process
[Step-by-step flow]

## Input
[What information/context the agent needs]

## Output
[What the agent produces]

## Design Principles
[Agent-specific rules beyond the Meta Agent principles]
```

## Naming Conventions

- Directory: lowercase, hyphenated (`async-comm`, `persona-transfer`)
- SKILL.md: Always uppercase
- Supporting files: lowercase, hyphenated

## Testing

Before submitting a new agent:
- [ ] Run through the full flow at least 3 times
- [ ] Test with different input scenarios
- [ ] Verify outputs are correct and useful
- [ ] Check that Meta Agent principles are followed
