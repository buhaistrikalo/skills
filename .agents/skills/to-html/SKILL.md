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

   - Choose the representation that makes the relationship easiest to inspect: semantic HTML/CSS, inline SVG, an embedded image, or a small interactive view with inline JavaScript. Hand-authored SVG is an option, not a requirement.
   - Give meaningful visual elements clear labels and provide an accessible text explanation. Use stable identifiers when needed for interaction.
   - One diagram answers one question. Put dense explanations in adjacent HTML, not inside the diagram.
   - Use before/after comparison for behavior changing over time, and tables only for aligned facts or trade-offs.

4. Create one descriptive `.html` file in the active workspace. It must open directly in a browser:

   - HTML5 document with language, title, charset, viewport, semantic landmarks, and explicit background.
   - Embed all required styles, scripts, fonts, and media in the file. Use system fonts or embedded fonts. Opening and using the artifact must require no build step, server, CLI, external CDN, account, or network access.
   - When representing an existing product, reuse its visual tokens and hierarchy after inspecting them. Otherwise use a restrained neutral style.
   - Responsive layout for narrow and wide screens. Make overflow and long labels intentional.
   - Include short code blocks only when they help assess a contract, behavior, or trade-off. Label existing code and proposed examples clearly; avoid implementation dumps. File paths may appear as compact evidence when they support an architectural claim.

## Verify and deliver

1. Confirm that the document separates current state from proposal and names its decision.
2. Check that every diagram edge and layer-impact claim is supported by inspected evidence or marked as an open question.
3. Check for external resource dependencies. Render the file when a local preview is available; check narrow layout, clipped content, contrast, horizontal overflow, and any interactions without network access. Report checks that could not be performed.
4. Deliver the same file path in chat. Iterate on that file when the user asks for changes.

## Boundaries

- Keep the artifact focused on evaluating the decision; visuals and code examples should support that purpose.
- Do not add a chat, annotation system, polling loop, local server, or publishing flow.
- Do not create a diagram merely to restate paragraphs; show a relationship that is otherwise hard to see.
- Prefer normal chat for a small answer with no decision, relationship, or change impact to inspect.
