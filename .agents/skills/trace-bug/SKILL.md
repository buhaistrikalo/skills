---
name: trace-bug
description: Use when the user asks why a bug happens, wants an explanation grounded in code, or says to check the real code/data path before fixing. Also use for missing data, inconsistent UI state, broken workflows, and suspected backend/frontend contract issues.
metadata:
  short-description: Trace bugs from real code paths
---

# Trace Bug

Trace a bug to an evidence-backed explanation. Distinguish a mechanism that could produce the symptom from the confirmed cause of the reported failure.

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
   - State what the inspected code establishes and which conditions would produce the symptom. Code showing a possible failure path does not by itself prove that this path caused the reported incident.
   - Confirm the cause only when reproduction, logs, or observed data connect the mechanism to the affected case and relevant code version. State the evidence and its limits; a local reproduction does not prove what ran in production.
   - Without that connection, label the explanation as a hypothesis. Name the missing evidence and a concrete check that would support or rule it out, such as reproducing the affected inputs or inspecting the relevant request, log, or stored value.
   - Name the smallest place where a fix belongs when the evidence supports it; otherwise describe the candidate fix conditionally.

4. Fix only when requested or clearly implied.
   - Prefer root-cause fixes over masking symptoms.
   - Keep the diff scoped to the traced path.
   - Add targeted validation when the behavior can regress.
   - Keep incident confirmation separate from fix validation. Passing checks for a change does not retroactively confirm a hypothesis about the original failure.

## Output

- cause: confirmed, hypothesis, or not established, with supporting evidence and limits
- relevant code path
- fix made or recommended
- verification performed
- next diagnostic check when the cause remains unconfirmed
