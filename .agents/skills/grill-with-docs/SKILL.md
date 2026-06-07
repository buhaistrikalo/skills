---
name: grill-with-docs
description: Use when the user wants to stress-test a plan against the project's existing domain language, glossary, code behavior, and documented decisions. Also use when they mention grilling a plan, sharpening terminology, walking a design tree, updating CONTEXT.md, or deciding whether an ADR is needed.
metadata:
  short-description: Stress-test plans against domain docs
---

# Grill With Docs

Challenge a plan against the existing domain model, sharpen the language, and capture resolved terminology and durable decisions under `.agents/`.

## Workflow

1. Start with the plan and the current source of truth.
   - Read the user's plan closely enough to identify the first unresolved domain or design decision.
   - Explore the codebase when a question can be answered from code instead of asking the user.
   - During exploration, look for `.agents/CONTEXT-MAP.md`, `.agents/CONTEXT.md`, `.agents/feature/**/CONTEXT.md`, and ADRs under `.agents/**/docs/adr/`.

2. Locate the documentation context.
   - If `.agents/CONTEXT-MAP.md` exists, use it to find the relevant context.
   - If only `.agents/CONTEXT.md` exists, treat the repo as a single-context project.
   - If neither exists, create documentation lazily only after the first term or decision is resolved.
   - Keep all generated domain docs under `.agents/`; do not create root `CONTEXT.md`, root `docs/adr/`, or context docs inside the application source tree.

3. Interview one decision at a time.
   - Ask exactly one question, wait for feedback, then continue.
   - For every question, give your recommended answer and the reason.
   - Walk the design tree by resolving dependencies between decisions before moving to downstream choices.
   - If code can answer part of the question, inspect it first and make the question more precise.

4. Challenge the plan against domain language.
   - If the user uses a term that conflicts with an existing glossary entry, call it out immediately.
   - If the user uses vague or overloaded language, propose a precise canonical term.
   - Stress-test relationships with concrete scenarios and edge cases.
   - When the user states how something works, check whether the code agrees. Surface contradictions directly.

5. Update `.agents/**/CONTEXT.md` inline when terms are resolved.
   - Capture resolved terms immediately instead of batching them for the end.
   - Use `references/CONTEXT-FORMAT.md`.
   - Keep `CONTEXT.md` as a glossary only. Do not put implementation details, API routes, file paths, database choices, task lists, or design notes in it.

6. Offer ADRs sparingly.
   - Offer an ADR only when the decision is hard to reverse, surprising without context, and the result of a real trade-off.
   - If any of those checks fails, skip the ADR.
   - Use `references/ADR-FORMAT.md`.
   - Store ADRs under `.agents/docs/adr/` for system-wide decisions or `.agents/feature/<context>/docs/adr/` for context-specific decisions.

## Documentation Layout

Single-context repos:

```text
/
|-- .agents/
|   |-- CONTEXT.md
|   `-- docs/
|       `-- adr/
`-- src/
```

Multi-context repos:

```text
/
|-- .agents/
|   |-- CONTEXT-MAP.md
|   |-- docs/
|   |   `-- adr/                    # system-wide decisions
|   `-- feature/
|       |-- payment/
|       |   |-- CONTEXT.md
|       |   `-- docs/adr/           # payment-specific decisions
|       `-- history/
|           |-- CONTEXT.md
|           `-- docs/adr/           # history-specific decisions
`-- src/
```

## Guardrails

- Do not ask the user questions that code or existing docs can answer.
- Do not ask a bundle of questions. One question per turn is the point of the skill.
- Do not let `CONTEXT.md` become a spec, scratchpad, task list, or architecture document.
- Do not create ADRs for obvious, reversible, or no-alternative decisions.
- Do not write domain documentation outside `.agents/` unless the user explicitly asks.
