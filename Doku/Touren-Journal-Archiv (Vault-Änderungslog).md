---
title: "Journal – Vault-Änderungen"
created: 2026-05-28
modified: 2026-05-28
tags:
  - journal
  - log
  - tagebuch
type: "Log"
---

# 📅 Journal – Vault-Änderungen

Persönliches Tagebuch für Änderungen und Arbeiten am Touren Vault. Manuelle Notizen zu den durchgeführten Arbeiten pro Tag.

---

## 2026-05-28 · Mittwoch

### 🎯 Was gemacht wurde:

**Einzeltouren-Sammlung erweitert:**
- 2 neue Touren hinzugefügt: **Eben-Emael (Belgien)** – grüne Route (6,3 km) und rote Route (9,1 km)
- Beide Touren starten vom Fort Eben-Emael (UNESCO-Kriegsdenkmal nahe Lüttich)

**Dokumentation aktualisiert:**
- `Einzeltouren-Übersicht.md` → 36 Touren → **38 Touren**
- `README.md` (Archiv) → Gesamt 388 GPX → **390 GPX**
- CLAUDE.md → Statistiken + neuer Workflow-Guide für künftige Touren
- `.claude/vault-journal.md` → technisches Änderungsjournal erstellt

**Erkenntnisse:**
- Neue Region Belgien hinzugekommen (erste belgische Touren!)
- Wichtiger Lernpunkt: Tabellen-Umnummerierung muss in **einem** Edit-Durchlauf erfolgen, sonst entstehen Duplikate

---

## 2026-05-15 · Mittwoch

### 🎯 Was gemacht wurde:

**Archiv-Struktur dokumentiert und verifiziert:**
- GPX-Archiv vollständig auf OneDrive synchronisiert
- 5 Sammlungen katalogisiert und übersichtlich dokumentiert:
  - Einzeltouren (36 deutsche Touren)
  - Komoot (25 internationale Touren)
  - Rother Wanderführer (286 Touren in 5 Unterordnern)
  - Vergessene Pfade Fränkische Schweiz (41 Touren)
  - Sonstige: Maastricht Stadtrundgänge (3 GPX)

**Dokumentation erstellt:**
- `README.md` (Archiv-Übersicht mit Statistik-Tabelle)
- Einzel-Übersichten für jede Sammlung (6 Dateien)
- CLAUDE.md: Archiv-Struktur + Frontmatter-Template + Fallstricke

**Gesamt:** 388 GPX-Dateien inventarisiert

**Wichtige Erkenntnisse / Notizen:**
- Archiv-Ordner heißt `Archiv (OneDrive)` mit Klammern und Leerzeichen — kritisch!
- Lange Komoot-Dateinamen können bei PowerShell `Copy-Item` fehlschlagen
- BRouter-GPX-Files enthalten Metadaten im XML-Kommentar (Zeile 2)
- Rother-Sammlung ist größte Sub-Sammlung (286 Touren)

---

## 2026-04-20 · Sonntag

### 🎯 Was gemacht wurde:

**Touren-Sammlungen von OneDrive importiert:**
- Alle GPX-Dateien aus `C:\Users\matth\OneDrive\Touren\` in Vault kopiert
- Ordnerstruktur erstellt: `Wanderungen/Archiv (OneDrive)/`
- 5 Untersammlungen angelegt:
  - `Einzeltouren/` (36 GPX)
  - `Komoot/` (25 GPX)
  - `Rother Wanderführer/` (286 GPX + 5 Unterordner)
  - `Vergessene Pfade Fränkische Schweiz/` (41 GPX)
- Symbole/Icons für Sammlungen festgelegt (🇩🇪, 🎽, 🥾, 📖, etc.)

**Wichtige Erkenntnisse / Notizen:**
- Gesamt: 388 GPX-Dateien (+ 3 separate Maastricht-GPX)
- PowerShell-Schleife notwendig für große Datenmengen
- Windows-Pfadlängen beachten (>260 Zeichen problematisch)
- Locus-Ordner enthält nur Kartendaten, keine GPX-Dateien

---

## 2026-02-01 · Montag

### 🎯 Was gemacht wurde:

**Touren Vault erzeugt und initialisiert:**
- Neues Obsidian Vault angelegt: `C:\Users\matth\Obsidian-Vaults\Touren`
- Grundstruktur erstellt:
  - `Wanderungen/` — Zentrale Sammlung
  - `Stadtrundgänge/` — Dokumentierte Stadtrundgänge
  - `Regionen/` — Regionale Informationen
  - `Planung/` — Reisepläne
  - `Ressourcen/` — Externe Links, Tipps, Checklisten
  - `Erfahrungen/` — Reiseberichte und Fotos
  - `Attachments/` — Bilder und Multimedia

**Dokumentation erstellt:**
- CLAUDE.md: Projekt-Anleitung für Claude Code
- README.md (Wanderungen): Übersicht
- Notizen-Konventionen festgelegt (Frontmatter, Wikilinks, Emojis)

**Wichtige Erkenntnisse / Notizen:**
- Vault ist **Wissensdatenbank**, keine Software
- Alle Inhalte auf Deutsch
- Wiki-Links ohne Dateierweiterungen verwenden
- Frontmatter mit Metadaten (tags, region, difficulty, duration)
- Obsidian Sync / NextCloud / WebDAV für Synchronisation konfiguriert

---

## Notizen zum Format

- **Datum:** `YYYY-MM-DD · Wochentag`
- **Was gemacht wurde:** Kurze, prägnante Zusammenfassung
- **Dateien betroffen:** Welche .md-Dateien wurden geändert?
- **Erkenntnisse:** Was habe ich gelernt? Besonderheiten? Fallstricke?

Dieses Journal dient zur **freien Dokumentation** der täglichen Arbeiten am Vault. Für technische Details siehe: [[.claude/vault-journal.md]]

---

*Letzter Eintrag: 2026-05-28*
