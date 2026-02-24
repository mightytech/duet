# Friction Log Archive

Resolved and closed friction log entries, moved here from `friction-log.md` during `/maintain` sessions. This keeps the active friction log lean while preserving history for pattern analysis.

**How entries get here:** When `/maintain` resolves a friction log entry, it moves the complete entry (including the `**Resolved:**` line) from the active log to this archive.

**Searching:** Use grep to search this archive when looking for historical patterns. The `/friction-log` skill searches here automatically before creating new entries.

---

## Entries

*Archived entries in reverse chronological order.*

---

## 2026-02-14 — Selectable voices and natural language config

**Type:** process
**Severity:** major
**Task:** all tasks
**Status:** resolved
**Resolved:** 2026-02-23 — Framework update implemented the voice/values split. Split voice-and-values.md into values.md (startup infrastructure) and voice.md (task-level shared context). Updated all task doc prerequisites, startup, CLAUDE.md, overview.md, README.md. The broader "selectable voices" and "natural language config" aspects remain as future capabilities enabled by the split — the architecture now supports multiple voice files and the config-spec already embraces NL modifiers.

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

## 2026-02-13 — Auto-play: execute SC code directly from the conversation

**Type:** process
**Severity:** major
**Task:** compose / iterate
**Status:** resolved
**Resolved:** 2026-02-14 — Added Auto-play config option (off/on, default off). Added Playing Audio section to common-patterns.md. Integrated auto-play into compose.md and iterate.md. /setup skill (created separately) verifies sclang is accessible.

**Observation:**
The current workflow requires the user to copy generated SC code, switch to SuperCollider, paste, and execute. This breaks creative flow. The AI has access to `sclang` (SC's command-line interpreter) and could run .scd files directly, making the conversation feel like jamming rather than code handoff.

**Confirmed reason:**
User proposed: "Could be nice... Try X / OK, how about this? (writes code; opens SC and/or plays file)." The goal is removing mechanical friction between creative idea and hearing it.

**Generalizable:** yes — any user with SC installed locally benefits

**Notes:**
Implemented as behavioral documentation rather than coded integration. The docs describe what the AI should do (stop previous audio, play in background, surface errors conversationally); the AI handles the shell-level mechanics at runtime. This is a clean example of the NLA advantage — a traditional app would need a coded SC integration layer, while the NLA just uses its existing tool access.

---

## 2026-02-13 — Setup skill and requirements system

**Type:** process
**Severity:** major
**Task:** compose (first session)
**Status:** resolved
**Resolved:** 2026-02-14 — Created /setup skill with environment.md caching. Added Sound Engine to config-spec. Renamed output-spec.md to output-spec-sc.md for engine-specific specs. Added environment check to /startup.

**Observation:**
Pieces may require specific software, extensions, or configurations (e.g., sc3-plugins for DWGBowed). No way to track what's needed or what's installed. The NLA can handle cross-platform installation naturally without coded platform detection.

**Confirmed reason:**
User identified: "you're actually completely capable of doing the setup for the user... one of the nice things about an NLA is that we actually don't have to code this sort of functionality for different platforms." Also noted that the sound engine itself (SuperCollider) shouldn't be hard-wired — other users might use different software.

**Generalizable:** yes

**Notes:**
Implemented with engine-specific output specs (output-spec-sc.md rather than generic output-spec.md) per user suggestion — avoids premature abstraction while providing a clear path for adding engines. Each engine gets its own tailored spec. Environment.md caches platform detection at the music directory root so /startup doesn't re-detect every session.

---

## 2026-02-14 — Iteration snapshots: versioned playable history

**Type:** process
**Severity:** minor
**Task:** iterate
**Status:** resolved
**Resolved:** 2026-02-14 — Implemented as `/snapshot` skill. Snapshots freeze code + context.md into iterations/ subfolder with a freeform name and a note. Part of the unified lifecycle pattern (snapshot/shelve/finish/resume).

**Observation:**
The `iterations/` folder exists in piece folders but has no defined convention yet. The concept: snapshots that freeze both the code and the context.md at a point in time, like git tags but always-present — so you can play any version side by side without mucking around at the repo level. Each snapshot would include the .scd file and a copy of context.md as it was at that moment, so you know what was (and wasn't) done when the music was captured.

**Generalizable:** yes

**Notes:**
Originally filed as a "needs to develop through use" entry during the music directory maintenance session. The user observed that snapshots are just another variant of the same "capture state with a note" pattern used by /shelve and /finish — the only difference is where the files go and whether the piece stays active. This insight led to implementing /snapshot alongside the other lifecycle skills rather than deferring it.

---

## 2026-02-13 — Composition lifecycle and workflow skills

**Type:** process
**Severity:** major
**Task:** compose (first session)
**Status:** resolved
**Resolved:** 2026-02-14 — Created /snapshot, /shelve, /finish, /resume skills. Expanded /startup with piece awareness. Added forking convention and lifecycle table to common-patterns.md. Updated skills tables in overview.md and CLAUDE.md.

**Observation:**
The system needs awareness of active compositions at startup and deliberate lifecycle transitions. Currently /startup loads system context but doesn't know what the user has been working on. There's no way to shelve, finish, resume, or fork a composition.

**Confirmed reason:**
User identified: session startup should show active pieces and let the user pick one. Lifecycle transitions should be deliberate moments that capture context — "the real value is prompting the user for notes at the moment they're most likely to have insight and least likely to write it down voluntarily."

**Generalizable:** yes

**Notes:**
Implemented as a unified lifecycle pattern: every transition (snapshot, shelve, finish) prompts for a note and freezes state. The core operation is the same — only the destination and whether the piece stays active differ. Forking handled as a conversational pattern during /iterate rather than a separate skill.

---

## 2026-02-13 — Music directory structure and composition persistence

**Type:** process
**Severity:** major
**Task:** compose (first session)
**Status:** resolved
**Resolved:** 2026-02-14 — Codified music directory conventions across config-spec.md, compose.md, iterate.md, overview.md, common-patterns.md. Created context-template.md. Iteration snapshots filed as separate pending entry for future development.

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
