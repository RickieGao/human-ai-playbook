# Project Scanner

Automatically extracts project information that would otherwise require user input.
Runs when Path A is selected (existing project detected).

## What to Scan

### 1. Project Type Classification

Before detailed scanning, classify the project type based on what's present:

| Indicators | Project Type | Implications |
|------------|-------------|--------------|
| Package manager + `src/`/`lib/`/`app/` | **Application** | Full tech stack, build/test/lint commands expected |
| Mostly `.md` files, no package manager | **Documentation** | Writing style matters, no build tools |
| `.md` files + CI workflows + scripts/automation dirs | **Docs + Automation** | Writing style + pipeline code standards needed |
| Mixed code and docs | **Hybrid** | Treat code and docs sections separately |

This classification affects which Quality Standards sections are relevant in the generated CLAUDE.md.

### 2. Tech Stack Detection

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
| `.github/workflows/*.yml` | GitHub Actions (check for API calls, scripts, tool invocations) |
| `scripts/`, `evolution/`, automation dirs | Scripting languages, automation tooling |

### 3. Command Detection

| Source | Extract |
|--------|---------|
| `package.json` scripts | build, test, lint, dev, start commands |
| `Makefile` | build, test, lint targets |
| `Cargo.toml` | `cargo build`, `cargo test` |
| `pyproject.toml` [tool.pytest] | test command |
| CI config files | build/test pipeline commands |

### 4. Code Convention Detection

| Source | Extract |
|--------|---------|
| `.eslintrc*` / `eslint.config.*` | Linting rules present |
| `.prettierrc*` | Formatting rules present |
| `.editorconfig` | Indentation, line ending conventions |
| `rustfmt.toml` | Rust formatting config |
| `pyproject.toml` [tool.black/ruff] | Python formatting config |

### 5. CI/CD Detection

| Source | Extract |
|--------|---------|
| `.github/workflows/*.yml` | GitHub Actions pipelines |
| `.gitlab-ci.yml` | GitLab CI |
| `Jenkinsfile` | Jenkins pipeline |
| `.circleci/config.yml` | CircleCI |

### 6. Team & History Detection

| Source | Extract |
|--------|---------|
| `git log --format='%an' \| sort -u` | Unique contributors |
| `git log --oneline -20` | Commit style (conventional commits?) |
| `git log --since='30 days ago' --oneline \| wc -l` | Activity level |

### 7. Existing CLAUDE.md Check

If `CLAUDE.md` exists, this is an update scenario. Read and present current content.

## Output Format

Present scan results as a confirmation prompt:

> "I scanned your project and detected:
> - **Project type**: [Application / Documentation / Docs + Automation / Hybrid]
> - **Tech stack**: [detected stack — include automation tooling if applicable]
> - **Build**: `[command]` (or "N/A — docs/automation project")
> - **Test**: `[command]` (or "N/A")
> - **Lint**: `[command]` (or "N/A")
> - **Code style**: [detected tools]
> - **CI/CD**: [detected setup]
> - **Team**: [N contributors in last 30 days]
> - **Commit style**: [detected pattern]
>
> Is this correct? Anything to add or fix? For example: tools I missed, special conventions, or known gotchas?"

## After Confirmation

Proceed to: `interview-protocol.md` (scenario-based collaboration questions, Stage 2)
