---
name: figma-fix
description: Use when the user provides a Figma node, screenshot, or visual reference and wants a narrow frontend change to match it. Also use for small UI copy, layout, spacing, state, or component adjustments driven by a concrete design reference.
metadata:
  short-description: Apply focused Figma UI fixes
---

# Figma Fix

Turn a concrete Figma or screenshot reference into a narrow frontend change.

## Workflow

1. Identify the exact surface.
   - Find the component, route, modal, table, or widget that corresponds to the design.
   - Keep scope to the named surface unless the user expands it.

2. Match existing product patterns.
   - Reuse local components, tokens, icons, and layout conventions.
   - Avoid new abstractions for one-off visual tweaks.
   - Do not touch backend code for frontend-only requests.

3. Implement the smallest useful diff.
   - Change only the files needed for the visible result.
   - Preserve adjacent behavior and unrelated copy.
   - Make text fit on mobile and desktop.

4. Verify visually when possible.
   - Run targeted lint/type checks when available.
   - Use browser or screenshots for meaningful UI changes.
   - Check that responsive layout and text do not overlap.

## Experimental Note

This skill works best when the user supplies a concrete node, screenshot, or exact UI surface. If the reference is vague, first find the closest implemented surface and state the assumption.
