# System Overview

This document describes what Duet does and how its pieces fit together. For what NLAs are and the principles behind them, see [nla-foundations.md](../nla-framework/core/nla-foundations.md).

---

## What This NLA Does

Duet is a collaborative music composition system. A human and an AI work together to create music using SuperCollider as the sound engine. The AI is a creative partner — opinionated, knowledgeable, honest — not a tool that generates music on command.

The conceptual flip: instead of traditional code calling an LLM through an API, the LLM is the application, orchestrating traditional tools (SuperCollider) while providing a human-centered creative interface.

| Task | Purpose | Trigger |
|------|---------|---------|
| **Compose** | Start a composition from a concept or mood | User has an idea to explore |
| **Iterate** | Refine the composition through feedback | User has listened and has a reaction |
| **Critique** | AI evaluates the composition and offers perspective | User wants honest assessment |
| **Spark** | Contextual creative provocation | User is stuck or wants lateral input |

### Compose

The starting point. Takes a creative prompt — a mood, a concept, a reference — and generates an initial SuperCollider sketch. The goal isn't a finished piece; it's something to *react to*.

**Source:** `compose.md`

### Iterate

The core loop. The human plays the code, listens, and reacts. The AI translates that reaction into musical changes, explains its reasoning, and presents the next version. This is where most of the creative work happens.

**Source:** `iterate.md`

### Critique

The AI steps back and evaluates the whole picture — harmonic content, rhythmic structure, form, timbre. Like a composition teacher reading a score: analytical, specific, honest. Acknowledges what it can't know (it can't hear the output).

**Source:** `critique.md`

### Spark

A creative provocation tailored to where the composition is right now. Inspired by Eno's Oblique Strategies, but contextual — it pushes against the specific situation, not at random.

**Source:** `spark.md`

### How It Connects

```
                    ┌─────────────────┐
                    │  Shared Context │
                    │  - Values/Voice │
                    │  - Patterns     │
                    │  - Output Spec  │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
        ┌──────────┐  ┌──────────┐  ┌──────────┐
        │ Compose  │  │ Critique │  │  Spark   │
        └────┬─────┘  └──────────┘  └──────────┘
             │
             ▼
        ┌──────────┐
        │ Iterate  │◄──── feedback loop
        └──┬───────┘
           │
           ▼
        ┌──────────┐
        │  Music   │
        └──────────┘
```

All tasks read shared context (voice, patterns, output spec). Compose starts the piece, Iterate refines it in a loop, Critique and Spark can intervene at any point. The human is always the listener and final decision-maker.

### Invocation via Skills

Each task has an explicit entry point — a Claude Code skill:

| Skill | Purpose |
|-------|---------|
| `/startup` | Load foundational context and check active pieces |
| `/compose` | Start a new composition from a concept or mood |
| `/iterate` | Refine the composition based on listening feedback |
| `/critique` | Get an honest assessment of the current composition |
| `/spark` | Get a contextual creative provocation |
| `/snapshot` | Save a versioned snapshot of the current piece |
| `/shelve` | Park the current piece for later |
| `/finish` | Mark a piece as done and capture reflections |
| `/resume` | Bring a shelved piece back to active work |
| `/setup` | Check environment and install what's needed |
| `/preferences` | Create or edit user configuration |
| `/friction-log` | Log observations to the friction log from any context |
| `/maintain` | Edit the NLA system itself |
| `/validate` | Check system consistency, trace scenarios, debug behavior |
| `/think` | Collaborative design exploration before planning |
| `/debrief` | Reflect on completed work while context is fresh |
| `/install` | Install a new NLA package |
| `/update` | Update the NLA — pull remote changes, apply package intent updates |
| `/check-updates` | Check for available updates without making changes |
| `/export` | Export as a plugin for Claude Code or Cowork |

Skills live in `.claude/skills/` and load their context on demand — `CLAUDE.md` provides the runtime identity, and each skill pulls in the specific docs it needs. `/startup` can also be re-run mid-session to reload foundational context after a long conversation.

### The Improvement Pipeline

The system improves through the friction log:

```
Observation from any context → /friction-log captures it → Friction Log → /maintain implements
```

`/friction-log` captures observations from any context — during composition, critique, or casual conversation. Entries accumulate in the friction log, where patterns emerge over time. `/maintain` processes them into doc changes. Resolved entries are archived to `friction-log-archive.md`.

