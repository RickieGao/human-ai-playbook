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
8. Determine output strategy based on scale selection (see Output Strategy section)
9. Present to user for review before writing (including file structure preview for multi-file output)
10. For single-file: write all content to CLAUDE.md
11. For multi-file: extract designated fragments into `.claude/rules/` files, keep remaining content in CLAUDE.md

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

- Single-file output: total CLAUDE.md should be under 200 lines
- Multi-file output: CLAUDE.md should be under 120 lines; each rules file under 50 lines
- Fragments should be self-contained (no cross-references)
- Use clear, imperative language (instructions for AI)
- Do not include information AI can infer from code
- Output strategy is determined by scale selection (see Output Strategy section)
- For multi-file output, `base/quality-standards.md` content is distributed across `rules/quality.md` and `rules/commit.md` instead of being included in CLAUDE.md

## Placeholder Fallback

When a placeholder value cannot be detected (Path A) or inferred (Path B), apply these fallbacks:

| Placeholder | Fallback |
|-------------|----------|
| `{{project_name}}` | Use directory name |
| `{{project_description}}` | `TODO: Add project description` |
| `{{tech_stack}}` | Must be resolved — ask user if scan fails |
| `{{build_command}}` | Omit the Build section from Commands |
| `{{test_command}}` | Omit the Test section from Commands; add to Known Pitfalls: "No test command detected — set up testing and update this file" |
| `{{lint_command}}` | Omit the Lint section from Commands |
| `{{coding_conventions}}` | "Follow existing code style in the repository" |
| `{{workflow_description}}` | Must be resolved — always comes from interview |
| `{{autonomy_description}}` | Must be resolved — always comes from interview |
| `{{communication_style_description}}` | Must be resolved — always comes from interview |
| `{{review_process_description}}` | "Per feature" (default) |
| `{{safety_constraints}}` | Omit the Safety Constraints section |
| `{{known_pitfalls}}` | Omit the Known Pitfalls section |

### Fallback Principles

1. **Never output raw placeholders** — `{{test_command}}` must never appear in the final CLAUDE.md
2. **Omit over stub** — if a value is unknown and non-critical, remove the section rather than inserting a generic placeholder
3. **Mark for follow-up** — when omitting something important (like tests), add a note in Known Pitfalls so the user is reminded to set it up
4. **Must-resolve placeholders** — `tech_stack`, `workflow_description`, `autonomy_description`, and `communication_style_description` must always be resolved (ask the user if detection fails)

## Output Strategy

The Kickoff Agent produces different file structures based on project scale:

### Single-file (solo-developer scale)
- Output: `CLAUDE.md` only
- All content assembled into one file
- Target: under 200 lines

### Multi-file (small-team scale)
- Output: `CLAUDE.md` + `.claude/rules/` directory
- CLAUDE.md contains: Project Identity, Collaboration Mode, Context Management
- Rules files contain: quality standards, workflow specifics
- Each rules file should be self-contained and under 50 lines

### Multi-file with path scoping (monorepo scale)
- Output: `CLAUDE.md` + `.claude/rules/` directory with path-scoped rules
- CLAUDE.md contains: Project Identity, Collaboration Mode, Context Management
- Global rules (no path scope): quality standards, commit conventions
- Path-scoped rules: per-package/module conventions, testing requirements
- Path-scoped rules use YAML frontmatter:
  ```yaml
  ---
  paths:
    - "packages/api/**/*"
  ---
  ```

### Strategy Selection
- solo-developer → single-file
- small-team → multi-file
- monorepo → multi-file with path scoping
