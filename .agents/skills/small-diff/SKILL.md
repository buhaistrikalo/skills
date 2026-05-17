---
name: small-diff
description: Use when a change has become too large, the user worries about extra lines or overengineering, or asks to simplify, reduce scope, avoid unrelated changes, or keep only the necessary diff.
metadata:
  short-description: Reduce changes to the needed diff
---

# Small Diff

Audit and shrink a change until only the useful work remains.

## Workflow

1. Inspect the diff.
   - Run `git status --short` and review the changed files.
   - Use `git diff --stat` to find noisy files.
   - Separate intended behavior changes from formatting, rewrites, and unrelated edits.

2. Classify the work.
   - Required: needed for the user request.
   - Incidental: harmless but not needed.
   - Risky: broad abstraction, behavior drift, or unrelated cleanup.

3. Trim.
   - Remove incidental and risky edits unless they are required.
   - Prefer existing flags, helpers, and patterns over new cross-tree plumbing.
   - Keep the fix close to the source of the requirement.

4. Recheck.
   - Run targeted checks for the touched surface.
   - Run `git diff --check`.
   - Explain what was removed and why.

## Output

- what changed
- what was cut
- remaining risk
- verification performed
