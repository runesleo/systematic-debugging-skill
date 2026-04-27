# systematic-debugging-skill

A single-file Claude Code skill that forces **Phase 0 context recall → Phase 1 root-cause work → Phase 2 pattern diffing → Phase 3 hypothesis tests → Phase 4 implementation**. `SKILL.md` states you may not enter the next phase until the previous one is done, and you may not ship fixes before root-cause investigation.

## When to use

- You hit **bugs, failing tests, unexpected behavior, performance issues, build breaks, or integration failures** and you are **before** the fix (matches the frontmatter `when_to_use` and the “ANY technical issue” bullet list in `SKILL.md`).
- Pressure tempts a quick patch, or you already burned multiple guesses—the skill explicitly calls those **high-signal** moments to follow the process.
- Multi-hop systems need logging at component boundaries before you pick a fix (`SKILL.md` Phase 1 guidance on evidence across layers).

## When NOT to use

- There is **no failing state** to investigate—no bug, no failing test, no unexpected behavior, no perf/build/integration issue. The Iron Law and Phase 4’s “create a failing test case” assume a defect-driven loop (`SKILL.md` Overview / Phase 4).
- Pure conceptual Q&A or reading code for pleasure with **no** remediation path; the gates target debugging work, not general study.
- Your workflow cannot emit the Phase 0 recall block before Phase 1. Skipping that is explicitly labeled a process failure in `SKILL.md`.

## Quick Start

```bash
git clone https://github.com/runesleo/systematic-debugging-skill ~/.claude/skills/systematic-debugging
```

Or copy `SKILL.md` to `~/.claude/skills/systematic-debugging/SKILL.md`.

Reference the skill manually in chat, or point `CLAUDE.md` at it so agents load the flow before patching.

## Typical scenarios

- Red CI: gather logs and recent diffs first, then touch code.
- Flaky production: stabilize reproduction and trace data flow before a single-variable change.
- Two or more failed fixes: per `SKILL.md` Phase 4 (“3+ fixes failed”) and Red Flags, stop stacking guesses—escalate to architecture and root-cause review instead of a blind next patch.

## Repository layout (contributors)

| Path | Role |
|------|------|
| `SKILL.md` | Entire skill: phases, red-flag table, quick reference—edit behavior here. |
| `LICENSE` | License text. |
| `SECURITY.md` | Security policy and reporting. |
| `CODE_OF_CONDUCT.md` | Community code of conduct. |
