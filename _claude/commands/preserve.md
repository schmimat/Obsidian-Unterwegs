---
context: conversation
description: Preserve session learnings to CLAUDE.md (any project)
model: opus
allowed-tools: Read, Edit, Write, Glob, Bash, AskUserQuestion
---

# /preserve - Preserve Session Knowledge to CLAUDE.md

Updates the **right** CLAUDE.md with key learnings from this session. CLAUDE.md is a *current-state* file, not a diary: every byte is loaded into every future session (and every subagent) below it.

Concept and rationale: `PKM-Dirigent/Doku/CLAUDE.md-Konzept – Aufbau und Pflege.md`.

## Instructions for Claude

### Step 1: Pick the target CLAUDE.md (not blindly the working directory)

1. Collect the files this session actually created or changed.
2. For their common topic folder, walk **upward** until the first `CLAUDE.md` → that is the target (the lowest file responsible for the topic).
3. If the topic is a project folder **without** its own CLAUDE.md (e.g. a pure documentation cluster with a `README.md`): the target is the parent CLAUDE.md, but only its short status block for that project (max. 5 lines). Details go into the project's `README.md` or a note, not into CLAUDE.md.
4. If the session touched several unrelated topics, update each target separately.
5. Tell the user which file(s) you will update and why. If no CLAUDE.md exists at all, go to Step 8.

### Step 2: Ask What to Preserve

Use AskUserQuestion with multi-select:

**Question:** "What should be preserved from this session?"

**Options (multi-select, max 4):**
1. **Status & Decisions:** What moved forward / completed, choices made and why
2. **Files & Structure:** Created/changed files, new directories, config
3. **Patterns & Insights:** Reusable learnings, discovered constraints, "aha" moments
4. **Blockers & Next Steps:** Warnings for future sessions, action items, pending work

### Step 3: Read the target and its parents

Read the target CLAUDE.md **and** the CLAUDE.md files above it (up to the root and the global copy). Note:
- existing sections and format
- entries that this session makes **obsolete, completed or wrong**
- facts that already live one level higher or lower (must not be duplicated)

### Step 4: Generate Updates — replace, don't append

**The six rules:**

| Rule | Meaning |
|---|---|
| **Current state only** | Rules, one-line decisions, open items, pointers. No narratives, no "how we found it". |
| **Replace, don't append** | Update an existing entry in place. Remove items that are done (move them to the archive, Step 6). Correct wrong statements instead of adding a "Korrektur" paragraph. |
| **Each fact once, at the lowest level** | Global rules (model choice, agents) only in `CLAUDE-Global.md`. Parent files only point to child files. Never copy a pattern into a second CLAUDE.md — link it. |
| **One line per entry** | Decisions as `**Entscheidung** — Grund (Datum)`. If it needs more than ~2 lines, the details belong in a note; CLAUDE.md links to it. |
| **No history chains** | No "Zuletzt aktualisiert / Vorherige Aktualisierung / Davor" footers. At most one line with date + topic of the last update. |
| **Absolute dates only** | Write `2026-09-29`, never "heute", "aktuell", "Heute: …", "letzte Woche" — they silently go stale. |

Maintainer notes that Claude need not read can go in HTML comments (`<!-- … -->`): Claude Code strips them before loading, so they cost no tokens.

**HIGH SIGNAL (include):** status changes, decisions + reason, new files/dirs (brief), safety-relevant facts, reusable pitfalls (one line + pointer), clear next steps.

**LOW SIGNAL (exclude):** explanations (point to docs), implementation details, full file contents, timestamps/session narration, completed items, anything already in a parent/child CLAUDE.md or in a note.

### Step 5: Apply Updates

Edit the target directly, then report:

```
CLAUDE.md Updated: <path>

Preserved:
- [What was added/changed]
Removed/archived:
- [What was replaced or moved to the archive]

Size: [X] lines, [Y] KB (~[Y*1000/3.5] tokens) — target ≤ 12 KB, limit 15 KB
```

### Step 6: Size check & archive (bytes, not lines)

```bash
wc -lc CLAUDE.md
```

Long lines make line counts misleading — **bytes decide**.

| Size | Action |
|---|---|
| ≤ 12 KB | fine |
| 12–15 KB | propose archiving completed items and narrative sections |
| > 15 KB | **archive before adding anything new**; ask the user which sections to move |

Always archivable without asking: completed next steps, `(ARCHIVABLE)` sections, `## Session Notes (DATE)` older than 7 days, "Zuletzt aktualisiert" chains.
Ask first for everything else. Never archive CORE or `(PROTECTED)` sections.

Archiving = **move verbatim** into `CLAUDE-Archive.md` next to the target (Step 7), then remove from CLAUDE.md. The archive is never loaded automatically; it is searched with Grep when needed.

### Step 7: Archive File Handling

Archive file = `CLAUDE-Archive.md` in the **same folder as the target CLAUDE.md**.

```markdown
# CLAUDE.md Archive

Archived content from CLAUDE.md to maintain context efficiency.

---

## Archived: [DATE] ([short reason])

[Archived section content, verbatim]

---
```

If the archive exists: append a new dated block. Never edit older archive blocks.

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

Then suggest a CLAUDE.md only if the folder has its own working rhythm (code, infrastructure, own safety rules). Pure documentation folders get a `README.md` and a status block in the parent CLAUDE.md instead.

---

## CORE Sections (Never Suggest Archiving)

Adapt to the project's actual CLAUDE.md:

- `## Approach` / `## Philosophy` / `## Was ist dieses Projekt?`
- `## Paths` / `## Structure` / `## Dateien`
- `## Key References` / `## Links`
- `## Key Decisions` (the one-liners themselves; their long explanations are archivable)
- `## Key Patterns` / `## Conventions` / `## Stolpersteine`
- Safety-relevant sections
- Any section with `(PROTECTED` in the heading

Mark sections in CLAUDE.md with `(PROTECTED)` or `(ARCHIVABLE)` to steer this.

---

## Guidelines

- **Context efficiency is paramount.** Future sessions and subagents pay for every token.
- **Current state over history.** History belongs in session logs, the archive or notes.
- **Point, don't duplicate.** Reference files instead of copying content.
- **Respect existing format.** Match the CLAUDE.md style already in use.
- **Ask before archiving non-auto content.** User decides what's truly essential.

---

## Technical Constraints

- `AskUserQuestion`: max. **4 Optionen** pro Frage, max. **4 Fragen** pro Aufruf — mehr führt zu einem stillen Fehler
- Master dieser Datei: `PKM-Dirigent/_claude/commands/preserve.md`. Identische Kopien in den **5 aktiven Vaults** (`_claude/commands/`: Knowledge Base, Konstruktionsbüro Schmidl, PKM-Dirigent, Unterwegs, Work), in `PKM-Dirigent/Cross-Vault/_claude/commands/` (Root-Kopie, im `Obsidian-Vaults`-Root nur verlinkt) und gerätelokal in `~/.claude/commands/` — nach Änderungen alle Kopien per `cp` nachziehen und per MD5 prüfen.
- `/compact` ist ein eingebautes Kommando — `compact.md` existiert bewusst nicht
