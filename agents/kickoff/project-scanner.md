# Project Scanner

Automatically extracts project information that would otherwise require user input.
Runs when Path A is selected (existing project detected).

## What to Scan

### 1. Tech Stack Detection

| Source File | Extract |
|-------------|---------|
| `package.json` | Language (JS/TS), framework (deps: react, vue, express, next...), package manager (lock file type) |
| `tsconfig.json` | TypeScript confirmation + config |
| `Cargo.toml` | Rust + dependencies |
| `go.mod` | Go + module name + dependencies |
| `pyproject.toml` / `requirements.txt` | Python + framework (django, flask, fastapi...) |
| `pom.xml` / `build.gradle` | Java/Kotlin + framework (Spring, etc.) |
| `Gemfile` | Ruby + framework (Rails, etc.) |
| `composer.json` | PHP + framework (Laravel, etc.) |

### 2. Command Detection

| Source | Extract |
|--------|---------|
| `package.json` scripts | build, test, lint, dev, start commands |
| `Makefile` | build, test, lint targets |
| `Cargo.toml` | `cargo build`, `cargo test` |
| `pyproject.toml` [tool.pytest] | test command |
| CI config files | build/test pipeline commands |

### 3. Code Convention Detection

| Source | Extract |
|--------|---------|
| `.eslintrc*` / `eslint.config.*` | Linting rules present |
| `.prettierrc*` | Formatting rules present |
| `.editorconfig` | Indentation, line ending conventions |
| `rustfmt.toml` | Rust formatting config |
| `pyproject.toml` [tool.black/ruff] | Python formatting config |

### 4. CI/CD Detection

| Source | Extract |
|--------|---------|
| `.github/workflows/*.yml` | GitHub Actions pipelines |
| `.gitlab-ci.yml` | GitLab CI |
| `Jenkinsfile` | Jenkins pipeline |
| `.circleci/config.yml` | CircleCI |

### 5. Team & History Detection

| Source | Extract |
|--------|---------|
| `git log --format='%an' \| sort -u` | Unique contributors |
| `git log --oneline -20` | Commit style (conventional commits?) |
| `git log --since='30 days ago' --oneline \| wc -l` | Activity level |

### 6. Existing CLAUDE.md Check

If `CLAUDE.md` exists, this is an update scenario. Read and present current content.

## Output Format

Present scan results as a confirmation prompt:

> "I scanned your project and detected:
> - **Tech stack**: [detected stack]
> - **Build**: `[command]`
> - **Test**: `[command]`
> - **Lint**: `[command]`
> - **Code style**: [detected tools]
> - **CI/CD**: [detected setup]
> - **Team**: [N contributors in last 30 days]
> - **Commit style**: [detected pattern]
>
> Is this correct? Anything to add or fix? For example: tools I missed, special conventions, or known gotchas?"

## After Confirmation

Proceed to: `interview-protocol.md` (scenario-based collaboration questions, Stage 2)
