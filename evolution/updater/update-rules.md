# Update Rules

## What Can Be Updated

- Methodology documents (`docs/`)
- Agent protocols (`agents/`)
- Templates (`agents/kickoff/templates/`)
- Search configuration (`evolution/collector/search-config.yaml`)

## What Cannot Be Updated (without explicit approval)

- Core principles (changes require maintainer discussion)
- Agent architecture (adding/removing agents)
- Project structure (directory layout)
- LICENSE

## Update Process

1. Updater drafts a proposal
2. Proposal is submitted as a GitHub issue or PR
3. Maintainer reviews and approves/rejects/modifies
4. If approved, changes are merged
5. CHANGELOG.md is updated

## Quality Checks

Before submitting an update proposal:
- [ ] Change is supported by evidence (linked in proposal)
- [ ] Affected files remain under 200 lines
- [ ] No contradictions introduced with other documents
- [ ] Tone and style match existing content
- [ ] Change is the minimum necessary (no scope creep)
