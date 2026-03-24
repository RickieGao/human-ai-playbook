# Interview Protocol

Detailed conversation flow for the Kickoff Agent's 3-round interview.

---

## General Rules

1. Ask one round at a time
2. Number your questions for easy reference
3. Provide defaults in parentheses: "Language? (default: TypeScript)"
4. Accept partial answers - fill gaps with sensible defaults
5. Summarize answers at the end of each round for confirmation

## Round 1: Project Basics

### Questions

```
1. What is your project name?
2. Describe your project in 1-2 sentences.
3. What is your tech stack?
   - Language(s):
   - Framework(s):
   - Database:
   - Other key tools:
4. What type of project is this?
   a) Greenfield (starting from scratch)
   b) Existing codebase (adding features / fixing bugs)
   c) Migration (moving between systems)
   d) Other: ___
5. What is the team size?
   a) Solo developer
   b) Small team (2-5)
   c) Large team (5+)
   d) Open source project
```

### After Round 1
Summarize: "Here's what I understand about your project: [summary]. Correct?"

## Round 2: Collaboration Preferences

### Questions

```
1. Which workflow fits best?
   a) TDD - Write tests first, then implement
   b) Plan-first - Detailed plan before any code
   c) Spec-driven - Formal specs/contracts first
   d) Incremental - Quick iterations, evolve as you go
2. How much AI autonomy do you want?
   a) Strict: Review every change before applying
   b) Moderate: AI executes plan, review at checkpoints
   c) High: AI works independently, review at PR level
3. Preferred communication style?
   a) Verbose: Detailed explanations and reasoning
   b) Concise: Key points only
   c) Minimal: Just the code/output
4. Any coding conventions?
   (naming, formatting, patterns, etc.)
5. How do you want to handle code review?
   a) Every change
   b) Per feature/task
   c) Per PR
```

## Round 3: Environment Configuration

### Questions

```
1. Build command(s): (e.g., npm run build)
2. Test command(s): (e.g., npm test)
3. Lint command(s): (e.g., npm run lint)
4. Any CI/CD to be aware of?
5. Security requirements or constraints?
6. Known pitfalls or gotchas in this codebase?
7. Any other tools or integrations?
```

## Assembly

After all 3 rounds, proceed to `decision-tree.md` to determine which
template fragments to include, then assemble per `templates/_assembly-rules.md`.
