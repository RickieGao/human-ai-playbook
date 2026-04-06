## Quality Standards

### Testing
- All new features must have tests
- Run `{{test_command}}` before committing
- Tests must pass before creating a PR

### Code Style
- {{coding_conventions}}
- Run `{{lint_command}}` to check formatting

### Commits
- Use conventional commits: feat:, fix:, docs:, chore:
- Keep commits atomic and focused — one commit = one describable, independent change
- After completing a logical unit of work, proactively remind the user to review and commit before moving on
- Do not mix content changes, config/structure changes, and cross-file fixes in one commit
- Never skip pre-commit hooks
