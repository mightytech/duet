# Common Patterns

Patterns and conventions shared across all tasks. When multiple tasks need the same approach, it lives here. Starting minimal — patterns will emerge through use and get added via `/friction-log` + `/maintain`.

---

## SuperCollider Code Conventions

### Code Structure

Present SC code in fenced code blocks with the `supercollider` language tag:

```supercollider
// Example: a simple sine tone
{ SinOsc.ar(440, 0, 0.2) }.play;
```

### Code Comments

Include comments that explain *musical intent*, not just what the code does:

- **Good:** `// Slow the LFO to let the texture breathe`
- **Not good:** `// Set frequency to 0.25`

Comments bridge the gap between code and music. They're especially important for users who are learning.

### Iteration Continuity

When iterating on a composition, always present the complete current state of the code — not just the diff. The human needs to be able to copy, paste, and run. If the code is getting long, break it into clearly labeled sections.

---

## Conversation Conventions

### Proposing Changes

When suggesting a modification, explain the musical reasoning first, then show the code:

1. What you're changing and why (musical reasoning)
2. The updated code
3. What to listen for when they play it

### Flagging Uncertainty

Use TK notes when you're unsure how something will sound:

| Note | When to use |
|------|-------------|
| `TK [LISTEN]` | You think this will work but can't verify — human needs to test |
| `TK [THEORY]` | Your theory-based prediction about how this sounds |
| `TK [SC-CHECK]` | You're unsure about SuperCollider syntax or behavior |
| `TK [ALTERNATIVE]` | You have another approach that might work better |

### The Current State

At natural checkpoints in the conversation, summarize where the composition stands:
- What's working (per the human's feedback)
- What's still being developed
- What hasn't been explored yet

---

## Playing Audio

When auto-play is enabled (see `config-spec.md`), the AI plays generated code so the user hears the result without leaving the conversation.

### The Play Workflow

1. **Save the code** to the piece's `.scd` file in the piece folder
2. **Stop previous audio** — free running synths before starting new ones (e.g., send `s.freeAll` to sclang)
3. **Play the new code** — execute the `.scd` file via `sclang` in the background so the conversation isn't blocked
4. **Handle errors conversationally** — if sclang reports compilation errors, surface them naturally ("That didn't compile — looks like a missing semicolon on line 12. Let me fix that."). Don't dump raw sclang output.

### Principles

- **Audio supplements, never replaces.** Always present the code and commentary in the conversation. The user should be able to read and understand what changed even if they couldn't hear it.
- **Stop before you start.** Always clean up previous audio before playing new code. The user shouldn't have to manually stop things.
- **Keep the server running.** Avoid booting/killing scsynth on every iteration — the boot time breaks creative flow. Keep the server alive between plays.
- **Invite listening.** After playing, prompt the user to listen and react: "I've started the updated version — take a listen. The new bass line comes in around bar 5."
- **The AI manages the plumbing.** sclang process management, server state, file paths — the AI handles these at runtime using its tools. The docs describe the behavior, not the shell commands.

---

## Piece Folders and Files

### Naming

Piece folders use freeform names chosen for memorability — `gypsy-eno`, `midnight-drones`, `the-one-that-clicks`. When starting a new piece, suggest a name based on the concept conversation and let the human approve or rename.

### context.md

The most important file in a piece folder. It's the bridge between sessions — a curated record of what the piece is about, what was decided, what was rejected, and what's unresolved. Use the template at `app/templates/context-template.md` as scaffolding; include sections that are relevant, skip ones that aren't. If the human overrides the structure (adds sections, removes them, reorganizes), follow their lead — that's valuable signal about what this piece needs.

Draft context.md as a distillation, not a transcript. Write it so someone (human or AI) starting a cold session can pick up the collaboration without re-reading the full conversation history.

### Music Directory

Read the music directory path from config (default `../duet-music/`). Pieces in progress live in `active/`, finished work in `done/`, parked ideas in `shelved/`. Don't maintain an index file — read folders and context files on demand.

### Forking

When the user wants to try a fundamentally different direction during `/iterate` — not a tweak, but a divergent path — fork the piece. Copy the piece folder with a new name (suggest one, human approves), and both versions stay in `active/`. This isn't a separate skill; it's a natural moment in the creative conversation. Recognize when the user is describing a fork ("what if we went in a completely different direction," "let's try a totally different approach to the harmony") and offer it.

### Lifecycle

Pieces move between `active/`, `shelved/`, and `done/` through deliberate transitions:

| Skill | From | To | Purpose |
|-------|------|----|---------|
| `/snapshot` | — | `iterations/` | Freeze current state as a bookmark; piece stays active |
| `/shelve` | `active/` | `shelved/` | Park a piece; capture thoughts for future self |
| `/finish` | `active/` | `done/` | Mark as complete; capture reflections |
| `/resume` | `shelved/` | `active/` | Bring a piece back to active work |

Every transition prompts for a note — the real value is capturing what the user is thinking at the moment they're most likely to have insight.

---

*These patterns apply across all tasks. Task-specific patterns live in the task docs themselves. Expand this file through `/maintain` as new patterns emerge.*
