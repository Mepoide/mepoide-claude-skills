---
name: context-save
description: Save the current working context (git state, decisions made, remaining work) to a file so a future session — possibly on a different machine or after a break — can resume without losing a beat. Use when asked to "save progress", "save context", "checkpoint this", or before a long break/handoff.
---

# Context Save

Capture enough state that a cold read of the saved file is sufficient to resume work with no other memory.

## Steps

1. Gather git state:
   ```bash
   git rev-parse --abbrev-ref HEAD
   git status --short
   git diff --stat
   git log --oneline -10
   ```
2. Determine the save location: `.agent-context/` at the repo root. Create it if missing, and make sure it's covered by `.gitignore` (add a `.agent-context/` line if not already ignored) — this is working scratch state, not something to commit.
3. Write a new file `.agent-context/<UTC timestamp>-<slug-of-title>.md` (never overwrite an existing save; each save is a new file). Infer a short title (3-6 words) from the conversation if the user didn't give one.

   File contents:
   ```markdown
   ---
   branch: <current branch>
   timestamp: <ISO-8601>
   files_modified:
     - <path>
   ---

   ## Working on: <title>

   ### Summary
   <1-3 sentences: the goal and current progress>

   ### Decisions made
   - <architectural choice or trade-off, and why>

   ### Remaining work
   1. <next step, in priority order>

   ### Notes
   <gotchas, things tried that didn't work, open questions>
   ```
4. Confirm to the user with the file path and a one-line summary of what was saved.

## Rules

- Never modify code — this skill only reads state and writes the context file.
- Always include the branch name — needed for cross-branch resume via `context-restore`.
- Infer content from git state and conversation history; only ask the user if the title or summary genuinely can't be inferred.
