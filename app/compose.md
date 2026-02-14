# Compose

Start a new musical idea from a concept, mood, or description. This is where compositions begin.

---

## Purpose

The Compose task takes a human's creative starting point — anything from "something upbeat and minimal" to "I want a dark ambient drone that sounds like being underwater" — and generates an initial SuperCollider sketch. This is a first draft, not a finished piece. The goal is to give the human something to *react to* — a starting point for the `/iterate` loop.

## Input

- A creative prompt: mood, concept, reference, or description of any specificity
- Optionally: tempo, key, time signature, or other constraints

If the human is vague, that's fine. Vagueness is a creative starting point, not a problem to solve.

## Output

- SuperCollider code that can be copied and run immediately
- Explanation of creative choices (why this scale, this rhythm, this texture)
- Music theory context if configured (see `config-spec.md`)
- A listening guide: what to pay attention to when they hit play

---

## Prerequisites

**Before running this task, read:**

1. **[NLA Foundations](../nla-framework/core/nla-foundations.md)** — Understand what you're doing
2. **[Voice and Values](shared/voice-and-values.md)** — Your creative identity
3. **[Common Patterns](shared/common-patterns.md)** — Conventions for code and conversation
4. **[Output Spec](shared/output-spec.md)** — Output format details

---

## Process

### Step 1: Understand the Vision

Listen to what the human says. Parse everything — mood words, references, constraints, things they explicitly don't want. If they say "something like Aphex Twin but calmer," they've told you a lot: electronic, textured, rhythmically interesting, but with space.

If the prompt is very sparse ("make something cool"), ask one focused question to get a direction. Don't interrogate — one question, then start.

### Step 2: Make Creative Decisions

Based on the human's input, make deliberate musical choices:

- **Scale/mode** — What harmonic palette fits the mood?
- **Tempo** — What pace serves the concept?
- **Texture** — Dense or sparse? Smooth or gritty?
- **Rhythm** — Driving beat, floating pulse, no pulse at all?
- **Timbre** — What kinds of sounds (oscillators, noise, samples)?

Make these choices with intention and explain your reasoning. This is where your musical knowledge adds value — you're not just generating code, you're making aesthetic arguments.

### Step 3: Generate SuperCollider Code

Write a complete, runnable SuperCollider sketch. Keep it focused:

- Start simple. A few voices, a clear idea. The human can always ask for more.
- Include comments that explain musical intent (see common-patterns.md)
- Make the code modifiable — use variables for key parameters so the human can tweak
- Ensure it runs as-is when pasted into SuperCollider

### Step 4: Present and Invite Reaction

After the code, tell the human:
1. What creative choices you made and why
2. What to listen for when they play it
3. What you're most uncertain about (be honest — you can't hear it)
4. One or two directions this could go next

The goal is to start the conversation, not deliver a finished product.

---

## Judgment Calls

- **How complex to start:** Err on the side of simpler. A clear idea with three voices is better than a complex piece the human can't parse. Build complexity through `/iterate`.
- **How literally to interpret the prompt:** Use judgment. "Minimalist" might mean Steve Reich or it might mean lo-fi beats. If ambiguous, pick one interpretation and say why. The human will redirect if you're off.
- **When to push back:** If the human asks for something contradictory ("chaotic but very structured"), name the tension. Offer two sketches if it helps — one leaning each way.

---

*This is the beginning of a collaboration, not the delivery of a product.*
