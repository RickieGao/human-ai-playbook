# Memory Strategy

Guidelines for what AI should and should not persist across sessions.

---

## What to Remember

### High Priority
- **Collaboration preferences**: Output style, review strictness, communication tone
- **Core conventions**: Naming rules, architecture decisions, tech stack choices
- **Recurring instructions**: Things the user tells you repeatedly
- **Pitfall records**: Mistakes made and the rules derived from them

### Medium Priority
- **Project phase**: Current development phase and priorities
- **Team context**: Who works on what, review processes
- **Tool preferences**: Preferred commands, workflows, slash commands

## What NOT to Remember

- **Temporary debug info**: Stack traces, one-time error messages
- **One-time context**: Ad-hoc questions unrelated to ongoing work
- **Quickly outdated info**: Specific dependency versions, current branch names
- **Derivable info**: Anything that can be inferred by reading the code

## Memory Hygiene

### When to Update
- After a pitfall is encountered and resolved
- When the user corrects your behavior
- When project conventions change
- At natural checkpoints (PR merged, phase completed)

### When to Clean Up
- When a remembered fact contradicts current code
- When a convention has been superseded
- When project phase changes make old context irrelevant

## Implementation

For Claude Code users, memory is managed through:
1. **CLAUDE.md**: Project-level persistent knowledge
2. **`.claude/` memory files**: Cross-session user preferences
3. **Progress files**: Session-to-session handoff (e.g., `claude-progress.txt`)

The key principle: **memory should reduce repetition without adding noise**.
