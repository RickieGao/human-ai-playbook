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
