# Duet

A collaborative human/AI music composition system, built as a Natural Language Application on the [NLA Framework](../nla-framework/).

Duet flips the typical AI architecture: instead of traditional code calling an LLM through an API, the LLM is the application — orchestrating SuperCollider while providing a human-centered creative interface. The AI is a genuine creative partner with opinions, musical knowledge, and honesty about what it can and can't do.

---

## Prerequisites

**NLA Framework** must be available at `../nla-framework/` (sibling directory to this project).

```bash
# If you haven't cloned it yet:
git clone <framework-repo-url> ../nla-framework
```

**Claude Code** must be installed. This project runs inside Claude Code sessions.

**SuperCollider** must be installed for playing the generated music. Download from [supercollider.github.io](https://supercollider.github.io/).

---

## Quick Start

1. Start Claude Code in this directory
2. Run `/startup` to load foundational context
3. Run `/compose` and describe what you want to hear
4. Copy the generated code into SuperCollider and play it
5. Tell the AI what you hear — run `/iterate` to refine
6. Use `/critique` for honest feedback, `/spark` when you're stuck

---

## What's Inside

```
├── CLAUDE.md                        # Runtime identity and configuration
├── app/                             # The application (LLM reads and executes)
│   ├── overview.md                  # What Duet does, how pieces connect
│   ├── shared/
│   │   ├── voice-and-values.md      # Creative identity and collaboration style
│   │   ├── common-patterns.md       # Shared conventions for code and conversation
│   │   └── output-spec.md           # Output format (SC code + commentary)
│   ├── config-spec.md               # What users can configure (developer-defined)
│   ├── compose.md                   # Start a composition
│   ├── iterate.md                   # Refine through feedback
│   ├── critique.md                  # Evaluate and offer perspective
│   └── spark.md                     # Creative provocation
├── config.md                        # User preferences (gitignored)
├── config/                          # Context-specific sub-configs
├── reference/                       # Maintenance records (not loaded at runtime)
│   ├── design-rationale.md          # Why the system is built this way
│   ├── friction-log.md              # Learning journal (active entries)
│   ├── friction-log-archive.md      # Resolved entries
│   ├── system-status.md             # Current state snapshot
│   └── sessions/                    # Maintenance session archives
├── .claude/skills/                  # Skill entry points
│   ├── startup/                     # Framework wrapper
│   ├── compose/                     # Start a composition
│   ├── iterate/                     # Refine through feedback
│   ├── critique/                    # Evaluate composition
│   ├── spark/                       # Creative provocation
│   ├── maintain/                    # Framework wrapper
│   ├── friction-log/                # Framework wrapper
│   ├── plan/                        # Framework wrapper
│   ├── preferences/                 # Framework wrapper
│   └── validate/                    # Framework wrapper
└── lib/                             # Traditional code helpers
```

---

## The Composition Loop

```
You have an idea → /compose generates a starting point → You listen in SuperCollider
    → You react → /iterate refines → You listen again → ...
```

At any point:
- `/critique` — Ask the AI to step back and assess the whole piece
- `/spark` — Get a creative provocation when you're stuck or comfortable

The AI is a partner, not a tool. It has opinions, pushes back when it disagrees, and suggests ideas you didn't ask for. But you're the one who can hear the music, so you always have the final call.

---

## Configuration

Run `/preferences` to personalize how Duet behaves:

- **Instruction depth** — How much music theory accompanies creative decisions (off / light / detailed)
- **Collaboration style** — How opinionated the AI is (deferential / balanced / opinionated)
- **SC detail level** — How much SuperCollider code is explained (beginner / intermediate / expert)
- **Adventurousness** — How far the AI pushes from conventional territory (grounded / exploratory / experimental)

Config files are gitignored so that `git pull` updates the app without touching your preferences.

---

## The Improvement Loop

```
Observe something → /friction-log captures it → Friction log stores it → /maintain implements changes
```

1. Compose music with Duet
2. Notice something that could be better (voice, code quality, missed pattern)
3. Run `/friction-log` to record the observation
4. When ready, run `/maintain` to process accumulated observations into doc changes
5. The docs improve, and Duet's behavior improves with them

---

## Why an NLA?

Traditional AI music tools generate music *for* you. Duet composes music *with* you. The difference is architectural:

- The LLM isn't called through an API — it IS the application
- The documentation isn't describing the app — it IS the app
- Changing behavior means editing prose, not writing code
- The AI has a genuine creative identity defined in `app/shared/voice-and-values.md`

This makes Duet a demonstration of what Natural Language Applications can do — software where documentation is source code and an LLM is the runtime.

---

## Framework Updates

```bash
cd ../nla-framework
git pull
```

Framework updates (skill logic, NLA foundations) take effect immediately through the thin wrapper pattern. Your domain content is never touched.

---

*For more about the NLA Framework, see the [framework README](../nla-framework/README.md).*
