# CLAUDE.md - human-ai-playbook

## Project Identity

This is a bilingual (Chinese/English) open-source project providing human-AI collaboration methodology and executable agent systems. The primary language for docs is Chinese; code and agent protocols use English.

## Repository Structure

- `docs/` - Methodology documentation (zh/ and en/)
- `agents/` - Agent system (meta/, kickoff/, async-comm/, retrospective/, persona-transfer/)
- `evolution/` - Self-evolution mechanism (collector/, analyzer/, updater/)
- `research/` - Research materials and competitive analysis
- `.github/workflows/` - CI/CD automation

## Collaboration Standards

### Writing Style
- Methodology docs: Clear, concise, actionable. Use tables for structured comparisons.
- Agent protocols: Structured markdown with clear sections. Machine-readable where possible.
- Bilingual: Chinese is primary. English translations should be natural, not literal.

### Commit Convention
- Use conventional commits: `feat:`, `fix:`, `docs:`, `chore:`
- Keep commits atomic and focused

### Key Decisions
- License: CC-BY-SA-4.0
- Meta Agent defines communication principles that all other agents must follow
- Kickoff Agent is the MVP priority - it generates CLAUDE.md for other projects
- Self-evolution uses a 4-step pipeline: collect -> analyze -> suggest updates -> human review

### What NOT to do
- Do not over-engineer agent protocols - start simple, iterate based on real usage
- Do not add features beyond the current phase scope
