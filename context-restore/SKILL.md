---
name: context-restore
description: Resume work from a context previously saved by the context-save skill, even in a fresh session or on a different machine. Use when asked to "resume", "restore context", "pick up where I left off", or at the start of a session on a repo that has a `.agent-context/` directory.
---

# Context Restore

## Steps

1. List saved contexts for the current branch:
   ```bash
   git rev-parse --abbrev-ref HEAD
   ls -t .agent-context/*.md 2>/dev/null
   ```
   If the user asked for a specific branch or "all branches", read the `branch:` frontmatter of each file instead of relying on `ls` order.
2. If there are none, say so plainly — don't invent a summary.
3. If there's exactly one, read it. If there are several, show a short numbered list (date, title, branch) and ask which one, defaulting to the most recent for the current branch.
4. Read the chosen file. Cross-check it against current reality before trusting it:
   ```bash
   git status --short
   git diff --stat
   git log --oneline -10
   ```
   Flag anything the saved file claims that no longer matches (e.g. a "remaining work" item that's already been committed, or a file listed as modified that's now clean).
5. Give a short welcome-back summary: what was being worked on, key decisions (treat these as settled — don't silently re-litigate them, but say so explicitly if you think one should be reconsidered), and the next concrete step from "Remaining work".
6. Continue the task from there — this skill's job ends once the user has full context back.
