# Template Assembly Rules

## How Templates Work

Each `.md` file in this directory is a **fragment** - a reusable section of a CLAUDE.md file. The Kickoff Agent selects and combines fragments based on the interview answers and the decision tree.

## Assembly Process

1. Start with all `base/` fragments (always included)
2. Add one `workflow/` fragment based on workflow choice
3. Add one `scale/` fragment based on team size
4. Add `domain/` fragment if applicable
5. Inject custom content from Round 3 answers
6. Concatenate in the order defined in `decision-tree.md`
7. Remove duplicate or contradictory instructions
8. Present to user for review before writing

## Fragment Format

Each fragment uses this structure:

```markdown
## [Section Title]

[Content with placeholders like {{project_name}}, {{test_command}}, etc.]
```

## Placeholder Reference

| Placeholder | Source | Example |
|-------------|--------|---------|
| `{{project_name}}` | Round 1, Q1 | "my-app" |
| `{{project_description}}` | Round 1, Q2 | "A REST API for..." |
| `{{tech_stack}}` | Round 1, Q3 | "TypeScript, Express, PostgreSQL" |
| `{{build_command}}` | Round 3, Q1 | "npm run build" |
| `{{test_command}}` | Round 3, Q2 | "npm test" |
| `{{lint_command}}` | Round 3, Q3 | "npm run lint" |

## Rules

- Total assembled CLAUDE.md should be under 200 lines
- Fragments should be self-contained (no cross-references)
- Use clear, imperative language (instructions for AI)
- Do not include information AI can infer from code
