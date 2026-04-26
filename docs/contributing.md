# Contributing to systematic-debugging-skill

Thank you for helping sharpen a **process skill** used under time pressure. Keep changes **literate**, **enforceable**, and **short enough to fit in context**.

## Where to edit

- **Primary:** `SKILL.md` only for behavioral/process changes.
- **Secondary:** `README.md` for install paths, audience, repo structure table.
- **`docs/`:** Maintainer-facing depth; keep aligned with `SKILL.md` (no contradictory gates).

## Design principles

1. **One phase at a time** — don’t blur Phase 1 evidence with Phase 4 patches in the same instruction block.
2. **Violations must be explicit** — name what “counts as skipping Phase 0” so agents can’t rationalize shortcuts.
3. **Operational, not philosophical** — every section should change what someone does in the next five minutes.

## Versioning

- Bump **`version`** in frontmatter when you materially change phase definitions or Iron Law wording.
- Use commit messages that explain **why** a gate moved (e.g. “CI boundary logging”).

## Testing contributions

There is no automated test suite. Review checklist:

- [ ] Read the full `SKILL.md` top-to-bottom — flows still linear where intended.
- [ ] Frontmatter YAML still valid (quotes, colons).
- [ ] README clone path matches actual GitHub org/repo.
- [ ] LICENSE file untouched unless lawyers/org policy require it.

## Tone and language

- Default body is **English** per upstream; README may be bilingual — keep technical terms consistent (`Phase`, `Iron Law`, `root cause`).
- Avoid doubling length unless adding **new gates** or **new failure modes**; practitioners skim under stress.

## Attribution

- Upstream inspiration is MIT — preserve **attribution** line in frontmatter when merging ideas from **obra/superpowers-skills**.

## Pull requests

- One logical change per PR (e.g. “Phase 1 multi-component block” OR “Phase 4.5 architecture stop rule”, not both).
- If you add examples, use **fictional** file names — avoid looking like real employer code dumps.

## Local preview

Render `SKILL.md` in any Markdown viewer; Claude Code users can symlink the folder into `~/.claude/skills/systematic-debugging` and invoke in a throwaway session.

## Changelog discipline

For user-visible phase renames or new hard stops, add a short bullet under README or in the PR description so downstream forks can rebase consciously.
