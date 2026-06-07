# CONTEXT.md Format

`CONTEXT.md` is a glossary for one domain context. It records the project's canonical language, not the implementation plan.

## Location

Single-context repos use:

```text
.agents/CONTEXT.md
```

Multi-context repos use:

```text
.agents/CONTEXT-MAP.md
.agents/feature/<context>/CONTEXT.md
```

Example:

```text
.agents/CONTEXT-MAP.md
.agents/feature/payment/CONTEXT.md
.agents/feature/history/CONTEXT.md
```

## Structure

```md
# {Context Name}

{One or two sentences explaining what this context is and why it exists.}

## Language

**Order**: A customer request for goods or services that the business has agreed to track.
_Avoid_: Purchase, transaction

**Invoice**: A request for payment sent to a customer after delivery.
_Avoid_: Bill, payment request

**Customer**: A person or organization that places orders.
_Avoid_: Client, buyer, account
```

## Rules

- Be opinionated. When multiple words could describe the same concept, pick one canonical term and list the weaker names under `_Avoid_`.
- Keep definitions tight. One or two sentences is usually enough.
- Define what the term is, not what it does in code.
- Only include terms specific to this project's domain context.
- Exclude general programming concepts, infrastructure terms, utility patterns, and implementation details.
- Group terms under subheadings only when natural clusters emerge.

Before adding a term, ask whether it belongs to the domain language or to the implementation. Only domain language belongs here.

## Context Map

When several contexts exist, `.agents/CONTEXT-MAP.md` lists where their glossaries live and how the contexts relate:

```md
# Context Map

## Contexts

- [Payment](./feature/payment/CONTEXT.md): collects money and tracks payment outcomes.
- [History](./feature/history/CONTEXT.md): records user-visible activity over time.
- [Fulfillment](./feature/fulfillment/CONTEXT.md): manages picking, packing, and dispatch.

## Relationships

- **Payment -> History**: Payment emits payment outcome events; History records them for the activity timeline.
- **Fulfillment -> History**: Fulfillment emits shipment events; History records them for user-visible order progress.
- **Payment <-> Fulfillment**: They share stable identifiers but do not own each other's entities.
```

The skill infers which structure applies:

- If `.agents/CONTEXT-MAP.md` exists, read it to find contexts.
- If only `.agents/CONTEXT.md` exists, use the single context.
- If neither exists, create the first context file lazily when a term is resolved.
- If multiple contexts exist and the right one is unclear after code/docs exploration, ask one clarifying question.
