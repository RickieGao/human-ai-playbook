# Kickoff Agent Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign the Kickoff Agent from a CLAUDE.md generator into a project startup guide that adapts to users with existing projects (path A) or just an idea (path B), using auto-detection, scenario-based questions, and staged review.

**Architecture:** The agent flow splits at environment detection: Path A (existing project) scans files and extracts config automatically; Path B (from idea) guides through needs clarification, market research, and tech recommendation before converging. Both paths merge into scenario-based collaboration preference questions, CLAUDE.md generation, staged review, and optional scaffold init. A self-update mechanism enables ongoing CLAUDE.md maintenance.

**Tech Stack:** Markdown protocol files (no runtime code). The agent is a set of structured prompts that guide AI behavior.

**Spec:** `docs/superpowers/specs/2026-03-25-kickoff-agent-redesign.md`

---

## File Structure

### Files to Modify

| File | Change |
|------|--------|
| `agents/kickoff/SKILL.md` | Rewrite: new positioning, dual-path flow, updated overview |
| `agents/kickoff/interview-protocol.md` | Rewrite: replace 3-round Q&A with scenario-based questions |
| `agents/kickoff/decision-tree.md` | Update: new mapping from scenario answers to template selections |
| `agents/kickoff/templates/_assembly-rules.md` | Update: dual data source table (path A vs B), new placeholders |
| `agents/kickoff/templates/base/context-management.md` | Update: add self-update mechanism rules |

### Files to Create

| File | Purpose |
|------|---------|
| `agents/kickoff/environment-detection.md` | Protocol for detecting path A vs B |
| `agents/kickoff/project-scanner.md` | Path A: auto-detection of tech stack, commands, conventions |
| `agents/kickoff/needs-clarification.md` | Path B Step 1: brainstorm-style needs clarification |
| `agents/kickoff/market-research.md` | Path B Step 2: existing solution research protocol |
| `agents/kickoff/tech-recommendation.md` | Path B Step 3: technology recommendation protocol |
| `agents/kickoff/staged-review.md` | Stage 4: section-by-section review with education |
| `agents/kickoff/self-update.md` | Self-update mechanism: triggers, flow, constraints |

### Files Unchanged

- All template fragments (`templates/base/`, `templates/workflow/`, `templates/scale/`) — content unchanged
- Example files (`examples/`) — still valid as output examples
- `templates/domain/_placeholder.md` — still future scope

---

## Task 1: Environment Detection Protocol

**Files:**
- Create: `agents/kickoff/environment-detection.md`

This is the entry point that determines which path the user follows.

- [ ] **Step 1: Write environment detection protocol**

Create `agents/kickoff/environment-detection.md` with:

```markdown
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
```

- [ ] **Step 2: Verify protocol completeness**

Read the file back. Confirm it covers: detection logic, both path transitions, edge cases, and announcement text for each path.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/environment-detection.md
git commit -m "feat(kickoff): add environment detection protocol for path A/B routing"
```

---

## Task 2: Project Scanner (Path A)

**Files:**
- Create: `agents/kickoff/project-scanner.md`

- [ ] **Step 1: Write project scanner protocol**

Create `agents/kickoff/project-scanner.md` with:

```markdown
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
| `git log --format='%an' | sort -u` | Unique contributors |
| `git log --oneline -20` | Commit style (conventional commits?) |
| `git log --since='30 days ago' --oneline | wc -l` | Activity level |

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
```

- [ ] **Step 2: Verify protocol completeness**

Read the file back. Confirm all detection categories from the spec are covered: tech stack, commands, conventions, CI/CD, team info, existing CLAUDE.md.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/project-scanner.md
git commit -m "feat(kickoff): add project scanner protocol for automatic detection"
```

---

## Task 3: Needs Clarification (Path B, Step 1)

**Files:**
- Create: `agents/kickoff/needs-clarification.md`

- [ ] **Step 1: Write needs clarification protocol**

Create `agents/kickoff/needs-clarification.md` with:

