---
name: skill-maker
description: Use when the user wants to create a new skill in this repository from an idea, workflow, or area of expertise. Also use when they want to add the skill folder, SKILL.md, agents/openai.yaml, and README entry in one pass.
metadata:
  short-description: Add a new skill to this repo
---

# Skill Maker

Create a publishable skill in this repository from a rough idea.

## Workflow

1. Choose a sharp name.
   - Use short kebab-case.
   - Prefer concrete task names over broad categories.
   - If the user dislikes a name, suggest simpler alternatives.

2. Write the skill.
   - Create `.agents/skills/<skill-name>/SKILL.md`.
   - Write frontmatter with `name`, `description`, and `metadata.short-description`.
   - Keep the body concise: purpose, workflow, guardrails, output.

3. Add UI metadata.
   - Create `.agents/skills/<skill-name>/agents/openai.yaml`.
   - Include `display_name`, `short_description`, and `default_prompt`.

4. Update repository docs.
   - Add the skill to the README table.
   - Keep the README description short and outcome-focused.

5. Verify.
   - Confirm files exist.
   - Run `git diff --check`.
   - Review `git status --short`.

## Guardrails

- Do not add a README inside each skill folder.
- Do not add scripts or references unless the workflow needs them.
- Do not make the skill a generic essay; make it an operating procedure.
