---
tags:
  - claude
  - projekt
created: 2026-08-10
modified: 2026-08-10
---

# CLAUDE.md — Unterwegs-Vault

Projekt-Instruktionen für Claude Code beim Arbeiten im Unterwegs-Vault.

## Was ist dieses Vault?

Neuer Vault als Merge von `Urlaub` + `Touren` (beide LXC-203-Geschwister-Ordner) — Reiseplanung, Wanderungen, Stadtrundgänge, Sehenswürdigkeiten und ein geplantes Urlaubstagebuch, das die anderen Kategorien direkt verlinken kann (Hauptgrund für den Merge: Cross-Vault-Wikilinks funktionieren in Obsidian nicht). Details zur Entscheidungsfindung: `memory/project-unterwegs-vault-struktur.md` und `memory/project-touren-vault-soll-git-bekommen.md` im Cross-Vault-Root (`/home/claude/Obsidian-Vaults`).

**Status (2026-08-10):** Vault-Shell (Task #3), Claude-Vorbereitung + Plugins (Task #6), Content-Migration (Task #4) und Link-/Konventions-Fixes (Task #5) abgeschlossen — Inhalte aus `Urlaub/` und `Touren/` sind als **Kopie** übernommen, die Quell-Vaults bleiben bis zur vollständigen Verifikation unangetastet (Rollback-Sicherheit). Die vault-präfixierten Excalidraw-/README-Pfade (`Touren/Wanderungen/…`, `Touren/Stadtrundgänge/…`) sind auf die neue Vault-Struktur (`Wanderungen/…`, `Stadtrundgänge/…`) korrigiert. Noch offen: `Regionen/` ist ein neues Organisationskonzept ohne Vorlage in den Quell-Vaults und noch nicht angelegt; uneinheitliches Frontmatter-Schema zwischen `Wanderungen`/`Stadtrundgänge`/`Übernachtungen` (`tags`/`created`/`modified`) und `Einpacklisten` (`title`/`erstellt`/`reise`/`zeitraum`) ist erkannt, aber noch nicht vereinheitlicht; zwei tote Wikilinks in `Stadtrundgänge/README.md` (`Maastricht - Kurztour (2-3h)`, `Maastricht - Altstadt Highlights` ohne „mit Epochen"-Suffix) zeigen auf nicht existierende Dateien — vermutlich bereits vor dem Merge in Touren kaputt, nicht migrationsbedingt.

## Geplante Vault-Struktur (Zielbild, noch nicht umgesetzt)

```
Unterwegs/
├── Reisen/<Reisename>/{<Reisename>.md, Tagebuch/YYYY-MM-DD.md}
├── Wanderungen/            (1:1 aus Touren, inkl. GPX-Archiv)
├── Stadtrundgänge/          (1:1 aus Touren)
├── Sehenswürdigkeiten/       (ex-Ausflüge aus Urlaub)
├── Übernachtungen/            (aus Urlaub)
├── Einpacklisten/               (aus Urlaub)
├── Regionen/                     (Bindeglied Reise ↔ Wanderung/Stadtrundgang)
├── Ressourcen/ · Clippings/ · Doku/   (aus beiden zusammengeführt)
├── _template/
├── _Wohnwagen-Technik/              (Sackmarkise/, Wohnwagen-*.md — eigener Unterordner)
└── OneNote-Archiv/                   (1:1 aus Urlaub)
```

Leitprinzip: Wanderungen/Stadtrundgänge/Sehenswürdigkeiten bleiben eigenständiges, wiederverwendbares Wissen — ziehen NICHT in Reise-Unterordner um. Vollständiger Entwurf inkl. Tagebuch-Frontmatter: `memory/project-unterwegs-vault-struktur.md`.

**Migrations-Herkunft der Ordner (2026-08-10):**

| Ordner | Quelle | Hinweis |
|---|---|---|
| `Wanderungen/`, `Stadtrundgänge/`, `_template/`, `Ressourcen/` | Touren, 1:1 | GPX-Archiv vollständig (477 Dateien verifiziert) |
| `Clippings/`, `Doku/` | Touren + Urlaub, zusammengeführt | `Doku/Claude – Änderungshistorie.md` neu begonnen, alte Verläufe als `Claude – Änderungshistorie (Archiv Touren/Urlaub).md` archiviert |
| `Übernachtungen/`, `Einpacklisten/` | Urlaub, 1:1 | |
| `_Wohnwagen-Technik/` | Urlaub (`Sackmarkise/` + `Wohnwagen-*.md`) | |
| `Sehenswürdigkeiten/`, `Reisen/`, `OneNote-Archiv/` | Urlaub (`Ausflüge/`, `Reisen/`, `OneNote-Archiv/`) | Quellordner waren bereits leer, nur Zielordner angelegt |
| `Regionen/` | — | Neu, noch nicht angelegt (kein Vorbild in den Quell-Vaults) |

**Bewusst nicht migriert:** `Urlaub/thumbnails/` (Plugin-Cache, regeneriert sich selbst), `Urlaub/Recherchen/` (leer), `README.md`/`CLAUDE.md`/`Willkommen.md`/`start-claude.ps1` beider Quell-Vaults (vault-spezifische Meta-Dateien, durch Unterwegs' eigene ersetzt).

## Autonomes Editieren: Änderungshistorie statt Rückfrage

Für **inhaltliche Änderungen an `.md`-Notizen** (Text, Frontmatter-Updates, neue Notizen inkl. Index-Verlinkung, Umbenennen/Verschieben inkl. Link-Fix) fragst du **nicht** mehr einzeln nach Bestätigung — `.claude/settings.json` erlaubt `Edit`/`Write` auf `*.md` bereits automatisch. Stattdessen trägst du jede Änderung in [[Doku/Claude – Änderungshistorie]] ein; der User bestätigt/verwirft wöchentlich gesammelt.

**Ausnahmen (weiterhin Rückfrage nötig):** Löschen von Dateien, strukturelle Auffälligkeiten, alles außerhalb von `.md`. Für den eigentlichen Verschiebe-Befehl (`mv`/Bash) gibt es bewusst keine automatische Freigabe.

## Sprache & Stil

- **Deutsch** für alle Inhalte (englische Fachbegriffe wie Plugin/Sync bleiben)
- Wikilinks `[[Notiz-Name]]` ohne `.md`-Endung
- Frontmatter mit `tags`, `created`, `modified` (bei Bearbeitung `modified` auf heute bumpen); Touren-Vokabular (`region`, `difficulty`, `duration`) für Wanderungen/Stadtrundgänge übernehmen

## Sync & Backup

Läuft über das Container-201/203-Sync+Git-Backup-Muster (`obsidian-sync-unterwegs.service` auf 201+203, `git-backup-unterwegs.timer` auf 201 → Repo `Obsidian-Unterwegs`) — **nicht** über das lokale `obsidian-git`-Plugin (das ist projektweit seit 2026-08-04 deaktiviert). Details: `Knowledge Base/IT@home/Aufgaben/Aufgabe – Vault Unterwegs auf 201 und 203 einrichten.md`.

## Plugins

Übernommen aus `Urlaub`/`Touren` (Plugin-Code kopiert, `data.json` bewusst nicht mitgenommen — startet mit Standardeinstellungen):

| Plugin | Zweck |
|--------|-------|
| `calendar` | Kalenderansicht für Tagesnotizen |
| `colored-tags` | Farbige Tags |
| `drawio-editor` | Draw.io-Diagramme einbetten/bearbeiten |
| `featured-image` | Automatisches Titelbild aus erstem Bild/YouTube-Link |
| `notebook-navigator` | Zwei-Spalten-Dateiexplorer mit Tag-Browsing |
| `obsidian-excalidraw-plugin` | Skizzen, handgezeichnete Karten |
| `obsidian-map-view` | Interaktive Karte für Übernachtungen/Routen/Sehenswürdigkeiten |
| `obsidian-outliner` | Listen wie in Workflowy/Roam |
| `obsidian-style-settings` | Theme/Plugin-CSS-Einstellungen |
| `pixel-perfect-image` | Bild-Resizing, Copy/Open im Explorer |
| `settings-search` | Globale Einstellungssuche |
| `tag-wrangler` | Tags umbenennen/mergen/durchsuchen |

Bewusst **nicht** übernommen: `obsidian-git` (projektweit seit 2026-08-04 deaktiviert, Backup läuft über `git-backup-unterwegs.timer` auf Container 201), `drawio`/`drawio-obsidian` (redundant zu `drawio-editor`), `obsidian-local-rest-api` (unvollständig installiert in Touren, keine `manifest.json`), `obsidian42-brat` (User-Entscheidung 2026-08-10).

**Hinweis:** Wie bei `Touren`/`Urlaub` fehlt auf diesem 203-Sync-Spiegel eine `.obsidian/community-plugins.json` (vermutlich von der Obsidian-Sync-Config ausgeschlossen, da reiner Client-UI-Zustand). Der Plugin-**Code** liegt bereit; ob die Plugins auf einem Client (z. B. ThinkPad X1) automatisch aktiviert sind oder dort einmalig manuell über Einstellungen → Community-Plugins eingeschaltet werden müssen, ist von hier aus nicht verifizierbar.

## Wichtige Dateien & Ordner

| Pfad | Inhalt |
|------|--------|
| `CLAUDE.md` | Diese Datei |
| `CC-Session-Logs/` | Session-Logs (via `/compress` + `/preserve`) |
| `_claude/` + `.claude` (Symlink) | cpr-Skills (`/compress`, `/preserve`, `/resume`) |
| `Doku/Claude – Änderungshistorie.md` | Protokoll autonomer `.md`-Änderungen (wöchentliche Sammelbestätigung) |
| `Doku/Claude – Änderungshistorie (Archiv Touren/Urlaub).md` | Änderungshistorien der Quell-Vaults bis zum Merge-Zeitpunkt |

## Arbeitsweise mit Claude Code

- Sessions mit `/resume` starten — lädt Session-History
- Mit `/preserve` am Ende speichern
- Session-Logs via `/compress` anlegen, danach `/compact` (eingebaut, kein Skill)

> **cpr-Skill-Pflege:** `/compress` und `/preserve` liegen jetzt in **8 Kopien** (6 ursprüngliche Vaults + Cross-Vault-Root + Unterwegs) — Änderungen synchron in allen 8 nachziehen.

---

**Zuletzt aktualisiert:** 2026-08-10
**Status:** Tasks #3, #4, #5, #6 abgeschlossen; offen: `Regionen/`-Konzept, Frontmatter-Vereinheitlichung, zwei vorbestehende tote Links in `Stadtrundgänge/README.md`, Mehrgeräte-Rollout (Task #7), Cross-Vault-Meta-Update (Task #8), Stilllegung Urlaub/Touren (Task #9)
