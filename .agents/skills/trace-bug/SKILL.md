---
name: trace-bug
description: Use when the user asks why a bug happens, wants an explanation grounded in code, or says to check the real code/data path before fixing. Also use for missing data, inconsistent UI state, broken workflows, and suspected backend/frontend contract issues.
metadata:
  short-description: Trace bugs from real code paths
---

# Trace Bug

Find the real source of a bug before proposing or making a fix.

## Workflow

1. Start from the symptom.
   - Identify the exact user-visible behavior.
   - Find the route, component, command, endpoint, job, or database field involved.
   - Do not ask for credentials if local code already explains the likely path.

2. Trace the source of truth.
   - Follow data from persistence/API to UI or from UI action to backend handler.
   - Prefer real code references over guesses.
   - Distinguish display transforms from stored data.

3. Explain the cause.
   - State where the behavior comes from.
   - Separate confirmed facts from assumptions.
   - Name the smallest place where the fix belongs.

4. Fix only when requested or clearly implied.
   - Prefer root-cause fixes over masking symptoms.
   - Keep the diff scoped to the traced path.
   - Add targeted validation when the behavior can regress.

## Output

- root cause
- relevant code path
- fix made or recommended
- verification performed
