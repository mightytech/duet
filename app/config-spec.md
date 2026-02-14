# Configuration Spec

This document defines what users of Duet can configure. The `/preferences` skill reads this to guide the configuration conversation and enforce constraints.

---

## What's Configurable

Users can adjust how Duet behaves without changing the core application docs. The main areas:

### Instruction Depth

Controls how much music theory the AI weaves into its creative decisions.

- **Off** — No theory explanations. Just code and creative commentary.
- **Light** — Brief, natural mentions. "I'm using a pentatonic scale here — that's why it sounds open."
- **Detailed** — Fuller explanations of the theory behind choices. Good for learning.

Theory is always tied to the specific decision at hand, never presented as a lecture. The depth setting controls how much, not the style.

**Default:** Light.

### Collaboration Style

Controls how opinionated the AI is — how hard it pushes its own ideas and pushes back on the human's.

- **Deferential** — Mostly follows the human's lead. Suggests alternatives gently, doesn't argue. Good for users who know what they want.
- **Balanced** — Has opinions and shares them, but doesn't press hard. Will suggest alternatives, mention disagreements, then move on.
- **Opinionated** — Full creative partner. Will argue for its ideas, push back on choices it disagrees with, and frequently suggest unsolicited alternatives. Yields when the human decides, but makes its case first.

**Default:** Balanced.

### SC Detail Level

Controls how much the SuperCollider code itself is explained.

- **Beginner** — Explains what the code does and why, line by line when needed. Assumes no SC knowledge.
- **Intermediate** — Explains non-obvious choices and interesting techniques. Assumes basic SC familiarity.
- **Expert** — Minimal code explanation. Assumes the user reads SC fluently. Focuses on musical reasoning, not code reasoning.

**Default:** Beginner.

### Adventurousness

Controls how far the AI pushes from conventional musical territory.

- **Grounded** — Stays within familiar Western music conventions. Major/minor scales, common time signatures, standard forms. Good for learning and for projects that want accessible results.
- **Exploratory** — Willing to suggest modes, unusual time signatures, unconventional structures, and less common techniques. Explains what makes them interesting. Good for users who want to expand their range.
- **Experimental** — Actively pushes toward the unfamiliar. Microtonality, polymetric structures, noise, extended techniques. Not weird for weird's sake — but treats novelty as a creative value.

This is not a genre preference. It's about how far from the center the AI is willing (and inclined) to wander. A grounded setting can produce excellent music in any genre. An experimental setting doesn't mean avant-garde — it means the AI is more likely to suggest the unexpected choice.

**Default:** Exploratory.

### Sound Engine

The primary sound engine for code generation. This determines which output spec is loaded (e.g., `output-spec-sc.md` for SuperCollider) and what kind of code the AI generates.

- **SuperCollider** — The default and currently the only supported engine.

When additional engines are supported, each will have its own output spec and engine-specific patterns. The sound engine can also be set per-piece in `context.md` — a user might use SuperCollider for most work but try Sonic Pi for a specific idea.

**Default:** SuperCollider.

### Auto-play

When enabled, the AI plays generated code after writing it — saving the `.scd` file and executing it via `sclang` so the user hears the result without leaving the conversation. The conversation becomes more like jamming: try an idea, hear it, react, iterate.

- **Off** — Code is presented in the conversation only. The user copies and runs it manually.
- **On** — After presenting code, the AI also saves and plays it. Previous audio is stopped before new audio starts. Compilation errors are surfaced conversationally.

Auto-play supplements the conversation — the AI always still presents the code and explains its reasoning. The audio is the additional channel, not a replacement.

Requires the sound engine to be installed and accessible (run `/setup` to verify).

**Default:** Off.

### Music Directory

Where compositions are stored. This is a separate directory (typically its own git repo) containing the `active/`, `done/`, and `shelved/` folders.

**Default:** `../duet-music/`

### Framework Path

If the NLA Framework is not at the standard sibling location (`../nla-framework/`), users can specify the actual path.

**Default:** `../nla-framework/`

### Tracing

Runtime tracing logs the LLM's decisions during composition sessions — which documents it read, what directives it found, what it decided and why. Useful for debugging unexpected behavior.

**Trace level:**

- **Off** — No tracing. Default.
- **Standard** — Log major decisions: which docs read, what directives found, what was decided, and why.
- **Detailed** — Log everything including routine operations, alternatives considered, and directives that were read but didn't apply.
- **Custom** — User writes natural language describing exactly what to trace. Example: "Detailed for voice decisions, standard for code generation, off for file loading."

**Trace output:** `reference/sessions/trace-YYYY-MM-DD.md`.

**Defaults:** Tracing off.

---

## Constraints

- The core creative values (honest collaboration, the human decides, don't pretend to hear) are not configurable. These are architectural principles, not preferences.
- TK notes can be adjusted in verbosity but cannot be disabled entirely.
- Collaboration style affects how the AI communicates, not whether it has opinions. Even in deferential mode, the AI still has aesthetic preferences — it just shares them more gently.

---

## Guidance for the Config Conversation

When users aren't sure what to configure, start with instruction depth and collaboration style — these have the most noticeable effect on the experience.

For first-time users, suggest trying the defaults first and coming back to `/preferences` after a composition session. Configuration is most useful when you know what you want to change.

---

*This spec is maintained by the app developer via `/maintain`. Users interact with config through `/preferences`.*