```markdown
# Needs Clarification (Brainstorm Mode)

The most important stage in the entire flow. Transforms a vague idea into a clear
requirements summary. No fixed question count — conversation quality determines when
this stage is complete.

## Entry

User has described an initial idea after Path B was selected.

## AI Role: Guide, Not Recorder

### Behaviors

1. **Probe the essence**
   - User says "I want to build X" → Ask "Why do you need X? How do you solve this problem today?"
   - Dig into the pain point, not the solution

2. **Challenge assumptions**
   - "You mentioned needing multi-user collaboration, but would a single-user version solve the core problem first?"
   - Help distinguish wants from needs

3. **Narrow scope**
   - When user adds features, ask: "Is this essential for the first version, or something to add later?"
   - Aggressively protect MVP boundary

4. **Make it concrete**
   - "Can you walk me through a typical use case? From opening the app to finishing the task, what are the steps?"
   - Ground abstract ideas in specific scenarios

5. **Summarize and confirm**
   - When sufficient depth is reached, output a requirements summary for confirmation

## Requirements Summary Template

When all four elements are clear, present:

> **Requirements Summary**
>
> **Core problem**: [One sentence — what pain point are we solving?]
>
> **Target user**: [Who uses this, in what context?]
>
> **MVP scope**:
> - [Must-have 1]
> - [Must-have 2]
> - [Must-have 3]
>
> **Explicitly out of scope (for now)**:
> - [Not doing 1]
> - [Not doing 2]
>
> **Success criteria**: [How do we know it works?]
>
> Does this capture what you want to build?

## Exit Condition

All four elements (core problem, target user, MVP scope, success criteria) are clear
AND user confirms the summary.

## After Confirmation

Proceed to: `market-research.md` (Step 2)

## Example Conversation

User: I want to make a bookkeeping tool

AI: There are many kinds of bookkeeping tools. How do you track expenses now?
What's frustrating about your current approach?

User: I use Excel, it's too tedious, I always forget

AI: So the core pain point is "recording is too cumbersome to stick with."
What would ideal bookkeeping look like for you? For example: finish
recording within 10 seconds of each purchase? Or spend 5 minutes
reviewing at night?

User: Ideally automatic, no manual entry

AI: Automatic bookkeeping usually means connecting to bank/payment APIs,
which is complex technically and compliance-wise. Some more practical
approaches: a) photo receipt recognition b) WeChat/Alipay statement
import c) voice quick-entry. Which direction feels most realistic?

[...conversation continues until requirements are clear...]
```

- [ ] **Step 2: Verify protocol completeness**

Read the file back. Confirm it covers: all 5 AI behaviors from spec, requirements summary template with all 4 elements, exit condition, example conversation.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/needs-clarification.md
git commit -m "feat(kickoff): add brainstorm-style needs clarification protocol"
```

---

## Task 4: Market Research (Path B, Step 2)

**Files:**
- Create: `agents/kickoff/market-research.md`

- [ ] **Step 1: Write market research protocol**

Create `agents/kickoff/market-research.md` with:

```markdown
# Market Research

After requirements are clarified, search for existing solutions before building new.
Helps users avoid reinventing the wheel.

## Entry

Requirements summary has been confirmed by the user.

## Process

### 1. Search for Existing Solutions

Based on the requirements summary, search for:
- Established products/apps that solve the same problem
- Open-source projects with similar goals
- Tools or services that partially address the need

Use web search and your knowledge to find relevant options.

### 2. Structured Comparison

Present findings in a comparison table:

> Based on your core need "[core problem from summary]", here are existing solutions:
>
> | Solution | Match | Strengths | What's Missing |
> |----------|-------|-----------|----------------|
> | [Product A] | High/Med/Low | [key strengths] | [gaps vs requirements] |
> | [Product B] | High/Med/Low | [key strengths] | [gaps vs requirements] |
> | [Product C] | High/Med/Low | [key strengths] | [gaps vs requirements] |
>
> [Product A] covers most of your needs. Have you tried it? If so, what didn't work?

### 3. Guide Decision

Three possible outcomes:

**Outcome A — Existing solution satisfies needs**
> "[Product] already solves your problem well. I'd recommend using it directly."
> → Flow ends. Kickoff Agent has saved the user from unnecessary work.

