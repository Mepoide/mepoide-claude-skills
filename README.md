# Mario's Claude Code skills

Personal skill library for Claude Code, installed at `~/.claude/skills/` (applies to every project on this machine).

## Provenance

- **22 skills copied from [mattpocock/skills](https://github.com/mattpocock/skills)** (`engineering/` and `productivity/` buckets, MIT-licensed — see [LICENSE-mattpocock-skills.md](LICENSE-mattpocock-skills.md)): `ask-matt`, `codebase-design`, `code-review`, `diagnosing-bugs`, `domain-modeling`, `grill-with-docs`, `implement`, `improve-codebase-architecture`, `prototype`, `research`, `resolving-merge-conflicts`, `setup-matt-pocock-skills`, `tdd`, `to-spec`, `to-tickets`, `triage`, `wayfinder`, `grilling`, `grill-me`, `handoff`, `teach`, `writing-great-skills`.

  These are fixed copies, not symlinks — this repo doesn't auto-update when upstream changes. To pull in upstream improvements, diff `skills/{engineering,productivity}/<name>/SKILL.md` in a fresh clone of `mattpocock/skills` against the copy here and merge by hand.

- **3 original skills**, written for this library, inspired by [gstack](https://github.com/garrytan/gstack)'s concepts but not copied from it (gstack's own SKILL.md files are tightly coupled to its own product infra — telemetry, `~/.gstack` state, compiled binaries, a branded voice its own docs say not to alter):
  - `context-save` / `context-restore` — save and resume working context (git state, decisions, next steps) across sessions, as plain files in the working repo's `.agent-context/`.
  - `health` — read-only code-quality dashboard (type checker, linter, tests, dead code) using whatever commands the target repo already documents.

## License

Skills under `LICENSE-mattpocock-skills.md`'s terms retain that copyright notice per MIT. The three original skills have no separate license file; treat them as freely reusable/modifiable personal tooling.
