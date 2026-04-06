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
