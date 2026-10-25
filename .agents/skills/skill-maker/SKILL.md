---
name: skill-maker
description: Create or improve reusable AI-agent skills, including their trigger descriptions, instructions, supporting resources, and validation. Use when the user asks to write a skill, fix an ineffective skill, update a borrowed skill, or turn a recurring workflow into a skill. Do not use merely to execute a task covered by an existing skill.
---

# Skill Maker

Turn a recurring job into instructions that improve an agent's decisions. Keep the skill self-contained and scale validation to the behavior being changed.

## Understand the job

- Start from the user's request, examples, and reported failures. For an existing skill, read its instructions, metadata, and resources relevant to the change.
- Identify the intended outcome, when the skill should activate, nearby requests it should leave alone, and what would demonstrate success.
- Inspect available files and tools before asking for facts. Ask only about unresolved choices that materially change the result; proceed on routine implementation details within the agreed scope.
- For borrowed skills, establish the source and compare the current upstream version with the local version when available. Preserve local adaptations, inspect required resources and attribution, and report uncertainty if the source or revision cannot be established. Do not overwrite a local skill just because upstream changed.

## Write the smallest useful procedure

- Keep the existing name when updating a skill unless the user requests a rename. Follow the target repository's layout and conventions.
- Write the frontmatter `description` as trigger logic: the recurring job, likely user requests, and exclusions that prevent plausible misrouting.
- In the body, explain the starting point, decisions that change the approach, expected result, and evidence needed to finish. Include failure handling for concrete failure modes.
- Include guidance that changes behavior; omit general knowledge, repeated instructions, and rules derived from a single example unless they generalize.
- Distinguish requirements from defaults. Explain why a constraint matters, and allow another approach when it satisfies the same requirement.
- Preserve the user's scope and existing authorization. Avoid adding approval checkpoints for already agreed work or treating a skill invocation as permission for unrelated external actions.
- Add scripts for repeated or fragile operations, references for substantial conditional guidance, and assets for files used in the output only when needed. Link each resource where it should be used and include every resource the procedure requires.
- Keep tool choices compatible with the target environment. Do not require a particular model, CLI, reviewer UI, or delegation mechanism unless the job actually depends on it; explain what remains possible when an optional tool is unavailable.
- Keep UI metadata consistent with the skill. Add or update `agents/openai.yaml` when the target repository uses it, and update the skill catalog when needed.

## Validate in proportion to the change

Choose the lightest check that can expose a meaningful failure. Increase coverage when the change affects more decisions or has consequential side effects.

| Change | Useful validation |
| --- | --- |
| Wording or a small instruction edit | Inspect the diff for changed meaning, contradictions, broken references, and unintended scope. |
| Trigger or workflow changes | Also walk through realistic requests: an intended use, a nearby request that should not trigger it, and a relevant edge or failure case. Check the expected decision and outcome. |
| Scripts, complex branching, or consequential actions | Also run affected helpers and representative workflows in an isolated workspace with permitted inputs and side effects. Check artifacts and failure handling. |

- Validate frontmatter, resource paths, and metadata with an available validator or direct inspection. Formatting checks do not prove behavioral quality.
- For scenario reviews, state the request, expected behavior, and whether it was checked by inspection or execution. Do not describe a walkthrough as an independent test.
- Use independent runs or comparison against the old version when they would resolve a real uncertainty and the environment supports them. Keep evaluation artifacts outside the shipped skill. Benchmarks and review interfaces are optional, not prerequisites for ordinary edits.
- Respect the task's authorization during trials; do not publish, close real tasks, or mutate production merely to test a skill.
- If a meaningful check cannot run, report what remains unverified. Do not invent results or interpret silence or empty feedback as approval.

## Review and deliver

Review changed files and repository status. Check that the update addresses the reported problem without adding unrelated obligations or removing useful existing behavior.

Report what changed, how it was checked, and any remaining limitation. Iterate on demonstrated failures or user feedback; stop when the requested change and appropriate checks are complete. Commit, install, or publish only when requested.
