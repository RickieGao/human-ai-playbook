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
