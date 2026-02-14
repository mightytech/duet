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

## 2026-02-13 — Auto-play: execute SC code directly from the conversation

**Type:** process
**Severity:** major
**Task:** compose / iterate
**Status:** pending

**Observation:**
The current workflow requires the user to copy generated SC code, switch to SuperCollider, paste, and execute. This breaks creative flow. The AI has access to `sclang` (SC's command-line interpreter) and could run .scd files directly, making the conversation feel like jamming rather than code handoff.

**Confirmed reason:**
User proposed: "Could be nice... Try X / OK, how about this? (writes code; opens SC and/or plays file)." The goal is removing mechanical friction between creative idea and hearing it.

**Generalizable:** yes — any user with SC installed locally benefits

**Affected documentation:**
- `app/config-spec.md` — add auto-play as a configurable option
- `app/common-patterns.md` — document the play workflow
- `app/iterate.md` — integrate auto-play into the iterate loop
- New: `/setup` skill should verify sclang is accessible

**Proposed fix:**
1. Add config option: `Auto-play: off | on` (default off). When on, the AI executes .scd files via sclang after writing them.
2. Implementation considerations:
   - Stop previous audio before playing new audio (send `s.freeAll` or equivalent)
   - Keep scsynth server running between iterations (avoid boot time on every play)
   - Surface sclang compilation errors conversationally — don't dump raw output
   - Run sclang in background so the conversation isn't blocked
   - Could also support opening files in the SC IDE as an alternative to headless play
3. The AI should always still present the code and commentary — auto-play supplements the conversation, doesn't replace it.
4. Worth exploring: could the AI detect when audio is playing and prompt for feedback after a reasonable listening period?

**Notes:**
This is a significant UX improvement that leverages the NLA's ability to use tools. A traditional app would need to build an SC integration layer. The NLA just runs a shell command. The /setup skill should verify sclang is on the PATH as part of environment checking.

---

## 2026-02-13 — Composition lifecycle and workflow skills

**Type:** process
**Severity:** major
**Task:** compose (first session)
**Status:** pending

**Observation:**
The system needs awareness of active compositions at startup and deliberate lifecycle transitions. Currently /startup loads system context but doesn't know what the user has been working on. There's no way to shelve, finish, resume, or fork a composition.

**Confirmed reason:**
User identified: session startup should show active pieces and let the user pick one. Lifecycle transitions should be deliberate moments that capture context — "the real value is prompting the user for notes at the moment they're most likely to have insight and least likely to write it down voluntarily."

**Generalizable:** yes

**Affected documentation:**
- `app/overview.md` — add lifecycle skills to skill table
- `.claude/skills/` — new skills: /shelve, /finish, /resume
- Startup skill needs update to scan active pieces

**Proposed fix:**
1. Enhanced /startup: after loading system context, read the music directory's `active/` folder. If 1-4 active pieces, use AskUserQuestion to let user pick which to continue (or start new). If more, list them.
2. `/shelve` skill: prompts for a note (why shelving, what state), updates context.md, moves folder from active/ to shelved/.
3. `/finish` skill: captures final notes and lessons learned, moves to done/.
4. `/resume` skill: moves piece from shelved/ back to active/, reads context.md, picks up collaboration.
5. Forking: when user wants to try a different direction, copy the piece folder with a new name. Could be part of /iterate or triggered by natural language ("let's fork this").

---

## 2026-02-13 — Setup skill and requirements system

**Type:** process
**Severity:** major
**Task:** compose (first session)
**Status:** pending

**Observation:**
Pieces may require specific software, extensions, or configurations (e.g., sc3-plugins for DWGBowed). No way to track what's needed or what's installed. The NLA can handle cross-platform installation naturally without coded platform detection.

**Confirmed reason:**
User identified: "you're actually completely capable of doing the setup for the user... one of the nice things about an NLA is that we actually don't have to code this sort of functionality for different platforms." Also noted that the sound engine itself (SuperCollider) shouldn't be hard-wired — other users might use different software.

**Generalizable:** yes

**Affected documentation:**
- `app/config-spec.md` — add sound engine as configurable setting
- New: `/setup` skill
- New: environment.md spec (music directory root)

**Proposed fix:**
1. `/setup` skill: reads piece-level `requirements.md`, reads `environment.md` (music dir root) to see what's installed, identifies gaps, installs with user confirmation, updates environment.md.
2. `environment.md` at music directory root, AI-maintained: records platform, sound engine, installed extensions.
3. Piece-level `requirements.md`: human-readable, AI-actionable. "Requires sc3-plugins (for DWGBowed)."
4. Sound engine should be a config setting, not hard-wired. Output spec and common patterns should eventually support other engines.
5. User platform preference in config.md or auto-detected. Always confirm before installing.

---

## 2026-02-13 — Music directory structure and composition persistence

**Type:** process
**Severity:** major
**Task:** compose (first session)
**Status:** pending

**Observation:**
First composition session revealed no structure for saving compositions. The system needs a standard way to organize music files, persist creative context across sessions, and track iteration history. Context persistence is especially important for NLA workflows — the AI needs to understand not just what was composed but why, and what was rejected.

**Confirmed reason:**
User identified: "documenting intent and the whys is just as important — or even more important, especially when it comes time to iterate. If a new session is started without any context we want to be able to pick up where we left off."

**Generalizable:** yes

**Affected documentation:**
- `app/overview.md` — document music directory convention
- `app/compose.md` — add step for saving output and drafting context.md
- `app/iterate.md` — add step for reading/updating context.md
- `app/config-spec.md` — add music directory path setting
- New: `app/templates/context-template.md`

**Proposed fix:**
1. Standard music directory structure (sibling to app, separate git repo):
   - `active/` — pieces in progress, each in its own folder
   - `done/` — finished work
   - `shelved/` — parked ideas (not "archived" — implies possible return)
   - Each piece folder: sketch.scd, context.md, requirements.md, iterations/
2. `context.md` template with sections: Concept, Sound Engine, Decisions (with reasoning), Rejected (with reasoning), References, Listening Notes, Unresolved, Iteration History.
3. Music directory path configurable in config-spec.md (default: ../duet-music/).
4. No persistent index file — AI reads folders and context.md files on demand. Index generated on request, not maintained.
5. Piece folders use freeform names for memorability.
6. AI drafts context.md, human reviews. Distillation of conversation, not transcript.
7. The iterate contract: update context.md before updating code — intent first, implementation second.

---

## Patterns to Watch

*Recurring themes that may need deeper attention:*

1. **SuperCollider code correctness** — Does the generated code compile and run? Track patterns in SC errors to improve code generation guidance.

2. **Theory-to-sound accuracy** — When the AI predicts how something will sound based on theory, how often does the human agree? Track mismatches to calibrate confidence.

3. **Feedback translation** — When humans give impressionistic feedback ("too busy," "needs warmth"), how accurately does the AI translate that into musical changes? Track cases where the translation misses.

4. **Collaboration balance** — Is the AI being too passive or too pushy? Track human reactions to pushback and unsolicited suggestions.

---

*This log is maintained by the `/friction-log` skill (which creates entries from any context) and the `/maintain` skill (which resolves and archives them). Resolved entries are moved to `friction-log-archive.md`.*