This separation exists because capturing observations and editing system docs are different tasks with different guardrails. The friction log is the handoff contract between them.

---

## For Humans

**To change AI behavior:**
- Identify which document governs that behavior
- Edit the document
- The change takes effect immediately (next run)

**To debug unexpected output:**
- Check which documents the AI read
- Look for ambiguity or missing guidance
- Add clarification or examples

**To add a new task:**
1. Create a new file in `app/` (e.g., `app/my-new-task.md`)
2. Follow the structure of existing task docs
3. Create a skill in `.claude/skills/my-new-task/SKILL.md`
4. Add it to the skills table in this overview and in CLAUDE.md
5. The new task inherits all shared context

---

## Document Hierarchy

```
app/
├── overview.md                      ← This file
│
├── shared/
│   ├── values.md                    ← Commitments, priorities, non-negotiables
│   ├── voice.md                    ← Tone, personality, style
│   ├── common-patterns.md           ← Shared conventions for code and conversation
│   └── output-spec-sc.md             ← Output format: SuperCollider
│
├── templates/
│   └── context-template.md          ← Scaffolding for new piece context files
│
├── config-spec.md                   ← What users can configure (developer-defined)
│
├── compose.md                       ← Start a composition
├── iterate.md                       ← Refine through feedback
├── critique.md                      ← Evaluate and offer perspective
└── spark.md                         ← Creative provocation

config.md                            ← User preferences (gitignored)
config/                              ← Context-specific sub-configs

../nla-framework/core/
├── nla-foundations.md               ← What NLAs are (framework)
└── skills/                          ← Skill logic (framework)

reference/
├── design-rationale.md              ← Why the system is built this way
├── friction-log.md                  ← Learning journal (active entries)
├── friction-log-archive.md          ← Resolved entries (searchable history)
├── system-status.md                 ← Current state snapshot
└── sessions/                        ← Maintenance session archives
```

### Music Directory

Compositions live in a separate directory (configurable, default `../duet-music/`), typically its own git repo. This keeps creative work separate from the system itself.

```
../duet-music/
├── active/                          ← Pieces in progress
│   └── [piece-name]/
│       ├── sketch.scd               ← Current code
│       ├── context.md               ← Intent, decisions, history
│       ├── requirements.md          ← Dependencies (if any)
│       └── iterations/              ← Version snapshots
├── done/                            ← Finished work
└── shelved/                         ← Parked ideas (may return)
```

Each piece lives in its own folder with a freeform, memorable name. The `context.md` file is the bridge between sessions — it captures what the piece is about, what was decided (and rejected), and what's unresolved. The AI drafts it, the human reviews it. See `app/templates/context-template.md` for the starting scaffolding.

---

## Document Index

### Shared Context
- [Values](shared/values.md) — Commitments, priorities, non-negotiables
- [Voice](shared/voice.md) — Tone, personality, style
- [Common Patterns](shared/common-patterns.md) — Shared conventions for code and conversation
- [Output Spec: SuperCollider](shared/output-spec-sc.md) — SC output format details
- [Config Spec](config-spec.md) — What users can configure and how

### Tasks
- [Compose](compose.md) — Start a composition from a concept or mood
- [Iterate](iterate.md) — Refine the composition through listening feedback
- [Critique](critique.md) — Evaluate the composition and offer perspective
- [Spark](spark.md) — Contextual creative provocation

### Reference
- [Design Rationale](../reference/design-rationale.md) — Why the system is built the way it is
- [Friction Log](../reference/friction-log.md) — Running log of issues and improvements
- [System Status](../reference/system-status.md) — Current state snapshot

---

## Getting Started

### First-Time Setup

1. Read [nla-foundations.md](../nla-framework/core/nla-foundations.md) — understand NLA concepts
2. Read this overview
3. Read shared context documents
4. Install SuperCollider if you haven't already

### Composing

1. Start Claude Code and run `/startup`
2. Run `/compose` with a concept, mood, or idea
3. Copy the generated SuperCollider code and run it
4. Tell the AI what you hear — run `/iterate` to refine
5. Use `/critique` for honest assessment, `/spark` when you're stuck
6. Use `/friction-log` to capture learnings as you go

---

*This is a living document. As the NLA system evolves, update this overview to reflect the current state.*
