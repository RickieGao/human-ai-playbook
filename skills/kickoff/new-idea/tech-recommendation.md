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
