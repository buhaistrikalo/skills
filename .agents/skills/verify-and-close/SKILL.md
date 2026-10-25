---
name: verify-and-close
description: Use when the user asks to verify a task end to end, says "проверь задачу, исправь если че и закрой", or wants a fix validated before closing the task. Do not use for pure root-cause explanations, status lists, or publish-only requests.
metadata:
  short-description: Verify work before closing tasks
---

# Verify And Close

Check a tracked task against its acceptance criteria and current runtime. Close it only when the evidence is sufficient.

## Workflow

1. Read the task, comments, requirements, acceptance criteria, and current status. Identify the evidence required by those criteria and applicable project gates; distinguish it from optional checks. Do not downgrade a required check merely because it is unavailable. Inspect the branch and dirty files; preserve unrelated work.
2. Trace the symptom through the real source of truth: UI, API, database, job, provider, or deployment path. Reproduce it when safe.
3. Mark findings as `confirmed`, `hypothesis`, `not reproduced`, or `blocked`. Do not present a plausible explanation as the root cause.
4. If the criteria are not met, make the smallest scoped fix and add regression coverage when it meaningfully protects the changed behavior. If the criteria are already met, finish without code changes; do not add a guardrail or test merely to produce a diff.
5. Run the focused checks and applicable required project gates. Choose additional integration, build, typecheck, lint, reviewer, runtime, API, UI, or E2E checks according to the behavior and risk; the list is not a mandatory checklist.
6. Close the task only when every acceptance item and required project gate has sufficient evidence. If required evidence is missing, leave the task open and name the missing evidence and how to obtain it. A skipped, timed-out, or unavailable optional check does not by itself block closure; report the limitation and why the available evidence is sufficient.

## Output

- `Status`: `VERIFIED`, `FIXED`, `NOT_REPRODUCED`, or `BLOCKED`.
- `Evidence`: each acceptance item mapped to a concrete check or source.
- `Root cause`: confirmed, hypothetical, or not established.
- `Changes`: files changed and why, or `none`.
- `Checks`: commands and results, including skipped checks, whether they are required or optional, and any resulting limitations.
- `Task`: closed, left open, or unchanged, with the reason.

## Guardrails

- A textual `PASS` or unrelated green check does not replace required evidence. A failed optional check that reveals an unmet acceptance criterion must be addressed before closure.
- Do not use a historical error as proof of a current defect or a current green check as proof that a historical error was fixed.
- Preserve unrelated dirty files; do not mutate production, expose secrets, commit, or publish without explicit scope.
