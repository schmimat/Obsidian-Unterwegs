---
context: conversation
description: Preserve session learnings to CLAUDE.md (any project)
model: opus
allowed-tools: Read, Edit, Write, Glob, Bash, AskUserQuestion
---

# /preserve - Preserve Session Knowledge to CLAUDE.md

Updates the project's CLAUDE.md with key learnings from this session, optimized for context efficiency.

## Instructions for Claude

### Step 1: Check for CLAUDE.md

Look for CLAUDE.md in the current working directory (or common variations):
- `CLAUDE.md`
- `Claude.md`
- `.claude/CLAUDE.md`

If not found, ask:
"No CLAUDE.md found. Would you like me to create one, or output preservation notes to conversation instead?"

### Step 2: Ask What to Preserve

Use AskUserQuestion with multi-select:

**Question:** "What should be preserved from this session?"

**Options (multi-select, max 4):**
1. **Status & Decisions:** What moved forward / completed, choices made and why
2. **Files & Structure:** Created/changed files, new directories, config
3. **Patterns & Insights:** Reusable learnings, discovered constraints, "aha" moments
4. **Blockers & Next Steps:** Warnings for future sessions, action items, pending work

### Step 3: Review Current CLAUDE.md

If CLAUDE.md exists, read it to understand:
- Current structure and format
- What sections exist
- What needs updating vs adding

### Step 4: Generate Updates

Based on selections, prepare updates following these rules:

**HIGH SIGNAL (include):**
- Status changes (1 line each)
- Decisions + rationale (table row format)
- New directories/files (brief tree or list)
- Clear next steps

**LOW SIGNAL (exclude):**
- Verbose explanations (point to docs)
- Implementation details (they're in files)
- Full file contents
- Timestamps or session logs

**FORMAT RULES:**
- Tables for structured data
- Single-line entries, not paragraphs
- Point to files: "See `path/to/file.md`"
- Target: CLAUDE.md under 280 lines

### Step 5: Apply Updates

Edit CLAUDE.md directly, then summarize:

```
CLAUDE.md Updated

Preserved:
- [What was added/changed]
- [What was added/changed]

CLAUDE.md is now [X] lines (target: <280)
```

### Step 6: Check Line Count & Archive Logic

After updating, count CLAUDE.md lines:
```bash
wc -l CLAUDE.md
```

**IF lines > 280:**

1. **Identify auto-archivable content:**
   - `## Session Notes (DATE)` sections older than 7 days
   - `## Completed Projects` section

2. **Calculate impact:**
   - Current lines
   - Lines after auto-archive

3. **Report to user:**
   ```
   CLAUDE.md is [X] lines (target: <280).

   Auto-archivable content found:
   - Session Notes (2026-01-10) - 25 lines
   - Completed Projects - 15 lines

   Archiving would reduce to [Y] lines.

   Archive now? [Yes / No, all content is essential]
   ```

4. **IF still > 280 after auto-archivable content:**

   Identify other sections that are NOT in the CORE list and NOT marked PROTECTED:

   ```
   Still over 280 lines. These sections could also be archived:
   - ## Old Reference Section - 12 lines
   - ## [Other Section] - 8 lines

   Archive these too? [Yes / No / Select which]
   ```

5. **IF user approves archiving:**
   - Append archived content to `{project_root}/CLAUDE-Archive.md`
   - Remove archived sections from CLAUDE.md
   - Report result

### Step 7: Archive File Handling

**Find project root** (same logic as /compress):
```
Walk up from pwd looking for CLAUDE.md or .git
Archive to: {project_root}/CLAUDE-Archive.md
```

**Archive file format:**
```markdown
# CLAUDE.md Archive

Archived content from CLAUDE.md to maintain context efficiency.

---

## Archived: [DATE]

[Archived section content]

---
```

**If archive exists:** Append new content with date header.

### Step 8: If No CLAUDE.md

Output a structured summary to conversation (similar to /compress):

```markdown
# Session Preservation: [Brief Title]
**Project:** [Directory name]
**Date:** [Today]

## [Selected sections with content]

---

## Quick Resume Context
[2-3 sentences for future sessions]
```

Then suggest: "Consider creating a CLAUDE.md to persist this across sessions."

---

## CORE Sections (Never Suggest Archiving)

These are examples of section names you should NEVER suggest archiving. Adapt to the project's actual CLAUDE.md:

- `## Approach` / `## Philosophy`
- `## Paths` / `## Structure`
- `## Key References` / `## Links`
- `## Skills` / `## Commands`
- `## Key Patterns` / `## Conventions`
- Any section with `(PROTECTED` in the heading

Customise this list by marking sections in your CLAUDE.md:
- Add `(PROTECTED)` to any heading to prevent archiving
- Add `(ARCHIVABLE)` to mark sections as safe to archive

---

## Auto-Archivable Patterns

These patterns are automatically identified as archivable:

| Pattern | Rule |
|---------|------|
| `## Session Notes (DATE)` | Archive if DATE is > 7 days old |
| `## Completed Projects` | Always archivable |
| Sections with `(ARCHIVABLE)` | User-marked as archivable |

---

## Guidelines

- **Context efficiency is paramount.** Future sessions pay for every token
- **Signal over noise.** The "why" matters more than the "what"
- **Point, don't duplicate.** Reference files instead of copying content
- **Respect existing format.** Match the CLAUDE.md style already in use
- **Never archive PROTECTED or CORE.** These are essential for Claude's operation
- **Ask before archiving non-auto content.** User decides what's truly essential

---

## Technical Constraints

- `AskUserQuestion`: max. **4 Optionen** pro Frage, max. **4 Fragen** pro Aufruf — mehr führt zu einem stillen Fehler
- Diese Datei liegt in **6 Vaults** (`_claude/commands/`) **plus dem vault-übergreifenden `Obsidian-Vaults`-Root** (angelegt 2026-08-08 für Cross-Vault-Sessions, siehe `Obsidian-Vaults/CLAUDE.md`) — Änderungen synchron in **allen 7** Kopien durchführen. Die Root-Kopie ist NICHT Obsidian-synced (liegt außerhalb aller Vaults, lokal auf LXC 203) — manuell auf jedem Gerät nachziehen, das dort ebenfalls Cross-Vault-Sessions starten soll.
- `/compact` ist ein eingebautes Kommando — `compact.md` existiert bewusst nicht
