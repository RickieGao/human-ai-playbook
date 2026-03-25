# Template Assembly Rules

## How Templates Work

Each `.md` file in this directory is a **fragment** - a reusable section of a CLAUDE.md file. The Kickoff Agent selects and combines fragments based on the interview answers and the decision tree.

## Assembly Process

1. Start with all `base/` fragments (always included)
2. Add one `workflow/` fragment based on workflow choice
3. Add one `scale/` fragment based on team size
4. Add `domain/` fragment if applicable
5. Inject custom content from scenario question answers
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
| `{{coding_conventions}}` | Scan detection or Q4 context | "Use camelCase for variables, PascalCase for components" |
| `{{workflow_description}}` | Q1 mapping | "Plan-first: discuss before coding" |
| `{{autonomy_description}}` | Q2 mapping | "Moderate: suggest but don't act without approval" |
| `{{communication_style_description}}` | Q3 mapping | "Concise: key points only" |
| `{{review_process_description}}` | Q5 mapping (full mode) or default | "Per feature" |
| `{{safety_constraints}}` | Q7 (full mode) or empty | "Never delete production data" |

## Data Source by Path

| Content | Path A Source | Path B Source |
|---------|--------------|---------------|
| `{{project_name}}` | Scan detection | Requirements summary |
| `{{project_description}}` | Scan detection | Requirements summary |
| `{{tech_stack}}` | Scan detection | Tech recommendation |
| `{{build_command}}` | Scan detection | Tech recommendation (inferred) |
| `{{test_command}}` | Scan detection | Tech recommendation (inferred) |
| `{{lint_command}}` | Scan detection | Tech recommendation (inferred) |
| `{{coding_conventions}}` | Scan detection (eslint/prettier config) | Tech recommendation defaults |
| `{{known_pitfalls}}` | Q6 + scan supplement | Q6 |

## Rules

- Total assembled CLAUDE.md should be under 200 lines
- Fragments should be self-contained (no cross-references)
- Use clear, imperative language (instructions for AI)
- Do not include information AI can infer from code
