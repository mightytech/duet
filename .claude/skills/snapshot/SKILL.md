---
name: snapshot
description: Save a versioned snapshot of the current piece — code and context frozen at this moment
---

# Snapshot

You are saving a snapshot of the current piece — freezing the code and context at this point in time so the user can return to it or compare it with future versions.

## Prerequisites

There must be an active piece in the current conversation. If there isn't, ask the user which piece to snapshot.

## Process

### 1. Prompt for a Note

Ask the user briefly: what's the state of the piece right now? Why save this version? This can be short — "before reharmonization" or "first version that grooves" is plenty. If the conversation already makes the reason obvious, suggest it and let them confirm.

### 2. Name the Snapshot

Suggest a short, descriptive name for the snapshot folder based on the note and conversation context. The user approves or renames. Examples: `v02-added-bass`, `before-reharmonization`, `first-groove`.

### 3. Save Files

Create a subfolder in the piece's `iterations/` directory with the snapshot name:

```
iterations/[snapshot-name]/
├── sketch.scd          ← Copy of current code
├── context.md          ← Copy of context.md as it stands now
└── note.md             ← Brief note: date, why this was saved, state of the piece
```

### 4. Update the Piece

Add an entry to the piece's Iteration History in `context.md`:
```
- **[snapshot-name] (date):** [brief description]
```

### 5. Confirm

Tell the user the snapshot is saved. The piece stays active — they can keep working.

## Key Points

- Snapshots are cheap. Don't overthink when to save one. If the user wants to save the state, save it.
- The piece continues in `active/` — this is a bookmark, not a transition.
- The `note.md` is for the snapshot itself (why it was saved). The `context.md` copy is a frozen record of all decisions up to that point.
