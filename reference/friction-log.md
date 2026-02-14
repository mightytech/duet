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

## 2026-02-14 — Selectable voices and natural language config

**Type:** process
**Severity:** major
**Task:** all tasks
**Status:** pending

**Observation:**
The AI's creative identity (voice-and-values.md) is currently a single fixed voice — the Lennon & McCartney creative partner. Users should be able to choose among voices (creative partner, music educator, production coach, etc.) or describe a custom one. More importantly, because NLA config is prose interpreted by an LLM, users aren't limited to enum choices. They can say "creative partner, but lean into teaching when I'm clearly lost" or "music educator who assumes I know jazz theory but not classical." This applies to all config settings, not just voice.

**Confirmed reason:**
User identified: "the power of an NLA — you can make big changes without huge changes in code." And on config: "users can say 'option a, but...' or 'option c, and...' This is powerful. It means they can modify application behavior in meaningful ways without rewriting the application... they're baked in features of NLAs and LLMs."

**Generalizable:** yes — both the voice pattern and the natural language config insight apply to any NLA

**Affected documentation:**
- `app/shared/voice-and-values.md` — Split into invariant values + selectable voice files
- `app/config-spec.md` — Add Voice setting; broaden all config guidance to embrace natural language modifiers
- `app/shared/voices/` — New directory for base voice files
- New: voice template for users writing custom voices
- All task doc prerequisites — "read voice-and-values.md" becomes "read values.md + configured voice"
- Framework: `core/nla-foundations.md` or config guidance should discuss natural language config as a fundamental NLA capability

**Proposed fix:**
1. Split `voice-and-values.md` into `values.md` (invariant: can't hear music, human decides, honesty) and voice files in `voices/` directory.
2. Ship 2-3 well-crafted base voices. Quality over quantity — each needs iteration.
3. Voice config setting: a voice name (loads the file), a voice name with natural language modifications, or a fully custom description.
4. Voice template for custom voices: what to include (identity, communication style, priorities, approach to disagreement), what principles are non-negotiable (the values).
5. Broaden config-spec guidance: enums are convenient defaults, natural language is the real interface. Every setting can accept "X, but..." or "X, and..." modifiers.
6. File the natural language config insight as framework feedback — it's a fundamental NLA capability the framework should discuss.

**Notes:**
This is an architectural change that deserves its own /maintain session. The voice split affects all task doc prerequisites (similar scope to the output-spec rename). The natural language config insight is framework-level and should be added to the framework feedback letter.

---

## Patterns to Watch

*Recurring themes that may need deeper attention:*

1. **SuperCollider code correctness** — Does the generated code compile and run? Track patterns in SC errors to improve code generation guidance.

2. **Theory-to-sound accuracy** — When the AI predicts how something will sound based on theory, how often does the human agree? Track mismatches to calibrate confidence.

3. **Feedback translation** — When humans give impressionistic feedback ("too busy," "needs warmth"), how accurately does the AI translate that into musical changes? Track cases where the translation misses.

4. **Collaboration balance** — Is the AI being too passive or too pushy? Track human reactions to pushback and unsolicited suggestions.

---

*This log is maintained by the `/friction-log` skill (which creates entries from any context) and the `/maintain` skill (which resolves and archives them). Resolved entries are moved to `friction-log-archive.md`.*