**Outcome B — Partial match, consider extending**
> "[Open-source project] has a solid foundation. You could add [missing feature]
> on top of it rather than starting from scratch."
> → Proceed to tech-recommendation.md with "extend existing" context.

**Outcome C — No adequate solution exists**
> "Your specific need for [unique requirement] isn't well served by existing tools.
> It's worth building something new."
> → Proceed to tech-recommendation.md with "build new" context.

## Key Principle

Be honest. Recommend the best solution even if it means "don't build anything."
This builds trust — the Kickoff Agent helps users do the right thing, not just
write code.

## After Decision

- Outcome A: Flow ends with recommendation
- Outcome B/C: Proceed to `tech-recommendation.md` (Step 3)
```

- [ ] **Step 2: Verify protocol completeness**

Read the file back. Confirm it covers: search process, comparison table format, all three outcomes from spec, honest recommendation principle.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/market-research.md
git commit -m "feat(kickoff): add market research protocol for existing solution evaluation"
```

---

## Task 5: Tech Recommendation (Path B, Step 3)

**Files:**
- Create: `agents/kickoff/tech-recommendation.md`

- [ ] **Step 1: Write tech recommendation protocol**

Create `agents/kickoff/tech-recommendation.md` with:

```markdown
# Tech Recommendation

Recommends a technology stack based on the user's requirements and technical background.
Only reached when market research confirms building is worthwhile.

## Entry

Market research completed with Outcome B (extend) or Outcome C (build new).

## Process

### 1. Assess User's Technical Level

Do not ask "what languages do you know?" directly. Instead:

> "Have you built anything similar before? Or what programming languages/tools
> do you work with day-to-day? No experience at all is totally fine."

Classify into:
- **Zero experience**: No programming background
- **Some experience**: Has coded but not in this domain
- **Experienced**: Comfortable with relevant technologies

### 2. Recommend Stack

**For zero-experience users:**
- Recommend ONE option only — avoid choice paralysis
- Prioritize: large community, abundant tutorials, strong AI coding assistance support
- Explain why in plain language

> "Since you're new to programming, I recommend:
> **Next.js + Supabase** — this combines frontend and backend in one framework,
> Supabase provides a ready-made database and auth system, and deployment is simple.
> The main advantage: there are tons of tutorials, and AI tools work very well
> with this stack.
>
> Sound good?"

**For users with some experience:**
- Recommend 1-2 options with brief comparison
- Leverage their existing knowledge

**For experienced users:**
- Present 2 options with trade-offs
- Respect their ability to evaluate

### 3. Confirm and Output Tech Summary

After user agrees on stack:

> **Tech Summary**
> - **Stack**: [selected technologies and why]
> - **Project structure**: [recommended directory layout]
> - **Dev tools**: [editor, package manager, etc.]
> - **Context**: [extending existing project / building new]

## Key Principles

- For zero-experience users, prioritize "AI can assist well with this stack"
- Don't pile on options — avoid choice anxiety
- Match the stack to MVP scope, don't over-engineer for future needs

## After Confirmation

Proceed to: `interview-protocol.md` (scenario-based collaboration questions, Stage 2)
```

- [ ] **Step 2: Verify protocol completeness**

Read the file back. Confirm it covers: natural technical level assessment, tiered recommendations by experience level, tech summary output, key principles from spec.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/tech-recommendation.md
git commit -m "feat(kickoff): add tech recommendation protocol with user-level adaptation"
```

---

## Task 6: Rewrite Interview Protocol (Stage 2 — Scenario-Based Questions)

**Files:**
- Modify: `agents/kickoff/interview-protocol.md` (full rewrite)

- [ ] **Step 1: Rewrite interview-protocol.md**

Replace the entire content of `agents/kickoff/interview-protocol.md` with:

```markdown
# Scenario-Based Collaboration Questions

Replaces the original 3-round abstract interview with concrete scenario questions.
Users answer based on intuition, not abstract concepts.

## Entry

- Path A: After project scan confirmation
- Path B: After tech recommendation confirmation

## Mode Selection

Present the choice (except Path B zero-experience users who default to full mode):

