---
tags: [claude, workflow, meta]
created: 2026-08-08
modified: 2026-08-08
---

# Claude – Änderungshistorie

> Protokoll aller `.md`-Dokumentänderungen, die Claude **ohne Einzel-Rückfrage** vorgenommen hat. Einmal pro Woche vom User gesammelt geprüft und bestätigt oder einzeln zurückgerollt — statt bei jeder Änderung live nachzufragen. Vault-übergreifendes Prinzip, ausgerollt aus dem Knowledge-Base-Vault (2026-08-08).

---

## 1. Ziel & Prinzip

Bisher fragte Claude vor praktisch jeder inhaltlichen Textänderung an einer bestehenden Notiz einzeln nach Bestätigung. Statt jede Änderung einzeln freizugeben, trägt Claude sie hier ein — der User sichtet die Tabelle **einmal pro Woche**, bestätigt sie pauschal oder verwirft einzelne Zeilen per Obsidian-Sync-Versionshistorie.

Technisch umgesetzt über `.claude/settings.json` (Vault-Root, checked-in): `Edit(**/*.md)` und `Write(**/*.md)` sind als Permission-Regel automatisch erlaubt — nur für `.md`-Dateien, alle anderen Tools (Bash, Settings selbst) bleiben normal bestätigungspflichtig.

## 2. Was läuft ohne Rückfrage, was nicht

**Ohne Einzel-Rückfrage (nur protokollieren):**
- Inhaltliche Ergänzungen, Korrekturen, Umformulierungen in bestehenden `.md`-Notizen
- Frontmatter-Pflege (`modified`-Bump, Tags)
- Neue Notizen anlegen inkl. Verlinkung in Index-Dateien (README.md, Sammlungs-Übersichten)
- Umbenennen/Verschieben von `.md`-Notizen (mit Link-Fix, siehe Ablauf unten)
- **Ausgenommen:** die „drei Stellen synchron halten"-Regel für GPX-Sammlungen (Sammlungs-Übersicht, Archiv-README, CLAUDE.md-Statistik, siehe Root-CLAUDE.md) bleibt unverändert Pflicht — sie ist kein Rückfrage-Thema, sondern eine inhaltliche Konsistenzregel

**Weiterhin Rückfrage nötig:**
- Löschen von Dateien
- Strukturelle Auffälligkeiten in bestehenden Notizen — erst klären, nicht still bereinigen
- Alles außerhalb von `.md`-Notizen (GPX-Dateien, Attachments, Settings)
- Destruktive oder schwer umkehrbare Aktionen generell (Systemprompt-Vorgabe „Executing actions with care")

### Ablauf beim Umbenennen/Verschieben

1. Alle eingehenden Wikilinks per Grep finden.
2. Datei verschieben/umbenennen, danach Links fixen.
3. Unter Windows kann `mv`/Rename bei aktivem Obsidian Sync mit „in use/busy" scheitern — `robocopy /MOVE` als Workaround.
4. Änderung mit altem + neuem Pfad und Anzahl gefixter Links in die Tabelle eintragen.

**Bewusste Einschränkung:** Für den eigentlichen Verschiebe-Befehl gibt es **keine** automatische Bash-Freigabe (Begründung: pauschale `mv`-Freigabe wäre nicht auf `.md`/den Vault beschränkbar und über Befehlsverkettung riskant) — ein einzelner technischer Bestätigungsklick dafür ist kein Rückfragen im inhaltlichen Sinn.

## 3. Tabellenformat

| Datum | Dokument | Änderung | Session/Kontext | Status |
|---|---|---|---|---|
| YYYY-MM-DD | [[Wikilink]] | Kurzbeschreibung (1 Zeile) | Kurzkontext | 🟡 offen |

- **Status:** 🟡 offen → 🟢 bestätigt (nach Wochen-Review) bzw. 🔴 verworfen → Zeile wandert ins Archiv (Abschnitt 5)
- Neue Einträge werden **oben** in der aktuellen Tabelle (Abschnitt 6) ergänzt (neueste zuerst)

## 4. Wochen-Workflow

1. Claude trägt laufend jede autonome Änderung in die Tabelle „Offene Änderungen" (Abschnitt 6) ein.
2. Einmal pro Woche sichtet der User die Tabelle.
3. Pauschale Bestätigung: Zeilen wandern gesammelt ins Wochen-Archiv (Abschnitt 5), Tabelle in Abschnitt 6 wird geleert.
4. Einzelne unerwünschte Änderung: über Obsidian-Sync-Dateiversionen zurückrollen, Zeile trotzdem als „🔴 verworfen" ins Archiv.

## 5. Archiv (bestätigte/verworfene Wochen)

_Noch keine abgeschlossene Woche._

## 6. Offene Änderungen (aktuelle Woche)

| Datum | Dokument | Änderung | Session/Kontext | Status |
|---|---|---|---|---|
| 2026-08-10 | [[CLAUDE]] | GPX-Archiv-Baum + Statistik: Normandie-Sammlung ergänzt (286→336 Rother-Touren, Gesamt 392→442) | Nachtrag fehlende Rother-Sammlung „Normandie" (5. Aufl., 50 GPX) | 🟡 offen |
| 2026-08-10 | [[Wanderungen/Archiv (OneDrive)/README]] | Statistik-Tabelle + Sammlungs-Sektion „Rother Wanderführer": Normandie ergänzt (286→336, Gesamt 392→442) | Nachtrag fehlende Rother-Sammlung „Normandie" | 🟡 offen |
| 2026-08-10 | [[Wanderungen/Archiv (OneDrive)/Rother-Übersicht]] | Bände-Tabelle + Dateistruktur: Normandie-Zeile ergänzt (286→336 Touren) | Nachtrag fehlende Rother-Sammlung „Normandie" | 🟡 offen |
| 2026-08-10 | [[Wanderungen/Archiv (OneDrive)/Rother-Normandie-Übersicht]] | Neue Notiz angelegt: Tourenliste (50 Stück) nach Vorlage der übrigen Rother-Bände | Nachtrag fehlende Rother-Sammlung „Normandie" | 🟡 offen |
| 2026-08-10 | [[Wanderungen/Archiv (OneDrive)/Einzeltouren-Übersicht]] | Fehlende Tour „Erquy (10,4 km)" ergänzt (Nr. 8, Folgezeilen umnummeriert), Zähler 40→41 | Nachtrag fehlende Einzeltour „Erquy"; Gesamt-Statistik in README + CLAUDE.md ebenfalls angepasst (443 GPX) | 🟡 offen |

---

**Zuletzt aktualisiert:** 2026-08-08
