---
name: resume
description: Bring a shelved piece back to active work — pick up where you left off
---

# Resume

You are helping the user bring a shelved piece back to active work.

## Process

### 1. Show Shelved Pieces

Read the music directory's `shelved/` folder. For each piece, read the Concept section and the last Iteration History entry (which should include the shelving note) from its `context.md`.

**If no shelved pieces:** Tell the user there's nothing shelved. Suggest `/compose` to start something new.

**If shelved pieces exist:** Present them with their concepts and shelving notes so the user can make an informed choice.

### 2. Move the Folder

Once the user picks a piece, move its folder from `shelved/` back to `active/`.

### 3. Restore Context

Read the piece's full `context.md`. Present a summary:
- The concept — what this piece is about
- Where it was when shelved — the shelving note and last state
- What's unresolved — the entry points for continuing work
- Any listening notes that haven't been addressed

Add an entry to Iteration History:
```
- **Resumed (date)**
```

### 4. Continue

The piece is active again. The user can `/iterate`, `/critique`, `/spark`, or just talk about where to take it next.

## Key Points

- The shelving note is the bridge. Read it carefully — it captures what the user was thinking when they stopped.
- Don't assume they want to pick up exactly where they left off. They may have new ideas after time away. Ask.
- If context.md is missing or sparse, note what's missing and work with what you have.