> "Now I'd like to understand how you want to collaborate with AI. Two options:
> - **Quick mode** (3 questions, ~2 minutes) — covers core preferences
> - **Full mode** (7 questions, ~5 minutes) — more detailed customization
>
> Which one?"

---

## Quick Mode (3 Core Questions)

### Q1 — Work Rhythm

> "You ask AI to implement a user login feature. How should AI work?
> a) Write a plan first, wait for your approval before coding
> b) Start coding, but show you after each small step
> c) Complete the whole feature, you review the final result"

**Maps to:**
- a → workflow: plan-first, autonomy: strict
- b → workflow: incremental, autonomy: moderate
- c → workflow: incremental, autonomy: high

### Q2 — Handling the Unexpected

> "While implementing your feature, AI notices an existing function is poorly written
> and fixing it would make things cleaner. What should AI do?
> a) Only do what you asked, don't touch anything else
> b) Tell you about the issue and ask if you want it fixed too
> c) Fix it along the way and tell you what changed"

**Maps to:**
- a → autonomy: strict, scope: requested-only
- b → autonomy: moderate, scope: suggest-expansion
- c → autonomy: high, scope: proactive-improvement

### Q3 — Communication Style

> "After AI completes a task, how should it report?
> a) Detailed explanation: what was done, why, and what alternatives existed
> b) Brief summary: what changed and key decisions
> c) Just the code diff, no explanation needed"

**Maps to:**
- a → communication: verbose
- b → communication: concise
- c → communication: minimal

---

## Full Mode (Additional 4 Questions)

### Q4 — Testing Attitude

> "About testing, what's your expectation?
> a) Every feature must have corresponding tests
> b) Core logic needs tests, edge cases are case-by-case
> c) Get the feature working first, add tests later"

**Maps to:**
- a → testing: strict (TDD encouraged)
- b → testing: moderate
- c → testing: minimal

### Q5 — Review Frequency

> "How often do you want to check AI's work?
> a) I want to see every file change
> b) After each complete feature
> c) I trust AI, I'll review at PR level"

**Maps to:**
- a → review: every-change
- b → review: per-feature
- c → review: per-pr

### Q6 — Known Pitfalls

> "Are there any 'gotchas' in this project that AI might trip over?
> For example: an API with hidden rate limits, a directory that shouldn't be touched,
> a dependency with known bugs? (Skip if none)"

**Maps to:** Direct insertion into known-pitfalls section of CLAUDE.md

### Q7 — Safety Red Lines

> "Is there anything AI must absolutely never do?
> For example: delete databases, access production, modify certain config files?
> (Skip if none)"

**Maps to:** Direct insertion into safety constraints section of CLAUDE.md

---

## After All Questions

Summarize collaboration preferences:

> "Here's your collaboration style:
> - [Work rhythm summary]
> - [Scope handling summary]
> - [Communication summary]
> - [Testing summary, if full mode]
> - [Review frequency, if full mode]
>
> Does this look right?"

After confirmation, proceed to CLAUDE.md generation (Stage 3) using the
decision tree (`decision-tree.md`) and assembly rules (`templates/_assembly-rules.md`).

Then proceed to: `staged-review.md` (Stage 4)
```

- [ ] **Step 2: Verify rewrite**

Read the file back. Confirm: mode selection, all 7 questions with scenario format, mapping annotations, summary template, flow transitions.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/interview-protocol.md
git commit -m "feat(kickoff): replace abstract interview with scenario-based questions"
```

---

## Task 7: Update Decision Tree

**Files:**
- Modify: `agents/kickoff/decision-tree.md`

- [ ] **Step 1: Update decision-tree.md**

The decision tree needs to map from the new scenario question answers instead of the old abstract questions. Update the file to:

1. Change "Q: Which workflow?" section to reference Q1 answer mappings (a/b/c → workflow selection)
2. Keep scale selection but note that for Path A it comes from scan detection, for Path B from tech recommendation
3. Update autonomy adjustments to reference Q2 answer mappings
4. Keep output assembly order unchanged
5. Add a note about data source differences between Path A and Path B

