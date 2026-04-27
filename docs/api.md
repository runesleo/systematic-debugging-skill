# systematic-debugging-skill — “API” (machine / agent contract)

This skill has **no HTTP or library API**. The contract is how **host tools** load and apply **`SKILL.md`**.

---

## Discovery interface (frontmatter)

Agents that support Claude-style skills typically read:

| Field | Consumer use |
|--------|----------------|
| `name` | UI / catalog label |
| `description` | Short listing text |
| `when_to_use` | Router: when to attach this skill to a session |
| `version` | Cache busting, diffing |
| `languages` | Optional filter |

**Behavioral contract:** If `when_to_use` matches (bugs, test failures, unexpected behavior, etc.), the agent should load the **full body** before proposing code edits.

---

## Phase protocol (behavioral API)

Each phase exposes **inputs** (what the agent must have) and **outputs** (what it must emit):

### Phase 0 — Context Recall

**Input:** Error text / symptom description.  
**Output:** Structured block:

```
Context Recall:
- Query: "..."
- Found: ...
- Action: ...
```

**Failure mode:** Proceeding to investigation without this block = process violation.

### Phase 1 — Root Cause Investigation

**Input:** Phase 0 complete.  
**Output:** Reproduction steps, evidence (logs, stack), boundary instrumentation plan for multi-component systems.

### Phase 2 — Pattern Analysis

**Input:** Phase 1 evidence.  
**Output:** Enumerated differences between working and broken paths.

### Phase 3 — Hypothesis and Testing

**Input:** Phase 2 comparison.  
**Output:** Single explicit hypothesis + minimal experiment result.

### Phase 4 — Implementation

**Input:** Confirmed hypothesis.  
**Output:** Failing test/repro, one fix, verification; or stop after 3 failed attempts for architecture review.

---

## Extension points for integrators

- **CLAUDE.md hook:** Projects can mandate “on error, follow `SKILL.md` phases” — document that in repo `CLAUDE.md`, not in this package.
- **CI bots:** May map Phase 1 “reproduce” to artifact URLs; keep secrets out of skill text.

---

## Compatibility

- **Markdown + YAML frontmatter** — parsers must tolerate `---` delimiters.
- No code execution implied; safe to vend as read-only file.

---

## Version negotiation

Consumers should treat **`version` frontmatter** as informational; there is no semver range negotiation. Pin by **git SHA** for reproducible audits.

---

## Error codes

None — failures are **process violations** described in prose (e.g. skipping phases, multiple simultaneous fixes).

---

## Example: host pseudo-code

```text
on_user_message(session):
  if matches_when_to_use(SKILL.frontmatter.when_to_use):
    inject(SKILL.body)
    enforce_gates(PHASE_ORDER)
```

Real hosts (Claude Code) use richer routing; this illustrates the intended attachment semantics.
