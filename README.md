# systematic-debugging

A structured 5-phase debugging methodology for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Root cause first, fixes second.

## Why

Claude Code is great at writing code, but when it hits a bug, the default behavior is often "try random fixes until something works." This skill forces a systematic approach:

1. **Phase 0: Memory Recall** — Check if you've seen this before
2. **Phase 1: Root Cause Investigation** — Read errors, reproduce, trace data flow
3. **Phase 2: Pattern Analysis** — Find working examples, compare differences
4. **Phase 3: Hypothesis Testing** — One variable at a time, scientific method
5. **Phase 4: Implementation** — Failing test first, then single fix

The iron law: **no fixes without root cause investigation first.**

## Install

```bash
# Clone into your Claude Code skills directory
git clone https://github.com/runesleo/systematic-debugging-skill ~/.claude/skills/systematic-debugging
```

Or manually copy `SKILL.md` to `~/.claude/skills/systematic-debugging/SKILL.md`.

## Usage

The skill triggers automatically when Claude Code encounters errors. You can also invoke it manually:

```
/debug
```

Or reference it in your `CLAUDE.md`:

```markdown
When encountering bugs, use the systematic-debugging skill before attempting fixes.
```

## The Core Idea

Most debugging time is wasted on:
- Guessing without evidence
- Fixing symptoms instead of root causes
- Trying multiple changes at once
- Skipping reproduction steps

This skill enforces discipline:

| Metric | Systematic | Random Fixes |
|--------|-----------|--------------|
| Time to fix | 15-30 min | 2-3 hours |
| First-time fix rate | ~95% | ~40% |
| New bugs introduced | Near zero | Common |

## Red Flags

If Claude starts saying things like:
- "Quick fix for now, investigate later"
- "Just try changing X and see"
- "I don't fully understand but this might work"

...the skill catches these and redirects to Phase 1.

## Customization

The skill is a single Markdown file. Customize it by:
- Adding project-specific debugging patterns
- Integrating with your memory/knowledge base in Phase 0
- Adding domain-specific red flags

## License

MIT

## Author

[@runes_leo](https://x.com/runes_leo) — Building AI x Crypto tools. Using Claude Code daily for prediction market strategies.
