# CLAUDE.md Self-Update Mechanism

AI can detect when CLAUDE.md needs updating and suggest changes,
but every update requires user review and approval.

## Trigger Signals

| Signal | Suggested Update |
|--------|-----------------|
| New dependency/tool added | Add to tech stack and related commands |
| User corrects same AI behavior 3+ times | Codify the correction as a rule |
| New pitfall discovered during work | Add to known pitfalls |
| User changes collaboration preference | Update collaboration mode |
| Major project structure change | Update project identity and scale config |
| Commands in CLAUDE.md no longer work | Fix commands |

## Update Flow

```
AI detects update signal
  → Wait for natural pause (task completion or break)
    → Present: current content vs suggested change + reason
      → User approves → Write change
      → User rejects → Do not change, remember user's judgment
      → User modifies → Write user's version
```

## Presentation Format

Use diff format for clarity:

> "I noticed you've told me three times not to add comments automatically.
> Suggest adding a rule to CLAUDE.md:
>
> ```diff
> ## Collaboration Mode
> + - Do not add explanatory comments in code unless explicitly asked
> ```
>
> Add this?"

## Behavioral Constraints

1. **Don't interrupt current work** — suggest at task completion or natural pauses
2. **Batch small updates** — combine multiple minor updates into one suggestion
3. **Don't repeat rejected suggestions** — unless circumstances clearly changed
4. **Keep CLAUDE.md under 200 lines** — when adding, consider what can be removed
5. **Show diff, not replacement** — user should see exactly what changes

## Responsibility Distribution

- **Kickoff Agent**: Initial generation + embeds self-update rules in CLAUDE.md
- **Any AI session**: Can detect signals and suggest updates during daily work
- **Retrospective Agent (v2)**: Periodic deep review and optimization suggestions
