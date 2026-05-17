---
name: write-a-skill
description: Use when the user wants to create, improve, or package an AI agent skill for a public repo, personal expertise, or reusable workflow. Also use when they mention writing a skill, skill ideas, skill positioning, skill README/SKILL.md, or turning know-how into a concise reusable agent workflow.
metadata:
  short-description: Create sharp reusable agent skills
---

# Write A Skill

Help the user turn a narrow piece of expertise into a practical AI-agent skill.

## Goal

Create skills that feel useful, specific, and credible. A good skill should make an agent noticeably better at one recurring job, not explain a broad topic.

## Workflow

1. Pick a narrow job.
   - Prefer "fix failing GitHub Actions from logs" over "DevOps".
   - Prefer "write competitor alternative pages" over "marketing".
   - Prefer tasks with repeated steps, hidden judgment, failure modes, or templates.

2. Define the trigger.
   - Write the `description` as activation logic, not marketing copy.
   - Include user phrases that should trigger the skill.
   - Exclude nearby tasks that should not trigger it.

3. Write the minimum operating procedure.
   - Start with what the agent should do first.
   - Add decision points only where they change behavior.
   - Include validation steps and common mistakes.
   - Do not teach general knowledge the model already has.

4. Add resources only when they earn their weight.
   - `scripts/` for repeatable commands or fragile transformations.
   - `references/` for long examples, schemas, checklists, or provider docs.
   - `assets/` for templates, images, boilerplate, or files copied into outputs.

5. Package it for discovery.
   - Put the skill under `.agents/skills/<skill-name>/`.
   - Include `SKILL.md`.
   - Add `agents/openai.yaml` when the repo uses Codex skill UI metadata.

## Skill Shape

Use this default structure:

```markdown
---
name: short-kebab-name
description: Use when the user wants to ... Also use when they mention ...
metadata:
  short-description: Verb phrase under 60 chars
---

# Human Title

One sentence: what this skill makes the agent better at.

## Workflow

1. First concrete step.
2. Second concrete step.
3. Verification or delivery step.

## Guardrails

- Avoid ...
- Prefer ...
- Ask only when ...
```

## Quality Bar

- The skill has one clear job.
- The trigger description is more specific than the title.
- The workflow changes how the agent behaves.
- The body is short enough to read in one pass.
- It names failure modes that a generic prompt would miss.
- It includes verification when the task can be checked.

## Idea Filter

Good skill ideas usually pass at least two checks:

- The task repeats often.
- The user has a recognizable point of view.
- The task has a concrete artifact at the end.
- Mistakes are expensive or embarrassing.
- There is a reliable workflow that most people skip.
- The public title makes expertise legible.

## Output

When creating a skill, produce the files directly when working in a repo. Otherwise, return:

- skill name
- trigger description
- final `SKILL.md`
- optional resource list
- one-line positioning for the public repo
