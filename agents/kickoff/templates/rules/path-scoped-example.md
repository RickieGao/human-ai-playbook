---
description: Example of a path-scoped rule for monorepo packages
paths:
  - "packages/api/**/*"
---

# API Package Rules

- All endpoints must include input validation
- Use the shared error handler from `packages/shared/errors`
- API tests go in `packages/api/tests/`, not in a top-level test directory
