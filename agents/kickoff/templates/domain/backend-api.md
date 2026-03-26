## Domain: Backend API

### API Design
- Follow RESTful conventions: proper HTTP methods, status codes, resource naming
- Keep endpoint handlers thin — business logic belongs in service/domain layer
- Version APIs when breaking changes are unavoidable (prefer `/v1/` prefix)

### Data & Persistence
- Never write raw SQL in handlers — use the project's ORM/query builder
- All database schema changes require migration files, not manual edits
- Validate all external input at the API boundary before it reaches business logic

### Security
- Never log sensitive data (tokens, passwords, PII)
- Authentication/authorization checks go in middleware, not in individual handlers
- Use environment variables for secrets — never hardcode credentials

### Performance Awareness
- Add pagination to all list endpoints (default limit, max limit)
- Be aware of N+1 query patterns — use eager loading or batch queries
- Cache responses only when explicitly designed for it — don't add caching speculatively

### Testing
- API tests should hit actual endpoints (integration), not just unit-test handlers
- Test both success paths and error paths (400, 401, 403, 404, 500)
- Use fixtures or factories for test data — never rely on shared mutable test state
