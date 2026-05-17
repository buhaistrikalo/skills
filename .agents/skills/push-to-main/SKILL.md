---
name: push-to-main
description: Use when the user asks to push, upload, publish, or "залей" changes to main. Also use when they provide a GitHub remote and want the current repository committed and pushed.
metadata:
  short-description: Commit and push to main carefully
---

# Push To Main

Publish the requested changes to `main` without shipping unrelated files.

## Workflow

1. Check state.
   - Verify branch, remote, and changed files.
   - Identify which paths belong to the user's request.

2. Commit only the requested change.
   - Stage only relevant files.
   - Review staged paths before committing.
   - Use a short human commit message.
   - Do not add `Co-authored-by` trailers.

3. Push and confirm.
   - Push to `main`.
   - Report commit hash and final git status.

## Guardrails

- Do not include unrelated dirty files.
- Do not run destructive git commands unless explicitly requested.
- If push fails because of network or SSH restrictions, request escalation and retry.
