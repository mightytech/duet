# Friction Log

Running log of learnings from Duet operation and human feedback. Each entry captures something worth remembering — problems, surprises, or things that worked well.

---

## How to Use This Log

**When to add entries:**
- After observing a correction or gap
- When you notice a pattern across multiple compositions
- When something works surprisingly well
- When something fails unexpectedly

**Entry types:**
- `output` — How the NLA generated code or commentary
- `process` — How the composition workflow functioned
- `documentation` — Clarity or gaps in the docs

**Severity includes positive:** Capture what works, not just what breaks.

---

## Entry Format

```markdown
## [DATE] — [CONTENT or CONTEXT]

**Type:** output | process | documentation
**Severity:** positive | minor | major
**Task:** [which task]
**Status:** pending | resolved | deferred | wont-fix

**Observation:**
[What happened or was noticed]

**Before:** [What the NLA produced]
**After:** [What the human wanted]

**Confirmed reason:**
[The human's explanation — their words, not a summary]

**Generalizable:** [yes | no | partially]
[Under what conditions does this apply?]

**Affected documentation:**
[Which app/ file and section would need to change]

**Proposed fix:**
[Specific enough for /maintain to act on]

**Notes:**
[Additional context, related entries, patterns noticed]
```

Not every entry needs all fields. The essentials are: Observation, Type, Severity, Status. The Before/After, Confirmed reason, and other fields are valuable when you have them — richer entries are more useful to `/maintain`. Include what you have; don't force what you don't.

**When `/maintain` resolves an entry**, it updates the Status field:
```markdown
**Status:** resolved
**Resolved:** [DATE] — [brief description of what was changed and where]
```

---

## Entries

*Entries are added chronologically, newest first.*

---

## Patterns to Watch

*Recurring themes that may need deeper attention:*

1. **SuperCollider code correctness** — Does the generated code compile and run? Track patterns in SC errors to improve code generation guidance.

2. **Theory-to-sound accuracy** — When the AI predicts how something will sound based on theory, how often does the human agree? Track mismatches to calibrate confidence.

3. **Feedback translation** — When humans give impressionistic feedback ("too busy," "needs warmth"), how accurately does the AI translate that into musical changes? Track cases where the translation misses.

4. **Collaboration balance** — Is the AI being too passive or too pushy? Track human reactions to pushback and unsolicited suggestions.

---

*This log is maintained by the `/friction-log` skill (which creates entries from any context) and the `/maintain` skill (which resolves and archives them). Resolved entries are moved to `friction-log-archive.md`.*
