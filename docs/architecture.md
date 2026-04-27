# systematic-debugging-skill — Architecture

This repository is a **single-artifact Claude Code Skill**: almost all behavior lives in **`SKILL.md`** (frontmatter + Markdown body). There is no runtime server, package entrypoint, or plugin binary.

## Artifact model

| File | Role |
|------|------|
| `SKILL.md` | Source of truth: phases, gates, violations, quick reference |
| `LICENSE` | Legal terms (MIT lineage noted in frontmatter attribution) |
| `README.md` | Human-oriented onboarding, clone paths, when to use / not use |

Consumers are **Claude Code** (or compatible agents) that load `SKILL.md` into context when `when_to_use` matches.

## Frontmatter contract

YAML frontmatter fields (see file for exact values):

- **`name`**: Display name for the skill.
- **`description`**: Short summary for routing.
- **`when_to_use`**: Trigger phrase for the agent router.
- **`version`**: Semantic-ish version for humans diffing updates.
- **`languages`**: Declared applicability (`all`).
- **`attribution`**: Credit to upstream superpowers lineage.

Changing frontmatter affects **discovery** — treat it like a public API.

## Process architecture: five phases

The body enforces a **strict partial order**:

1. **Phase 0 — Context Recall**  
   Mandatory first step: extract error keywords, search memory/docs/git history, emit structured “Context Recall” block.  
   **Violation:** entering Phase 1 without Phase 0 output.

2. **Phase 1 — Root Cause Investigation**  
   Reproduce, read stack traces, inspect recent changes, add **boundary instrumentation** in multi-component systems, trace data flow to source.

3. **Phase 2 — Pattern Analysis**  
   Compare broken vs working code, list differences without dismissing “small” deltas.

4. **Phase 3 — Hypothesis and Testing**  
   Single hypothesis, minimal experiment, explicit “don’t know” path.

5. **Phase 4 — Implementation**  
   Failing test first, **one** fix, verify; **3+ failed fixes** triggers architectural escalation per SKILL text.

## Gating mechanism

Gates are **social/process** (Markdown instructions), not compiled checks. Effectiveness depends on the host agent **honoring** “NO FIXES WITHOUT ROOT CAUSE” and phase ordering.

## Iron Law

Two stacked rules appear early:

- No fixes before root-cause investigation.
- No investigation before context recall.

Everything else hangs off this sequencing.

## Extensibility

- **Additive sections** in `SKILL.md` (new anti-patterns, new checklists) are the normal extension path.
- **Forks** can narrow `when_to_use` for domain-specific stacks while keeping phase skeleton.

## Non-architecture

- No `package.json`, no Python `src/` — deployment is **copy or git clone** into `~/.claude/skills/...`.
