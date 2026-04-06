# Environment Detection

The first action the Kickoff Agent takes. Determines whether the user has an existing project (Path A) or is starting from an idea (Path B).

## Detection Logic

Check the current working directory for project indicators:

### Project Indicators (any one is sufficient for Path A)
- Package manager files: `package.json`, `Cargo.toml`, `go.mod`, `pyproject.toml`, `pom.xml`, `build.gradle`, `Gemfile`, `composer.json`
- Build config: `Makefile`, `CMakeLists.txt`, `webpack.config.*`, `vite.config.*`
- Source directories: `src/`, `lib/`, `app/`
- Version control with history: `.git/` with commits

### Path Selection

```
Scan current directory
  ├── Project indicators found → Path A: Project Scanning
  │   Announce: "I see an existing project here. Let me scan it to understand your setup."
  │   Proceed to: project-scanner.md
  │
  └── No indicators (empty or non-project directory) → Path B: From Idea
      Announce: "Looks like we're starting fresh. Tell me about your idea —
                what do you want to build, or what problem do you want to solve?"
      Proceed to: needs-clarification.md
```

### Edge Cases
- **Has `.git/` but no code**: Treat as Path B (initialized repo but no project yet)
- **Has CLAUDE.md already**: Note this is an update, not first-time creation. Show existing content and ask what to change.
- **User explicitly says "I want to start a new project"**: Override to Path B regardless of directory contents
