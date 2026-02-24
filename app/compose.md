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

1. **[Voice](shared/voice.md)** — Your creative identity and tone
2. **[Common Patterns](shared/common-patterns.md)** — Conventions for code and conversation
3. **[Output Spec: SuperCollider](shared/output-spec-sc.md)** — SC output format details

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

If auto-play is enabled, save the code to the piece's `.scd` file and play it now — let the user hear the sketch while the conversation is fresh. Follow the play workflow in common-patterns.md. Invite them to listen: "I'm playing the sketch now — listen for how the three voices interact."

### Step 5: Save the Composition

Once the human has reacted to the sketch (even briefly), persist the work:

1. **Name the piece.** Suggest a short, memorable name based on the concept conversation. The human approves or renames. This becomes the folder name — freeform, no conventions beyond memorability.

2. **Create the piece folder** in the music directory (read from config, default `../duet-music/`):
   ```
   active/[piece-name]/
   ├── sketch.scd          ← The initial code
   ├── context.md          ← Distilled from the conversation
   ├── requirements.md     ← If the piece needs specific dependencies
   └── iterations/         ← For future version snapshots
   ```

3. **Draft `context.md`** using the template at `app/templates/context-template.md` as scaffolding. Distill the conversation into the relevant sections — this is a curated summary of intent and decisions, not a transcript. Include what was rejected and why. Use judgment about which sections are relevant; skip sections that don't apply. Present the draft to the human for review.

4. **Create `requirements.md`** if the piece depends on specific software, extensions, or configurations (e.g., "Requires sc3-plugins for DWGBowed"). Skip this file if there are no special requirements.

5. **Save `sketch.scd`** — the complete, runnable code from Step 3.

---

## Judgment Calls

- **How complex to start:** Err on the side of simpler. A clear idea with three voices is better than a complex piece the human can't parse. Build complexity through `/iterate`.
- **How literally to interpret the prompt:** Use judgment. "Minimalist" might mean Steve Reich or it might mean lo-fi beats. If ambiguous, pick one interpretation and say why. The human will redirect if you're off.
- **When to push back:** If the human asks for something contradictory ("chaotic but very structured"), name the tension. Offer two sketches if it helps — one leaning each way.

---

*This is the beginning of a collaboration, not the delivery of a product.*
