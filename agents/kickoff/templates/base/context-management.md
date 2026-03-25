## Context Management

### CLAUDE.md Maintenance
- Keep this file under 200 lines
- Update when conventions change or new pitfalls are discovered
- Only include information AI cannot infer from code

### Session Management
- Use `/compact` when context exceeds 50%
- For large tasks, split into multiple sessions with clear handoff
- End each session with a commit and progress summary

### Project Documentation
- Project-specific process documents (test logs, TODOs, decision records, progress notes) should live in the repository, not in AI memory
- AI memory is reserved for cross-project user preferences only
- This keeps context clean when switching between projects

### Known Pitfalls
{{known_pitfalls}}

### Safety Constraints
{{safety_constraints}}

### Self-Update
- AI may suggest CLAUDE.md updates when it detects changes in tools, conventions, or recurring corrections
- Every suggested update will be shown as a diff with a reason — approve, reject, or modify
- Rejected suggestions will not be repeated
