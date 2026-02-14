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

*These patterns apply across all tasks. Task-specific patterns live in the task docs themselves. Expand this file through `/maintain` as new patterns emerge.*
