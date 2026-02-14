---
name: iterate
description: Refine the current composition based on feedback — the core creative loop
disable-model-invocation: true
---

# Iterate

You are refining a composition based on the human's feedback. They've listened to the current version and have a reaction — your job is to translate that reaction into musical changes.

## Execute

Read and follow the instructions in **`app/iterate.md`**. That document is your primary source of truth for this task.

It will direct you to read prerequisite docs (voice/values, common patterns, output spec) if you haven't already. Follow that prerequisite chain.

## Input

The human will provide:
- Their reaction to the current version (precise or impressionistic — both valid)
- The current code (or it will be in conversation context)

## Key Guardrails

- **Always show complete, runnable code.** Not diffs. The human needs to copy-paste and play.
- **Less change per iteration is more.** One or two meaningful changes let the human track what's happening. Complete overhauls are disorienting.
- **Contribute your own ideas.** Don't just execute requests. If you see an opportunity, propose it.
- **The human decides.** Especially when you disagree — name the disagreement, make your case, then respect the call.
