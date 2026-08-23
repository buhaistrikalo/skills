---
name: verify-and-close
description: Use when the user asks to verify a task end to end, says "проверь задачу, исправь если че и закрой", or wants a fix validated before closing the task. Do not use for pure root-cause explanations, status lists, or publish-only requests.
metadata:
  short-description: Verify work before closing tasks
---

# Verify And Close

Check a tracked task against its acceptance criteria and current runtime. Close it only when the evidence is sufficient.

## Workflow

1. Read the task, comments, requirements, acceptance criteria, and current status. Inspect the branch and dirty files; preserve unrelated work.
2. Trace the symptom through the real source of truth: UI, API, database, job, provider, or deployment path. Reproduce it when safe.
3. Mark findings as `confirmed`, `hypothesis`, `not reproduced`, or `blocked`. Do not present a plausible explanation as the root cause.
4. If the criteria are not met, make the smallest scoped fix and add a focused regression. If they are met, add only a useful guardrail or regression.
5. Run the focused checks and the relevant project gates: integration, build, typecheck, lint, diff, reviewer, runtime, API, UI, or E2E checks.
6. Close the task only when every acceptance item has evidence. If a check is skipped, times out, or needs unavailable auth/runtime, leave the task open and report the blocker.

## Output

- `Status`: `VERIFIED`, `FIXED`, `NOT_REPRODUCED`, or `BLOCKED`.
- `Evidence`: each acceptance item mapped to a concrete check or source.
- `Root cause`: confirmed, hypothetical, or not established.
- `Changes`: files changed and why, or `none`.
- `Checks`: commands and results, including skipped checks.
- `Task`: closed, left open, or unchanged, with the reason.

## Guardrails

- A skipped check or textual `PASS` is not enough when integration, runtime, or required evidence is missing.
- Do not use a historical error as proof of a current defect or a current green check as proof that a historical error was fixed.
- Preserve unrelated dirty files; do not mutate production, expose secrets, commit, or publish without explicit scope.
