---
name: handoff
description: Use when the user wants to compact the current conversation into a handoff document for another agent or future session to continue the work. Also use when they mention handoff, transfer context, continue in a new session, or summarize the session for the next agent.
metadata:
  short-description: Prepare an agent handoff document
---

# Handoff

Create a compact handoff document so a fresh agent can continue the current work.

## Workflow

1. Clarify the focus from the user request.
   - If the user passed arguments or described the next session, tailor the handoff to that goal.
   - If no focus is provided, summarize the active work and current state.

2. Gather only useful continuation context.
   - Include the goal, decisions made, current status, blockers, changed files, commands run, validation results, and next actions.
   - Reference existing artifacts by path or URL instead of duplicating them.
   - Mention relevant open questions and assumptions.

3. Add a suggested skills section.
   - List the skills the next agent should invoke and why.
   - Include only skills that are relevant to the next likely task.

4. Redact sensitive data.
   - Do not include API keys, passwords, tokens, private credentials, or unnecessary personally identifiable information.
   - Replace sensitive values with clear placeholders such as `[REDACTED_API_KEY]`.

5. Save the handoff outside the workspace.
   - Write the document to the user's OS temporary directory, not the current repository.
   - Use a descriptive filename such as `handoff-<short-topic>.md`.
   - In the final response, provide the saved path and a brief note on what the handoff covers.

## Output

The handoff document should usually include:

- current objective
- what has already happened
- important files, URLs, or artifacts
- current repo/runtime state
- suggested skills
- next steps
- validation and known risks

## Guardrails

- Do not copy long content from PRDs, plans, ADRs, issues, commits, or diffs; link to them.
- Do not save the handoff inside the project unless the user explicitly asks.
- Do not expose secrets while trying to be complete.
