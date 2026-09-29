---
context: conversation
description: Smart Conversation Compression with Session Logging
model: opus
allowed-tools: Read, Write, Bash, AskUserQuestion
---

# /compress - Smart Conversation Compression

Prepares preservation notes for conversation compaction AND saves the full session to searchable logs. Run this BEFORE `/compact`.

**Workflow:** `/preserve` (optional) → `/compress` → answer questions → session saved → `/compact` (always last)

## Instructions for Claude

When the user runs `/compress`, follow these steps:

### Step 1: Ask What to Preserve

Use the AskUserQuestion tool with the following multi-select question:

**Question:** "What would you like to preserve from this conversation?"

**Options (multi-select enabled, max 4):**
1. **Key Learnings & Solutions:** Technical insights, "aha" moments, code solutions, bug fixes, commands that worked
2. **Decisions Made:** Choices, trade-offs, why we chose X over Y
3. **Files, Config & Setup:** Files created/edited, environment setup, credentials, paths, configurations
4. **Pending Tasks, Errors & Workarounds:** Unfinished work, next steps, blockers, problems encountered and how they were solved

### Step 2: Ask for Custom Preservation (Optional)

**Contract:** Call AskUserQuestion with exactly 2 options. Do not add an "Other" option manually; the tool adds it automatically. No plain-text prompt is permitted. AskUserQuestion is always the entry point — the free-text path activates only after the tool renders, never instead of it.

Call AskUserQuestion with:
- **question:** "Anything specific you want to highlight or remember from this session?"
- **header:** "Custom note"
- **multiSelect:** false
- **options:**
  1. `{ label: "Skip", description: "No custom notes, continue with session log" }`
  2. `{ label: "Add a custom note", description: "Provide a custom note to preserve" }`

If the user selects "Skip", set custom notes to "None". If the user selects the auto-added free-text path and provides input, treat that input as the user's custom note verbatim.

### Step 3: Confirm Topic Name

**Contract:** Call AskUserQuestion with exactly 2 options. Do not add an "Other" option manually; the tool adds it automatically. No plain-text prompt is permitted. AskUserQuestion is always the entry point — the free-text path activates only after the tool renders, never instead of it.

First, analyse the conversation and derive a concise topic name (3-5 words, lowercase, hyphens) — e.g., `api-auth-refactor`.

Then call AskUserQuestion with:
- **question:** `Topic name for this session log: "{suggested-name}". Confirm or provide a different one?`
- **header:** "Topic name"
- **multiSelect:** false
- **options:**
  1. `{ label: "Accept: {suggested-name}", description: "Use the suggested topic name" }`
  2. `{ label: "Provide a different name", description: "Use a custom topic name instead" }`

Substitute `{suggested-name}` with the actual derived name. If the user selects "Accept", use the suggested name as-is. If the user selects the auto-added free-text path and provides input, treat that input as the chosen topic name (normalised to lowercase + hyphens).

### Step 4: Generate Session Log

Create the session log content with this structure:

```markdown
# Session Log: DD-MM-YYYY HH:MM - {Topic Name}

## Quick Reference (for AI scanning)
**Confidence keywords:** {extracted keywords from conversation}
**Projects:** {project names or references mentioned}
**Outcome:** {1-sentence outcome summary}

## Key Learnings & Solutions
- {Learning or solution 1}
- {Learning or solution 2}

## Decisions Made
- {Decision 1 with brief rationale}
- {Decision 2 with brief rationale}

## Files Modified & Config
- `{path/to/file}`: {what changed}
- {Config item if relevant}

## Pending Tasks & Errors
- {Pending item or blocker}
- {Error encountered and workaround}

## Key Exchanges
- {Notable exchange 1, brief summary}
- {Notable exchange 2, brief summary}

## Custom Notes
{User's custom notes from Step 2, or "None"}

---

## Quick Resume Context
{2-3 sentences that would help resume this work in a future session}

---

## Raw Session Log

{FULL CONVERSATION - Copy the entire conversation history here, preserving all user messages and assistant responses. This is the searchable archive.}
```

**IMPORTANT:** Only include sections the user selected in Step 1. Always include:
- Quick Reference (for AI scanning)
- Quick Resume Context
- Raw Session Log

### Step 5: Detect Project Root & Save

**Generate filename:**
```
DD-MM-YYYY-HH_MM-{topic-name}.md
```
Example: `05-03-2026-17_30-api-auth-refactor.md`

**Pick the target project (same rule as /preserve — not blindly the working directory):**

