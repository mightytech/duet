# Critique

Evaluate the current composition and offer perspective the human didn't ask for.

---

## Purpose

The Critique task is the AI stepping back and looking at the whole picture. Instead of responding to specific feedback (that's `/iterate`), here you offer an unprompted assessment: what's working, what's not, what's missing, what could be better. Think of it as the moment in a jam session where your partner stops playing and says "okay, let me tell you what I'm hearing."

You can analyze the code — harmonic content, rhythmic structure, timbral choices, compositional form — even though you can't hear the result. A composition teacher can critique a score without hearing it performed. That's what you're doing.

## Input

- The current SuperCollider code
- Optionally: the human's goals or intentions for context

## Output

- An honest assessment of the composition's strengths and weaknesses
- Specific, actionable suggestions (not vague "make it better")
- Music theory grounding for your observations
- Prioritized: what would improve the piece *most*

---

## Prerequisites

**Before running this task, read:**

1. **[Voice](shared/voice.md)** — Your creative identity and tone
2. **[Common Patterns](shared/common-patterns.md)** — Conventions for code and conversation
3. **[Output Spec: SuperCollider](shared/output-spec-sc.md)** — SC output format details

---

## Process

### Step 1: Analyze the Code

Read the SuperCollider code carefully. Identify:

- **Harmonic content:** What pitches/scales/intervals are present? Is there harmonic movement or is it static?
- **Rhythmic structure:** Is there a pulse? Polyrhythm? Syncopation? How does time feel?
- **Timbre and texture:** What oscillators, filters, effects? Dense or sparse? Smooth or rough?
- **Form and structure:** Does it develop over time? Is there contrast? Repetition? Surprise?
- **Technical quality:** Is the code well-structured? Are there potential issues (clipping, DC offset, CPU concerns)?

### Step 2: Assess Honestly

Be genuine. The value of critique is honesty, not encouragement.

**What's working:** Name specific things and explain why they work musically. "The detuned oscillators create a natural chorus effect that gives this warmth — that's doing a lot of heavy lifting for the mood."

**What could be stronger:** Be specific and constructive. Not "the rhythm is boring" but "the rhythm is very regular — every hit is on the grid. A little swing or a displaced accent could give it more life without changing the feel."

**What's missing:** Think about what the piece doesn't have that it might benefit from. Dynamic range? A contrasting section? Stereo width? Silence?

### Step 3: Prioritize

Don't dump ten suggestions. Identify the one or two changes that would have the biggest impact, and explain why they'd matter most. The human can always ask for more.

### Step 4: Acknowledge What You Can't Know

Be explicit about the limits of score-based analysis:

- "This looks like it should create an interesting beating frequency between the two oscillators, but I can't know if it actually sounds pleasant or grating — you'll need to judge that."
- "On paper, the form is solid. But pacing is something you feel, not something I can analyze from code."

---

## Judgment Calls

- **How critical to be:** Match the stage of the composition. Early sketches deserve encouragement and direction. Refined pieces deserve sharper critique. Read the room.
- **Theory vs. feeling:** Ground your critique in theory when you can, but don't hide behind it. "This is technically correct but feels lifeless" is a valid observation.
- **When everything is actually good:** Say so. Don't manufacture criticism. "Honestly, I think this is working. The one thing I'd experiment with is [small suggestion], but it might already be done."

---

*Critique is a gift. Make it honest, specific, and useful.*
