# Kickoff Agent - Project Initialization Guide

> Guides users through a structured interview to generate a CLAUDE.md
> and initial project structure for human-AI collaboration.

## Overview

The Kickoff Agent conducts a 3-round interview, then assembles outputs:

```
Round 1: Project Basics     -> What are you building?
Round 2: Collaboration Prefs -> How do you want to work with AI?
Round 3: Environment Setup   -> What tools and constraints?
         |
         v
Output: CLAUDE.md + project structure suggestions + memory recommendations
```

## How to Use

Invoke this agent at the start of a new project. It will ask you questions
in 3 rounds and generate a customized CLAUDE.md based on your answers.

### Round 1: Project Basics
- Project name and description
- Tech stack (language, framework, database, etc.)
- Project type (greenfield, existing codebase, migration, etc.)
- Team size (solo, small team, large team)
- Primary goals and success criteria

### Round 2: Collaboration Preferences
- Preferred workflow (TDD, plan-first, spec-driven, incremental)
- AI autonomy level (strict review, moderate, high autonomy)
- Communication style (verbose, concise, minimal)
- Code style preferences (formatting, naming conventions)
- Review process (every change, per feature, per PR)

### Round 3: Environment Configuration
- Build and test commands
- CI/CD setup
- Special tools or constraints
- Security requirements
- Known pitfalls or gotchas

## Output

After the interview, the agent:
1. Assembles a CLAUDE.md from template fragments (see `templates/`)
2. Suggests initial project structure
3. Recommends memory/tool configuration
4. Provides a summary for human review before finalizing

## Design Principles

- Ask one round at a time; do not overwhelm
- Provide defaults and examples for each question
- Let the user skip questions (sensible defaults apply)
- Always show the assembled result for human review before writing files
- Follow the Meta Agent communication principles at all times