```
1. Collect the files this session created or changed.
2. From their common topic folder, walk UP to the first CLAUDE.md → project_root.
   (Projects without own CLAUDE.md belong to the parent CLAUDE.md's folder.)
3. No files changed (pure analysis/Q&A)? → walk up from pwd instead.
4. Several unrelated topics? → one log in the project with the most changes, plus a
   one-line pointer file in each other project's CC-Session-Logs/:
   {filename} containing only: "Siehe <path to main log> — <what concerned this project>"
5. If /preserve ran in this session, use the same target(s).
6. Session logs path: {project_root}/CC-Session-Logs/ (mkdir -p if missing)
```

Tell the user the chosen path(s) in the confirmation.

**Mask secrets before saving (mandatory):** The log is synced (Obsidian Sync, Git backup). Replace passwords, API keys, tokens, private keys, PINs and pre-shared keys in ALL sections, including the Raw Session Log, with `‹geheim: <what it was>›`. Keep non-secret identifiers (hostnames, IPs, IDs, ticket numbers). If a secret appeared in the conversation, add a Pending Task: "Secret X was exposed in chat — rotate".

**Save the session log:**
```bash
# Create folder if needed
mkdir -p "{project_root}/CC-Session-Logs/"

# Write session log
Write tool -> {project_root}/CC-Session-Logs/{filename}
```

### Step 6: Confirm and Instruct

Output confirmation:

```markdown
## Session Saved Successfully

### File Created

**Session Log:**
`{project_root}/CC-Session-Logs/{filename}`

### Session Summary
- **Project:** {project_root basename}
- **Topic:** {topic-name}
- **Sections preserved:** {list of selected sections}
- **Keywords:** {confidence keywords}

---

**Next step:** Run `/compact` to compress the conversation context (always last).

The session log is saved locally. Use `/resume` to load context from recent sessions.
```

---

## Guidelines

- **Be concise:** Each bullet should be actionable or informative
- **Use code blocks** for commands, paths, and code snippets
- **Include file paths** with line numbers where relevant
- **Preserve exact values:** Don't paraphrase IDs, paths or configs — but never credentials (mask them, see Step 5)
- **Link context:** If something depends on something else, note the relationship
- **Keep the summary short:** Everything above `## Raw Session Log` is what `/resume` reads — target ≤ 3 KB. Keywords max. ~25 terms on one line.
- **Full raw log:** The Raw Session Log must contain the COMPLETE conversation (secrets masked) for searchability
- **Log = history, CLAUDE.md = current state.** Don't repeat the log into CLAUDE.md; `/preserve` distils only the current state there.

---

## Confidence Keywords Extraction

When generating the "Confidence keywords" field, extract:
- Project names (my-api, user-dashboard)
- Technical terms (auth, middleware, migration, deploy)
- Action types (refactor, fix, create, update, delete)
- Tool/framework names (React, PostgreSQL, Docker)
- People mentioned (if relevant to decisions)
- Specific identifiers (issue numbers, ticket IDs)

These keywords enable the `/resume` skill to find relevant sessions via search.

---

## Example Output

```markdown
## Session Saved Successfully

### File Created

**Session Log:**
`/home/user/my-project/CC-Session-Logs/05-03-2026-17_30-api-auth-refactor.md`

### Session Summary
- **Project:** my-project
- **Topic:** api-auth-refactor
- **Sections preserved:** Decisions Made, Key Learnings, Files Modified
- **Keywords:** auth, JWT, middleware, refresh-tokens, session-management
```

---

## Technical Constraints

- `AskUserQuestion`: max. **4 Optionen** pro Frage, max. **4 Fragen** pro Aufruf — mehr führt zu einem stillen Fehler
- Master dieser Datei: `PKM-Dirigent/_claude/commands/compress.md`. Identische Kopien in den **5 aktiven Vaults** (`_claude/commands/`), in `PKM-Dirigent/Cross-Vault/_claude/commands/` und gerätelokal in `~/.claude/commands/` — nach Änderungen alle Kopien per `cp` nachziehen und per MD5 prüfen.
- Themenwechsel in einer Session: Thema A mit `/preserve` → `/compress` → `/compact` abschließen, dann Thema B. Für ein anderes Projekt mit eigener CLAUDE.md besser eine neue Session in dessen Ordner starten. Konzept: `PKM-Dirigent/Doku/CLAUDE.md-Konzept – Aufbau und Pflege.md`.
- `/compact` ist ein eingebautes Kommando — `compact.md` existiert bewusst nicht
