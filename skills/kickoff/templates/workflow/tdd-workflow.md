## Workflow: Test-Driven Development

1. **Write test first**: Define what "correct" means before implementing
2. **Confirm test fails**: Run `{{test_command}}` to verify the test fails
3. **Implement**: Write the minimum code to pass the test
4. **Confirm test passes**: Run tests again
5. **Refactor**: Clean up while keeping tests green
6. **Commit**: One commit per test-implement cycle

### Rules
- Never write implementation before the test
- Never delete or weaken a test to make it pass
- If a test is wrong, discuss with the human before changing it
