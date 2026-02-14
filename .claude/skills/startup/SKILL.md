---
name: startup
description: Initialize the NLA runtime. Use at session start or when context feels stale after long work.
---

# Startup

## Step 1: Load Foundational Context

Read these documents **in order:**

1. **`../nla-framework/core/nla-foundations.md`** — What NLAs are, the hybrid model, key principles
2. **`app/overview.md`** — What this NLA does, how its pieces connect
3. **`app/shared/voice-and-values.md`** — Creative identity and collaboration style
4. **`app/shared/common-patterns.md`** — Shared conventions for code and conversation
5. **`app/shared/output-spec-sc.md`** — SC output format details
6. **`config.md`** (if it exists) — User preferences. If config routes to sub-configs, read those too.

## Step 2: Check Active Pieces

Read the music directory (from config, default `../duet-music/`) and scan `active/` for piece folders.

**If no active pieces:** Note "No active pieces" and suggest `/compose` to start something new.

**If 1–4 active pieces:** Use `AskUserQuestion` to let the user pick. For each piece, read the Concept section of its `context.md` to show a meaningful description — not just the folder name. Include a "Start something new" option.

**If more than 4 active pieces:** List them all with their concepts. Ask the user which to continue, or whether they want to start new.

**If a piece folder has no `context.md`:** Still show it — use the folder name, note that context is missing.

When the user picks a piece, read its full `context.md` and present a brief summary: the concept, what state it's in (from Iteration History and Unresolved), and any listening notes that haven't been addressed yet.

## Step 3: Quick Environment Check

After a piece is selected, glance at `environment.md` (music directory root) and the piece's `requirements.md` if it exists. This is a quick status check, not a full setup.

- **Environment assessed, requirements met:** Don't mention it — everything's fine.
- **Requirements exist but no environment.md:** Note what the piece needs and suggest running `/setup`. Example: "gypsy-eno needs sc3-plugins — run `/setup` to check your environment."
- **Known gaps** (environment.md exists but doesn't include something requirements.md needs): Flag the specific gap.

Keep this lightweight — one line, not a wall of text. The user can run `/setup` if they want the full check.

## Step 4: Confirm Ready

Confirm you've loaded foundational context. Note whether config was loaded. Present the active piece (if selected) or await direction.

## When to Re-Run

Run `/startup` again if:
- Your context has been compacted and project specifics feel fuzzy
- You've been working for a long session and foundational context feels stale
- You're switching between pieces
