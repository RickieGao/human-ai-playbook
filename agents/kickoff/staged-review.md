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

Show: Testing requirements, commit conventions (including granularity and timing guidance), code style.

> **What this does**: Ensures AI produces consistent quality. Without this, AI might
> write tests sometimes and skip them other times.

**Review checkpoint**: Verify the Commits subsection includes:
- Atomic commit principle (one commit = one independent change)
- Proactive commit reminders (AI reminds user after completing a logical unit)
- No-mix rule (content, config, and cross-file fixes stay separate)

If missing, add from the `quality-standards.md` template before proceeding.

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