Key changes:
- Workflow selection: Q1-a → plan-first, Q1-b → incremental, Q1-c → incremental
- Scale selection: Path A from git contributor count, Path B from user context
- Autonomy: Derived from Q1 + Q2 combination
- Add note: "If Q1-a AND Q4-a (full mode), consider TDD workflow instead of plan-first"

- [ ] **Step 2: Verify update**

Read the file back. Confirm all mappings from new scenario questions are present and consistent with interview-protocol.md.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/decision-tree.md
git commit -m "feat(kickoff): update decision tree for scenario-based question mappings"
```

---

## Task 8: Update Assembly Rules

**Files:**
- Modify: `agents/kickoff/templates/_assembly-rules.md`

- [ ] **Step 1: Update _assembly-rules.md**

Add the dual data source table and new placeholders:

1. Add a "Data Source by Path" table:

| Content | Path A Source | Path B Source |
|---------|--------------|---------------|
| `{{project_name}}` | Scan detection | Requirements summary |
| `{{project_description}}` | Scan detection | Requirements summary |
| `{{tech_stack}}` | Scan detection | Tech recommendation |
| `{{build_command}}` | Scan detection | Tech recommendation (inferred) |
| `{{test_command}}` | Scan detection | Tech recommendation (inferred) |
| `{{lint_command}}` | Scan detection | Tech recommendation (inferred) |
| `{{known_pitfalls}}` | Q6 + scan supplement | Q6 |

2. Add new placeholders:

| Placeholder | Source |
|-------------|--------|
| `{{workflow_description}}` | Q1 mapping |
| `{{autonomy_description}}` | Q2 mapping |
| `{{communication_style_description}}` | Q3 mapping |
| `{{review_process_description}}` | Q5 mapping (full mode) or default |
| `{{safety_constraints}}` | Q7 (full mode) or empty |

3. Update assembly step 5: "Inject custom content from scenario question answers" (was "Round 3 answers")

- [ ] **Step 2: Verify update**

Read the file back. Confirm dual source table is present and all new placeholders are documented.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/templates/_assembly-rules.md
git commit -m "feat(kickoff): update assembly rules with dual data sources and new placeholders"
```

---

## Task 9: Staged Review Protocol

**Files:**
- Create: `agents/kickoff/staged-review.md`

- [ ] **Step 1: Write staged review protocol**

Create `agents/kickoff/staged-review.md` with:

```markdown
# Staged Review

Section-by-section review of the generated CLAUDE.md. Builds user understanding
and ownership by explaining each section's purpose before asking for confirmation.

## Entry

CLAUDE.md draft has been generated (Stage 3 complete).

## Process

Present CLAUDE.md in 4-5 sections. For each section:
1. Show the content
2. Explain its purpose in one sentence
3. For Path B users: add a concrete example of how this affects collaboration
4. Wait for user to confirm, modify, or add content
5. Only proceed to next section after confirmation

## Sections

### Section 1: Project Identity

Show: Project name, description, tech stack, common commands.

> **What this does**: AI reads this first every session to understand what your project
> is and how to run it.

Path B extra: "For example, if you later add a database, you'd update the tech stack
and add migration commands here."

### Section 2: Collaboration Mode

Show: Workflow, scope handling, communication style, review process.

> **What this does**: This is your 'working contract' with AI. It will strictly follow
> these rules. For instance, it won't refactor code without your permission.

### Section 3: Quality Standards

Show: Testing requirements, commit conventions, code style.

> **What this does**: Ensures AI produces consistent quality. Without this, AI might
> write tests sometimes and skip them other times.

### Section 4: Guardrails and Pitfalls

Show: Known pitfalls, safety constraints, prohibited actions.

> **What this does**: This is the 'safety fence' — the most important section, because
> this contains knowledge AI cannot infer from your code.

Path B extra: "This section might be thin right now. As your project grows, you'll
discover more gotchas — come back and add them."

### Section 5: Context Management (if applicable)

Show: CLAUDE.md maintenance rules, session management, self-update mechanism.

> **What this does**: Keeps your CLAUDE.md alive and accurate as the project evolves.

## After All Sections Confirmed

Write CLAUDE.md to project root directory.

> "CLAUDE.md has been written to your project root. This is a living document —
> update it anytime as your project evolves. AI will also suggest updates when
> it notices things have changed."

Then offer optional scaffold:

> "Would you like me to initialize the project? (Create directory structure,
> install dependencies, set up toolchain)"

- If yes: proceed with scaffolding based on tech summary
- If no: flow ends
```

