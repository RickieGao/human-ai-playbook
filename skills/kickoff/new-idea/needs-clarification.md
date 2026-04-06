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
