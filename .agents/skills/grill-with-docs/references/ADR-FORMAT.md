# ADR Format

ADRs record durable decisions and the reason they were made. They should be short.

## Location

System-wide ADRs live in:

```text
.agents/docs/adr/
```

Context-specific ADRs live beside that context's glossary:

```text
.agents/feature/<context>/docs/adr/
```

Examples:

```text
.agents/docs/adr/0001-use-domain-events-between-contexts.md
.agents/feature/payment/docs/adr/0001-use-provider-webhooks-as-source-of-truth.md
.agents/feature/history/docs/adr/0001-store-append-only-activity-events.md
```

Create the directory lazily only when the first ADR is needed.

## Numbering

Scan the relevant ADR directory for the highest existing number and increment by one:

```text
0001-slug.md
0002-slug.md
0003-slug.md
```

## Template

```md
# {Short title of the decision}

{One to three sentences explaining the context, what was decided, and why.}
```

Optional sections are allowed only when they add real value:

- `Status` frontmatter such as `proposed`, `accepted`, `deprecated`, or `superseded by ADR-NNNN`.
- `Considered Options` when rejected alternatives are likely to come up again.
- `Consequences` when downstream effects are non-obvious.

## When To Offer An ADR

Offer an ADR only when all three checks pass:

1. The decision is hard to reverse.
2. The decision would be surprising without context.
3. The decision came from a real trade-off between plausible alternatives.

Skip the ADR if the decision is obvious, easy to reverse, temporary, or had no meaningful alternative.

## Good ADR Candidates

- Architectural shape that would be expensive to change later.
- Integration patterns between contexts.
- Technology choices that carry real lock-in.
- Boundary and ownership decisions.
- Deliberate deviations from the obvious path.
- Constraints that are not visible in code.
- Rejected alternatives worth remembering.
