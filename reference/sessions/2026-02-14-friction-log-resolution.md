# Maintenance Session: Resolve All Pending Friction Log Entries

**Date:** 2026-02-14
**Status:** Complete

## Intent

Process the four friction log entries from the first composition session (2026-02-13) into system documentation. These covered the full gap between "we can compose" and "we can compose across sessions with a real workflow."

## Design Thinking

The entries were interconnected. Directory structure was foundational, lifecycle and setup built on it, auto-play was independent. We worked in that order.

**Key user insights that shaped the work:**

- **Snapshots are just another shelve/finish.** Originally deferred as "needs to develop through use." The user saw that the core operation (capture state + note → put somewhere) is identical across /snapshot, /shelve, /finish. Only the destination differs. This collapsed a fuzzy concept into something implementable.

- **The iterate contract is judgment-based.** "Would a future session need to know this?" — not "how big was the code change?" Small code changes can carry big decisions (4/4 → 7/8). The AI's marginal cost of updating context.md is near zero, so the threshold should be about intent, not effort.

- **The template is for the AI, not the human.** So rigidity isn't a concern — it's scaffolding, not a form. Human overrides are signal worth learning from.

- **Engine-specific specs beat premature abstraction.** Rather than making output-spec engine-agnostic (which would water it down), lock each spec to an engine. `output-spec-sc.md` now; `output-spec-sonic-pi.md` when that engine arrives. If overlap emerges, extract it then.

- **Environment as a cache.** Platform detection results go in `environment.md` so /startup reads instead of re-detecting. /setup writes it; everything else consumes it.

## Changes Made

- Codified music directory conventions across all relevant docs
- Created context-template.md for AI scaffolding
- Built lifecycle skills (/snapshot, /shelve, /finish, /resume) as a unified pattern
- Expanded /startup with piece awareness and environment checking
- Created /setup skill with environment.md caching
- Added Sound Engine config, renamed output-spec to output-spec-sc
- Added auto-play config and play workflow documentation
- Updated README with new skills, config options, and file tree
- Wrote framework feedback letter (10 learnings) to nla-framework repo

## Framework Feedback

After completing the Duet work, we identified patterns that should flow upstream to the NLA framework. Wrote a feedback letter at `../nla-framework/reference/feedback/2026-02-14-duet-maintenance-learnings.md` covering 9 missing patterns (persistence, session bridges, lifecycle, startup extensibility, environment management, tool-specific specs, tool execution, deeper create-app scaffolding, NLA→framework feedback channel) and 4 assumptions to broaden (Cardinal Rule framing, startup scaffold leaks, scaffold shaping expectations, validate assuming determinism). Filed as a friction log entry in the framework repo.

This is the first "maintenance exit interview" — the letter itself is the prototype of the proposed pattern.

## State at Close

All four friction log entries resolved and archived. The system now supports full composition lifecycle: create, iterate, snapshot, shelve, finish, resume. Environment management and auto-play are documented and ready for first real use. No pending Duet friction log entries. Framework feedback filed and awaiting framework /maintain processing.
