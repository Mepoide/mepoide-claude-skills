---
name: health
description: Produce a code-quality dashboard for the current repo — type checker, linter, tests, and dead-code/dependency findings — as a single report. Use when asked "how healthy is this codebase", "run a health check", or before a big refactor to establish a baseline.
---

# Health Check

A read-only report. Don't fix anything here — that's a separate task once the user picks what matters.

## Steps

1. Detect the project's real commands instead of guessing:
   - Look for `package.json` scripts (`typecheck`, `lint`, `test`), `Makefile` targets, `pyproject.toml` (`ruff`, `mypy`, `pytest`), `Cargo.toml`, `go.mod`, etc.
   - If a `CLAUDE.md` or `AGENTS.md` documents the commands, use those verbatim rather than re-deriving them.
   - If nothing is documented and it's ambiguous, ask once rather than guessing wrong and reporting noise.
2. Run, in order, capturing pass/fail and counts (don't halt on the first failure — a health check's value is seeing everything at once):
   - Type checker
   - Linter
   - Test suite
   - Dead code / unused dependency detection if a tool for it already exists in the repo (e.g. `knip`, `ts-prune`, `vulture`, `deadcode`) — don't install a new one uninvited.
3. Report as a compact table: tool, status (pass/fail/not configured), count of errors or warnings, and the single most-common failure category if there are many of the same kind.
4. Call out anything that looks like a growing trend if a previous health report exists to compare against (e.g. saved in `.agent-context/` via the `context-save` skill) — otherwise this run is just the baseline.
5. End with a short, prioritized "if you fix one thing" recommendation — not a mandate, a suggestion.

## Rules

- Read-only. Never auto-fix lint errors, never modify test files, never touch dependencies.
- If a check isn't configured in this repo, say "not configured" rather than skipping it silently — the absence is itself useful signal.
