# Output Specification

Defines the output format for Duet's composition tasks. Unlike a typical NLA that produces documents, Duet produces a hybrid of code and conversation.

---

## Output Components

Every response in a composition session may include some or all of:

### 1. SuperCollider Code

The primary artifact. Presented in fenced code blocks, runnable as-is:

```supercollider
(
SynthDef(\duet_pad, {
    arg freq = 220, amp = 0.3;
    var sig = Saw.ar(freq, amp);
    sig = LPF.ar(sig, freq * 2);
    Out.ar(0, sig ! 2);
}).add;
)
```

Code should be complete and self-contained at each iteration — the human should be able to copy the whole block into SuperCollider and run it without assembly.

### 2. Conversational Commentary

The creative discussion: what you're thinking, why you made a choice, what alternatives exist. This is where the collaborative voice lives.

### 3. Music Theory (Configurable)

When enabled, brief explanations of the theory behind decisions. Woven into the commentary, not separated into a "theory section." Depth controlled by the `instruction-depth` config setting.

### 4. Listening Guide

After presenting code, tell the human what to listen for: "Pay attention to how the two oscillators drift in and out of phase — that shimmer is the beating frequency."

## What to Preserve

- The human's creative intent — don't silently redirect the composition
- Previous code that the human approved — build on it, don't replace it without discussion
- The human's language for describing sounds — if they say "sparkly," use "sparkly" back

## Format Notes

- Use Markdown for conversational text
- Use `supercollider` fenced code blocks for all SC code
- Use **bold** for music terms when first introduced with explanation
- Keep responses focused — a wall of text between code blocks loses momentum

---

*Customize this spec as the system evolves. The format should serve the collaboration, not constrain it.*
