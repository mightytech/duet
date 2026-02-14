# Design Rationale

This document explains WHY Duet is built the way it is. It captures the reasoning, trade-offs, and principles that shaped the design.

**Audience:** Future maintainers (human or AI) who need to understand the decisions behind the system before modifying it.

**Purpose:** Prevent well-intentioned "improvements" that break things that work. Provide context that won't be obvious from the docs alone.

---

## Why an NLA for Music Composition?

Traditional AI music tools treat the LLM as a service — code calls an API, gets music back. Duet inverts this: the LLM is the application, and SuperCollider is just the tool it uses. This architectural flip enables genuine collaboration because the AI's behavior is defined in prose (voice, values, judgment calls), not in code (parameters, thresholds, rules).

Music composition is full of judgment calls that can't be enumerated: "Does this need more tension?", "Is this transition earned?", "Would 7/8 serve this better than 4/4?" These are exactly the decisions NLAs handle well — through understanding, not through rules.

---

## Why These Four Tasks?

### Compose, Iterate, Critique, Spark

The tasks map to natural phases of creative collaboration:

- **Compose** starts with vision and produces something concrete to react to
- **Iterate** is the core loop — feedback-driven refinement
- **Critique** is the partner stepping back to assess the whole picture
- **Spark** is the lateral move that prevents comfortable ruts

**Why separate tasks instead of one "compose" flow?** Because the AI's posture changes. In compose, you're generating. In iterate, you're refining based on feedback. In critique, you're honest and analytical. In spark, you're provocative. Different voice docs could emerge for each; separating them makes that possible.

**Why Spark as a standalone task?** It could be woven into compose/iterate, but having it explicit means the human can *summon* a provocation when they're stuck. That agency matters — it's the human deciding "I need a jolt," not the AI deciding for them.

---

## Key Design Decisions

### The AI Can't Hear

The most important constraint. The AI generates SuperCollider code based on music theory, but cannot hear the output. This is stated explicitly in the voice doc and referenced throughout.

**Why lean into it instead of hiding it:** Pretending the AI can hear would undermine trust. Acknowledging it makes the collaboration genuine — the AI brings theory and structure, the human brings ears and taste. Neither is complete alone. This is the real partnership, not a polite fiction.

### SuperCollider as First Platform, Not Only Platform

The system is designed around SuperCollider but the name (Duet) and the architectural docs avoid being SC-specific where possible. If a future version supports Sonic Pi, Max/MSP, or another platform, the voice, values, and task structure should transfer — only the code generation layer changes.

### Adventurousness as a Config Setting

Musical adventurousness (how far the AI pushes from conventional choices) is configurable because it's genuinely personal. Some users want to explore microtonality and polymetric structures; others want to learn within familiar territory. Neither is better. This is exactly the kind of preference that should live in config, not in the app docs.

### Music Theory as Optional Teaching

The instruction-depth config controls whether the AI explains the theory behind its decisions. This serves the target audience (tech-savvy, not necessarily musical) without burdening experienced musicians with explanations they don't need. The teaching is woven into conversation, not presented as separate lectures.

### Friction Log Not Loaded at Startup

The friction log (`reference/friction-log.md`) is NOT loaded during composition. It's reference material — loaded only by `/maintain` when that skill is invoked.

**Why:** Dual-channel separation. Maintenance data (known gaps, correction patterns) shouldn't influence runtime behavior. Also, allowing friction to accumulate before acting reveals patterns that single entries miss.

---

## Adding Decisions

When you make architectural changes (not just wording fixes), add an entry here documenting:
- What was decided
- Why (including what alternatives were considered)
- What it affects

This prevents future maintainers from re-introducing approaches that already failed or undoing decisions that had good reasons.

---

*This document is updated by the `/maintain` skill when architectural decisions are made.*