- [ ] **Step 2: Verify protocol completeness**

Read the file back. Confirm: all 5 sections from spec, purpose explanations, Path B extras, post-review actions, scaffold offer.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/staged-review.md
git commit -m "feat(kickoff): add staged review protocol with education and ownership"
```

---

## Task 10: Self-Update Mechanism

**Files:**
- Create: `agents/kickoff/self-update.md`
- Modify: `agents/kickoff/templates/base/context-management.md`

- [ ] **Step 1: Write self-update protocol**

Create `agents/kickoff/self-update.md` with:

```markdown
# CLAUDE.md Self-Update Mechanism

AI can detect when CLAUDE.md needs updating and suggest changes,
but every update requires user review and approval.

## Trigger Signals

| Signal | Suggested Update |
|--------|-----------------|
| New dependency/tool added | Add to tech stack and related commands |
| User corrects same AI behavior 3+ times | Codify the correction as a rule |
| New pitfall discovered during work | Add to known pitfalls |
| User changes collaboration preference | Update collaboration mode |
| Major project structure change | Update project identity and scale config |
| Commands in CLAUDE.md no longer work | Fix commands |

## Update Flow

```
AI detects update signal
  → Wait for natural pause (task completion or break)
    → Present: current content vs suggested change + reason
      → User approves → Write change
      → User rejects → Do not change, remember user's judgment
      → User modifies → Write user's version
```

## Presentation Format

Use diff format for clarity:

> "I noticed you've told me three times not to add comments automatically.
> Suggest adding a rule to CLAUDE.md:
>
> ```diff
> ## Collaboration Mode
> + - Do not add explanatory comments in code unless explicitly asked
> ```
>
> Add this?"

## Behavioral Constraints

1. **Don't interrupt current work** — suggest at task completion or natural pauses
2. **Batch small updates** — combine multiple minor updates into one suggestion
3. **Don't repeat rejected suggestions** — unless circumstances clearly changed
4. **Keep CLAUDE.md under 200 lines** — when adding, consider what can be removed
5. **Show diff, not replacement** — user should see exactly what changes

## Responsibility Distribution

- **Kickoff Agent**: Initial generation + embeds self-update rules in CLAUDE.md
- **Any AI session**: Can detect signals and suggest updates during daily work
- **Retrospective Agent (v2)**: Periodic deep review and optimization suggestions
```

- [ ] **Step 2: Update context-management.md template**

Add self-update rules to `agents/kickoff/templates/base/context-management.md`. After the existing "Known Pitfalls" section, add:

```markdown
### Self-Update
- AI may suggest CLAUDE.md updates when it detects changes in tools, conventions, or recurring corrections
- Every suggested update will be shown as a diff with a reason — approve, reject, or modify
- Rejected suggestions will not be repeated
```

- [ ] **Step 3: Verify both files**

Read both files back. Confirm self-update.md covers all trigger signals, flow, constraints from spec. Confirm context-management.md has the new section without breaking existing content.

- [ ] **Step 4: Commit**

```bash
git add agents/kickoff/self-update.md agents/kickoff/templates/base/context-management.md
git commit -m "feat(kickoff): add CLAUDE.md self-update mechanism"
```

---

## Task 11: Rewrite SKILL.md (Agent Entry Point)

**Files:**
- Modify: `agents/kickoff/SKILL.md` (full rewrite)

- [ ] **Step 1: Rewrite SKILL.md**

Replace the entire content of `agents/kickoff/SKILL.md` with:

```markdown
# Kickoff Agent - Your First Step from Idea to Project

> The first AI you talk to when you have a creative idea. Guides you from a vague
> notion to a clear plan, or helps configure an existing project for AI collaboration.

## What It Does

The Kickoff Agent is the entry point for starting any project with AI. It adapts
to your situation:

