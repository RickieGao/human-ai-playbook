## Context Management

### CLAUDE.md Maintenance
- Keep this file under 200 lines
- Update when conventions change or new pitfalls are discovered
- Only include information AI cannot infer from code

### Session Management
- Use `/compact` when context exceeds 50%
- For large tasks, split into multiple sessions with clear handoff
- End each session with a commit and progress summary

### Known Pitfalls
{{known_pitfalls}}
