---
tags:
  - claude
  - workflow
  - meta
created: 2026-08-08
modified: 2026-08-08
---

# Claude – Änderungshistorie

> Protokoll aller `.md`-Dokumentänderungen, die Claude **ohne Einzel-Rückfrage** vorgenommen hat. Einmal pro Woche vom User gesammelt geprüft und bestätigt oder einzeln zurückgerollt — statt bei jeder Änderung live nachzufragen. Vault-übergreifendes Prinzip, ausgerollt aus dem Knowledge-Base-Vault (2026-08-08).

---

## 1. Ziel & Prinzip

Bisher fragte Claude vor praktisch jeder inhaltlichen Textänderung an einer bestehenden Notiz einzeln nach Bestätigung. Statt jede Änderung einzeln freizugeben, trägt Claude sie hier ein — der User sichtet die Tabelle **einmal pro Woche**, bestätigt sie pauschal oder verwirft einzelne Zeilen. Sicherheitsnetz: `obsidian-git` committed/pusht alle 30 Min. nach `github.com/schmimat/Obsidian-Urlaub` — jede Änderung ist über die Git-Historie rückgängig machbar.

Technisch umgesetzt über `.claude/settings.json` (Vault-Root, checked-in): `Edit(**/*.md)` und `Write(**/*.md)` sind als Permission-Regel automatisch erlaubt — nur für `.md`-Dateien, alle anderen Tools (Bash, Settings selbst) bleiben normal bestätigungspflichtig.

## 2. Was läuft ohne Rückfrage, was nicht

**Ohne Einzel-Rückfrage (nur protokollieren):**
- Inhaltliche Ergänzungen, Korrekturen, Umformulierungen in bestehenden `.md`-Notizen
- Frontmatter-Pflege (`modified`-Bump, Tags)
- Neue Notizen anlegen inkl. Verlinkung in Index-Dateien (README.md)
- Umbenennen/Verschieben von `.md`-Notizen (mit Link-Fix, siehe Ablauf unten)

**Weiterhin Rückfrage nötig:**
- Löschen von Dateien
- Strukturelle Auffälligkeiten in bestehenden Notizen — erst klären, nicht still bereinigen
- Alles außerhalb von `.md`-Notizen: Settings/Permissions, Plugin-Konfiguration
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
4. Einzelne unerwünschte Änderung: über `git log`/`git revert` (GitHub-Historie) oder Obsidian-Sync-Dateiversionen zurückrollen, Zeile trotzdem als „🔴 verworfen" ins Archiv.

## 5. Archiv (bestätigte/verworfene Wochen)

_Noch keine abgeschlossene Woche._

## 6. Offene Änderungen (aktuelle Woche)

| Datum | Dokument | Änderung | Session/Kontext | Status |
|---|---|---|---|---|
| _(noch keine Einträge)_ | | | | |

---

**Zuletzt aktualisiert:** 2026-08-08
