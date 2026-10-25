---
name: push-to-main
description: Use when the user asks to push, upload, publish, or "залей" changes to main. Also use when they provide a GitHub remote and want the current repository committed and pushed.
metadata:
  short-description: Commit and push to main carefully
---

# Push To Main

Publish the requested changes to `main` without shipping unrelated files.

## Workflow

1. Establish the source and destination.
   - Inspect the current branch or detached HEAD, remotes, staged and unstaged changes, and untracked files. Preserve unrelated work, including the user's staging choices.
   - Identify the requested changes, including existing commits. Inspect history and diffs; a clean working tree does not mean there is nothing to publish.
   - Choose the intended push remote from the request and repository configuration. Ask only if the destination or scope remains materially ambiguous.
   - Fetch that remote's `main` and compare ancestry with the source and local `main`. Use the fetched remote branch as the integration base; do not assume local `main` is current or that all local commits belong to this request. If remote `main` does not exist, verify the intended initial publication before creating it.

2. Prepare a scoped commit when needed.
   - Review the actual diff, not just filenames. Stage only requested paths or hunks; do not commit unrelated changes already in the index.
   - If mixed changes or the current checkout make isolation difficult, prepare the requested patch in an isolated checkout based on the fetched remote `main`. Preserve the source checkout and its dirty files.
   - Use a short human commit message. Do not add `Co-authored-by` trailers.
   - Reuse existing requested commits when appropriate instead of creating an empty or duplicate commit.

3. Integrate without shipping unrelated history.
   - If the prepared source descends from remote `main` and every outgoing commit is in scope, it can be pushed directly. The source branch does not need to be named `main`.
   - If local `main` is behind and has no outgoing changes, fast-forward it only when the checkout permits it safely. If the requested commits are already on remote `main`, report that no push is needed.
   - For a diverged branch or a branch containing unrelated commits, use an isolated integration branch from the fetched remote `main` and apply only the requested commits or patch. Check dependencies so the selected changes still work without excluded commits.
   - Resolve integration conflicts when the intended result follows from the code and agreed scope. Ask about unresolved behavior choices rather than guessing. Do not rewrite shared history to make integration easier.
   - Review the complete outgoing commit list and diff against remote `main`, and run checks appropriate to the resulting change. Confirm that excluded work did not enter the candidate.

4. Push to the explicit destination and verify.
   - Use an explicit refspec such as `git push <remote> <prepared-ref>:refs/heads/main`; do not rely on the current branch's upstream.
   - After success, verify that remote `main` contains the prepared commit. Report its hash, the destination, checks performed, and final working-tree status, including any local branch left behind the remote.

## When Push Fails

- Read the actual error before retrying. For a non-fast-forward rejection, fetch again, integrate the new remote commits, and recheck the resulting candidate. Never force-push as a shortcut.
- For authentication or permission failures, check the intended remote and available authentication mechanism without exposing credentials. Request missing access only when needed; repeated retries do not fix missing permissions.
- For DNS, connection, proxy, or SSH transport failures, inspect the relevant connectivity and configuration. Retry after a concrete correction or a likely transient failure; do not change security or global network settings just to bypass an error.
- For protected-branch, hook, or required-check rejections, follow the repository's supported review flow when authorized. Do not bypass protections or claim that a PR is a successful push to `main`.
- If the result is uncertain after a connection failure, check whether the remote already contains the commit before pushing again. Stop repeated attempts when the same failure persists without new evidence or a corrective action, and report the exact blocker and remaining step.

## Guardrails

- Do not include unrelated dirty files.
- Do not run destructive git commands unless explicitly requested.
- A request to publish the scoped changes is sufficient authorization for the normal commit and push flow; do not add a second approval checkpoint unless a new material decision or an actual environment requirement demands it.
