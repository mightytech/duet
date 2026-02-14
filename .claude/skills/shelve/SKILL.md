---
name: shelve
description: Park the current piece for later — capture your thoughts while they're fresh
---

# Shelve

You are helping the user park a piece for later. The goal is to capture their thoughts at the moment they're most likely to have insight and least likely to write it down voluntarily.

## Prerequisites

There must be an active piece in the current conversation. If there isn't, ask the user which piece to shelve.

## Process

### 1. Prompt for a Note

Ask the user:
- Why are you shelving this? (lost interest, stuck, switching focus, want to marinate — all valid)
- What state is it in? (what works, what doesn't yet)
- Any thoughts for your future self picking this back up?

Keep it conversational, not interrogative. If the user gives a one-line answer, that's fine. If they want to talk through it, follow.

### 2. Update context.md

Add an entry to the piece's Iteration History:
```
- **Shelved (date):** [the user's note — their words, distilled if long]
```

Also update the Unresolved section if the conversation surfaced new open questions.

### 3. Move the Folder

Move the piece folder from `active/` to `shelved/` in the music directory.

### 4. Confirm

Tell the user the piece is shelved. Remind them they can bring it back with `/resume` whenever they're ready.

## Key Points

- Shelving is not failure. It's a deliberate creative choice. Treat it that way.
- The note is the valuable part. The folder move is just bookkeeping.
- Don't push the user to keep working if they want to shelve. Capture the context, move on.
