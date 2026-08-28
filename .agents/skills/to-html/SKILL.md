---
name: to-html
description: Create a standalone HTML decision document from a product or technical discussion. Use when the user asks to visualize a plan, architecture, current versus target behavior, system relationships, impact of a change, or an implementation proposal as an HTML page. Also use when they say "/to-html", "сделай HTML-план", "визуализируй архитектуру", or "покажи связи". Do not use for static images, production UI implementation, slide decks, or an answer that is clearer as short chat prose.
metadata:
  short-description: Turn plans and architecture into HTML
---

# To HTML

Create one portable HTML file that helps the user inspect a decision before implementation.

## Build the document from evidence

1. Inspect the relevant product, code, and documents before writing. Distinguish verified current behavior, proposed changes, and open questions. Do not present an inference as an existing fact.

2. Define the document around one decision. Use only the sections that clarify it:

   - goal and user-visible outcome;
   - current state;
   - target behavior or proposed approach;
   - architecture, sequence, or dependency map;
   - impact by layer: UI, API, contracts, storage, operations;
   - risks, migration concerns, and acceptance checks;
   - options only when the user needs to choose.

3. Put relationships in visuals, not decorative cards:

   - Use hand-authored inline SVG for architecture, flows, and state transitions.
   - Give every meaningful SVG node and edge a stable `id` and a `<title>`.
   - One diagram answers one question. Put dense explanations in adjacent HTML, not inside the SVG.
   - Use before/after comparison for behavior changing over time, and tables only for aligned facts or trade-offs.

4. Create one descriptive `.html` file in the active workspace. It must open directly in a browser:

   - HTML5 document with language, title, charset, viewport, semantic landmarks, and explicit background.
   - Inline CSS and SVG by default; no build step, server, CLI, external CDN, account, or network dependency.
   - When representing an existing product, reuse its visual tokens and hierarchy after inspecting them. Otherwise use a restrained neutral style.
   - Responsive layout for narrow and wide screens. Make overflow and long labels intentional.
   - Do not place source-code blocks in the artifact. File paths may appear as compact evidence when they support an architectural claim.

## Verify and deliver

1. Confirm that the document separates current state from proposal and names its decision.
2. Check that every diagram edge and layer-impact claim is supported by inspected evidence or marked as an open question.
3. Render the file when a local preview is available; check narrow layout, clipped content, contrast, and horizontal overflow.
4. Deliver the same file path in chat. Iterate on that file when the user asks for changes.

## Boundaries

- This is a decision artifact, not a mockup of production UI and not an implementation plan made of code snippets.
- Do not add a chat, annotation system, polling loop, local server, or publishing flow.
- Do not create a diagram merely to restate paragraphs; show a relationship that is otherwise hard to see.
- Prefer normal chat for a small answer with no decision, relationship, or change impact to inspect.
