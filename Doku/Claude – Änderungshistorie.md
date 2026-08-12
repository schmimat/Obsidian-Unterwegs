---
tags: [claude, workflow, meta]
created: 2026-08-10
modified: 2026-08-12
---

# Claude – Änderungshistorie

> Protokoll aller `.md`-Dokumentänderungen, die Claude **ohne Einzel-Rückfrage** vorgenommen hat. Einmal pro Woche vom User gesammelt geprüft und bestätigt oder einzeln zurückgerollt — statt bei jeder Änderung live nachzufragen. Vault-übergreifendes Prinzip, ausgerollt aus dem Knowledge-Base-Vault (2026-08-08).

> **Vorgeschichte:** Dieser Vault entstand am 2026-08-10 durch Merge von `Urlaub` + `Touren`. Die Änderungshistorien beider Quell-Vaults bis zum Merge-Zeitpunkt liegen als Archiv daneben: [[Claude – Änderungshistorie (Archiv Touren)]], [[Claude – Änderungshistorie (Archiv Urlaub)]]. Diese Datei beginnt frisch ab dem Merge.

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
| 2026-08-12 | [[../Wanderungen/Archiv (OneDrive)/Rother-Bretagne-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-CinqueTerre-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Daenemark-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Neapel-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Mallorca-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Normandie-Übersicht]] | Je Region eine `mapview`-Übersichtskarte ergänzt (`path:"<Kürzel>_"`-Query, z. B. `path:"Bret_"` für alle 51 Bretagne-Touren) — zeigt alle Touren der Region auf einer Karte statt 336 Einzel-Embeds; einzelne GPX-Downloadlinks in den Tabellen unverändert gelassen (Referenz-Archiv, kein Einzel-Embed pro Zeile nötig) | User-Auftrag „eine Übersichtskarte pro Region", direkte Fortsetzung der GPX/Map-View-Korrektur bei den Maastricht-Notizen | 🟡 offen |
| 2026-08-12 | [[../Ressourcen/GPX-Setup-Anleitung]], [[../Ressourcen/GPX-Verwaltung]] | Falsche `mapview`-Codeblock-Syntax korrigiert: `{"geoDataUrl": "..."}`/`{"coordinates": [...], "zoom": ...}` existieren im Map-View-Plugin nicht (im Quellcode verifiziert, `src/main.ts`/`src/mapState.ts` — echte Felder sind `query`/`mapZoom`/`mapCenter`/`autoFit`, GPX-Datei über `path:`-Query-Operator ansprechen) | User fragte, warum ein GPX-Wikilink auf Android die Datei statt der Karte öffnet — Recherche ergab: keine Notiz im Vault hatte je einen funktionierenden Embed, weil die dokumentierte Syntax nie existiert hat | 🟡 offen |
| 2026-08-12 | [[../Stadtrundgänge/Maastricht/Maastricht - Kurztour (2-3h) - mit Epochen]], [[../Stadtrundgänge/Maastricht/Maastricht - Langtour (5-6h) - mit Epochen]], [[../Clippings/Rund um Kornelimünster]] | Funktionierenden `mapview`-Codeblock (korrekte Syntax, s.o.) ergänzt — Langtour hatte zuvor gar keinen GPX-Abschnitt im Fließtext, nur Frontmatter | Gleicher Kontext wie oben — Fix auf alle 3 Notizen mit tatsächlich vorhandener GPX-Datei ausgeweitet | 🟡 offen |
| 2026-08-12 | [[../Stadtrundgänge/Maastricht/Maastricht - Highlights (3-4h) - mit Epochen]], [[../Ressourcen/GPX-Verwaltung]] | Toten Verweis auf nicht existierende `Maastricht-Route.gpx` entfernt: `gpx_file`-Frontmatter in der Highlights-Notiz gelöscht, stattdessen Platzhalter-Abschnitt „Route fehlt noch" (inerter Beispiel-Codeblock zum späteren Nachtragen) eingefügt; Tabellenzeile + Ordnerstruktur in `GPX-Verwaltung.md` auf „⏳ Route fehlt noch" korrigiert | User-Bestätigung „Route fehlt noch, Notiz und Tabelle bitte anpassen" | 🟡 offen |
| 2026-08-11 | [[../CLAUDE.md]] | Plugins-Abschnitt aktualisiert: Fehlender Plugin-Code auf X1 gefunden, Root Cause geklärt (`community-plugin`-Kategorie fehlte seit Erstinstallation in `ob sync-config` auf 201/203) und per Live-Fix auf beiden Containern behoben — X1 hat jetzt alle 12 Plugin-Ordner lokal, `Fully synced` verifiziert | Knowledge-Base-Session, User bat um Prüfung + Nachtrag, dann nach Screenshot um Config-Check auf 201/203 „siehe auch alle andere Vaults" → Fix auf alle 7 Vaults ausgeweitet | 🟢 bestätigt |
| 2026-08-11 | [[../.obsidian/community-plugins.json]] (kein `.md`), [[../CLAUDE.md]] | 11 von 12 Plugins auf X1 aktiviert (`community-plugins.json` geschrieben + Obsidian komplett neu gestartet, User bestätigte Neustart); `settings-search` als leerer/unvollständiger Plugin-Ordner auf 203 entdeckt | User-Auftrag „Plugins auf X1 unter Community-Plugins aktivieren" | 🟢 bestätigt |
| 2026-08-11 | [[../CLAUDE.md]] (Status-Zeilen, Task #9 abgeschlossen) | Touren + Urlaub archiviert nach User-Bestätigung „Unterwegs ist verifiziert": Container-201-Kopien read-only + umbenannt, 203 bereinigt, beide GitHub-Repos vom User manuell archiviert (kein `gh`-CLI/Token verfügbar) — Task #9 vollständig abgeschlossen | User-Auftrag „archiviere Touren und Urlaub im Github und nur auf 201 als lokaler Ordner aber ro und mit verändertem Namen", Bestätigung „Erledigt, beide archiviert" | 🟢 bestätigt |
| 2026-08-11 | [[../CLAUDE.md]] (Plugin-Tabelle + Root-Cause-Absatz) | Zusatzbefund per User-Screenshot: `settings-search` v1.3.10 vault-übergreifend inkompatibel mit Obsidian 1.13.6 (Update durch vorherigen Neustart ausgelöst) — betraf `Touren`/`Knowledge Base`, nicht direkt `Unterwegs` (hier nie vollständig installiert). Auf User-Entscheidung „überall deinstallieren" hin in `Touren`/`Knowledge Base` entfernt (nicht in diesem Vault, da hier ohnehin nicht funktionsfähig vorhanden); Tabelle hier bereinigt | User-Auftrag „Plugin überall deinstallieren" | 🟢 bestätigt |

---