- **Have an existing project?** → Scans your codebase, detects your setup, asks a
  few scenario questions about collaboration style, generates a customized CLAUDE.md
- **Just have an idea?** → Helps you clarify requirements, researches existing solutions,
  recommends technology, then sets up your CLAUDE.md

The goal is not just to generate a config file — it's to help you make the right
decision about what to build (or not build) and how to work with AI effectively.

## Flow

```
Detect Environment
  ├── Existing project → Scan & confirm → Collaboration questions → CLAUDE.md
  └── New idea → Clarify needs → Research market → Tech recommendation
                                                          ↓
                                         Collaboration questions → CLAUDE.md
                                                          ↓
                                              Staged review (section by section)
                                                          ↓
                                              Optional: scaffold project
```

## Protocols

| Protocol | File | Purpose |
|----------|------|---------|
| Environment Detection | `environment-detection.md` | Determine Path A or B |
| Project Scanner | `project-scanner.md` | Path A: auto-detect project config |
| Needs Clarification | `needs-clarification.md` | Path B: brainstorm requirements |
| Market Research | `market-research.md` | Path B: evaluate existing solutions |
| Tech Recommendation | `tech-recommendation.md` | Path B: recommend tech stack |
| Scenario Questions | `interview-protocol.md` | Both paths: collaboration preferences |
| Decision Tree | `decision-tree.md` | Map answers to template selections |
| Staged Review | `staged-review.md` | Section-by-section review with education |
| Self-Update | `self-update.md` | Ongoing CLAUDE.md maintenance |
| Assembly Rules | `templates/_assembly-rules.md` | How template fragments combine |

## Design Principles

- **Auto-detect what you can** — don't ask users for information that's in their code
- **Scenario over abstraction** — use concrete situations, not abstract concepts
- **Honest guidance** — recommend existing solutions when they fit; building isn't always the answer
- **Ownership through understanding** — explain why each part matters, review section by section
- **Living document** — CLAUDE.md evolves with the project via self-update mechanism
- Follow the Meta Agent communication principles at all times
```

- [ ] **Step 2: Verify rewrite**

Read the file back. Confirm: new positioning, dual-path flow diagram, complete protocol table with all files, updated design principles.

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/SKILL.md
git commit -m "feat(kickoff): rewrite SKILL.md with new positioning and dual-path flow"
```

---

## Task 12: End-to-End Walkthrough Verification

**Files:**
- Read: All files created/modified in Tasks 1-11

- [ ] **Step 1: Verify Path A flow continuity**

Read files in Path A order and verify each file's "After" / "Proceed to" references correctly:
1. `environment-detection.md` → (project found) → `project-scanner.md`
2. `project-scanner.md` → `interview-protocol.md`
3. `interview-protocol.md` → `decision-tree.md` + `templates/_assembly-rules.md` → generation
4. After generation → `staged-review.md`
5. `staged-review.md` → write file, optional scaffold

- [ ] **Step 2: Verify Path B flow continuity**

Read files in Path B order and verify references:
1. `environment-detection.md` → (empty dir) → `needs-clarification.md`
2. `needs-clarification.md` → `market-research.md`
3. `market-research.md` → (outcome A: end) or → `tech-recommendation.md`
4. `tech-recommendation.md` → `interview-protocol.md`
5. Same as Path A from step 3 onward

- [ ] **Step 3: Verify no broken references in SKILL.md protocol table**

Every file listed in `SKILL.md` protocol table exists and matches actual filenames.

- [ ] **Step 4: Verify decision tree consistency**

Mappings in `decision-tree.md` match the Q1-Q7 mappings in `interview-protocol.md`.

- [ ] **Step 5: Verify assembly rules consistency**

All placeholders in `_assembly-rules.md` are used in at least one template fragment, and all template fragments use only documented placeholders.

- [ ] **Step 6: Fix any issues found**

If any broken references, missing transitions, or inconsistencies are found, fix them.

- [ ] **Step 7: Final commit (if fixes needed)**

```bash
git add -A agents/kickoff/
git commit -m "fix(kickoff): resolve cross-reference issues from end-to-end review"
```
