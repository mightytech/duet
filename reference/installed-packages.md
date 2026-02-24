# Installed Packages

Packages installed in this NLA, maintained by `/install` and `/update`.

Each entry records what package was installed, when, what state the package was in, and what changes were made. This log is how `/update` knows what's current and what needs changing.

---

## NLA Framework

**Installed:** Pre-convention tracking (original `/create-app` generation)
**Source:** `../nla-framework/`

Original project generated via `/create-app` before the framework had formal package tracking.

### Convention Update — 2026-02-18

**Applied by:** Framework maintainer (manual, from framework side)
**Reason:** Framework removed scaffold directory and established intent files as single source of truth. Existing projects needed alignment with current conventions.

**Skill wrappers added:**
- `.claude/skills/install/SKILL.md` — thin wrapper delegating to `core/skills/install.md`
- `.claude/skills/update/SKILL.md` — thin wrapper delegating to `core/skills/update.md`

**Skill wrappers modified:**
- `.claude/skills/startup/SKILL.md` — added `disable-model-invocation: true` frontmatter (ejected/custom startup; full custom content preserved, only frontmatter added)

**Reference files created:**
- `reference/feedback-log.md` — standard feedback log structure
- `reference/feedback-log-archive.md` — empty archive
- `reference/installed-packages.md` — this file

**CLAUDE.md updated:**
- Added `/install` and `/update` to skills table

**Note:** Duet has a custom (ejected) startup skill with significant domain-specific logic. The convention update preserved all custom content and only added the required frontmatter flag. Duet already had config infrastructure, validate, preferences, and friction-log in place.

### Updated 2026-02-21

**Package state:** `05eb69e` (framework HEAD)

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| `skills-intent.md` | `/plan` removed from framework; `/export` added | Deleted `.claude/skills/plan/`, removed `/plan` from CLAUDE.md and system-status.md. Created `.claude/skills/export/SKILL.md` thin wrapper, added `/export` to CLAUDE.md skills table. |
| `skills-intent.md` | README drift from convention update | Added `install/`, `update/`, `export/` to README skills tree. Added `feedback-log.md`, `feedback-log-archive.md`, `installed-packages.md` to README reference tree. |

**Notes:** Core file changes (maintenance learnings in foundations/maintain/validate, output-spec made optional, Cardinal Rule broadened, startup extensibility) propagate automatically via thin wrappers. Duet's ejected startup is unaffected. No action taken on startup un-eject — current ejected version works well.

---

<!-- /install and /update maintain this file. Each package gets a section with install
     history and update records. Don't remove old entries — they tell the full story. -->
