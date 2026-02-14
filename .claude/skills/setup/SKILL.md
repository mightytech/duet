---
name: setup
description: Check your environment and install what's needed for the current piece
---

# Setup

You are checking the user's environment against what the current piece (or the system in general) needs, and helping install anything that's missing.

This is one of the places where the NLA shines — you can handle cross-platform differences naturally through judgment and conversation, without coded platform detection. Just check what's there, figure out what's missing, and help the user get set up.

## Process

### 1. Read the Environment

Check if `environment.md` exists at the music directory root (from config, default `../duet-music/`).

**If it exists:** Read it. It records the platform, sound engine, and what's already installed. Use this as your starting point — don't re-detect things that are already known.

**If it doesn't exist:** This is a first-time setup. Detect the basics:
- Platform (run `uname` or equivalent — don't overthink this)
- Sound engine (check if `sclang` is on the PATH, or whatever the configured engine requires)
- Create `environment.md` with what you find (see format below)

### 2. Check Requirements

If there's an active piece, read its `requirements.md`. Compare what's needed against what `environment.md` says is available.

If there's no active piece, check the general system requirements: is the configured sound engine installed and accessible?

### 3. Report and Offer Help

**If everything is met:** Say so briefly. "Environment looks good — SuperCollider and sc3-plugins are installed."

**If there are gaps:** List what's missing and offer to help install. Always confirm before installing anything. Be specific about what you'll do:

```
Your piece needs sc3-plugins (for DWGBowed), but I don't see them installed.

On macOS, the easiest way is:
  brew install sc3-plugins

Want me to run that?
```

Use your knowledge of the platform (from environment.md or detection) to suggest the right installation method. If you're unsure, say so and ask.

### 4. Update environment.md

After any changes (new detection or new installs), update `environment.md` in the music directory root.

## environment.md Format

This file is AI-maintained — the AI writes it, reads it, and keeps it current. It lives at the music directory root.

```markdown
# Environment

## Platform
[OS name and version, e.g., "macOS 14.2" or "Ubuntu 24.04"]

## Sound Engine
[Engine name, version, and path — e.g., "SuperCollider 3.13.0, sclang at /usr/local/bin/sclang"]

## Installed Extensions
[List of installed extensions/plugins relevant to composition]
- sc3-plugins (installed via Homebrew, 2026-02-14)

## Last Checked
[Date of last setup run]
```

Keep it simple and factual. This isn't documentation — it's a cache of what's known about the environment.

## Key Points

- **Always confirm before installing.** No silent installs, ever.
- **Use the platform naturally.** You know how macOS, Linux, and Windows differ. Apply that knowledge — don't ask the user to figure out platform-specific commands.
- **Update environment.md** after every setup run so future sessions don't re-detect unnecessarily.
- **Be honest about limits.** If you can't determine whether something is installed, say so. If installation fails, help debug rather than retrying blindly.
