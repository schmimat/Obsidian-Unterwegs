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
| 2026-08-17 | `Reise-Guides/Le Havre/*.mp3` (14 Audiodateien, kein `.md`) | TTS-Erzeugung abgeschlossen: alle 14 Stationstexte per OpenAI-API (`tts-1-hd`, Stimme `onyx`) in mp3 umgewandelt, 19.680 Zeichen gesamt, Kosten ca. 0,59 $. Erster Durchlauf scheiterte komplett an `insufficient_quota` (Account ohne Guthaben), nach Guthaben-Hinterlegung durch den User zweiter Durchlauf erfolgreich (12/14 direkt, 2/14 nach kurzem DNS-Aussetzer im zweiten Anlauf) — alle 14 Dateien per Größencheck verifiziert (keine 0-Byte-Datei). API-Key wurde vom User im Chat eingefügt; nur transient als Env-Var verwendet, nirgends in eine Vault-Datei geschrieben — User auf das Risiko hingewiesen, dass ein künftiges `/compress` dieser Session den Key sonst in den rohen Session-Log schreiben und darüber ins `Obsidian-Unterwegs`-GitHub-Repo gelangen könnte; Empfehlung, den Key sicherheitshalber zu rotieren | User-Auftrag „Guthaben leg ich gleich auf, mach mit Option 1 weiter" / „Ist hinterlegt" | 🟡 offen |
| 2026-08-17 | `Reise-Guides/Le Havre/` (umbenannt/verschoben von `Le-Havre-Audioguide/`, eigenständiges Vault außerhalb von `Unterwegs`, kein `.md` in diesem Vault selbst betroffen — reiner Ordner-Move), [[../Aufgaben/Aufgabe – Audio-Guide Le Havre erstellen (LXC 203)]] | User-Entscheidung: Bereitstellung läuft jetzt über **Obsidian Publish mit Passwortschutz** statt Obsidian Sync (Grund: Sync teilt ganze Vaults ohne Read-only-Rolle, Publish erlaubt Passwortschutz ohne Obsidian-Account für die Ehefrau). Deshalb Vault von `Le-Havre-Audioguide/` auf generisches `Reise-Guides/` umbenannt (Le Havre als erster Unterordner, künftige Ausflüge können weitere Unterordner werden) und nach `Reise-Guides/Le Havre/` verschoben. Aufgaben-Notiz entsprechend aktualisiert (Abschnitte 1/3.1/3.6/4/5/6, Tags, `bearbeiter`-Feld) — `ob publish-*`-Befehle auf 203 verifiziert vorhanden, Publish-Einrichtung selbst noch offen (Kosten/Passwort/Teilveröffentlichung erst mit User klären) | User-Auftrag „Wir machen es über Obsidian Publish mit Passwortschutz. Dann muss der Vault aber anders heißen." + Folgefrage zum Namen | 🟡 offen |
| 2026-08-17 | `Le-Havre-Audioguide/` → siehe Zeile oben, umbenannt (14 Notizen `0000 - Einführung.md` bis `0013 - MuMa.md`, kein `.md` in diesem Vault) | Erste Hälfte der Aufgabe „Audio-Guide Le Havre" abgearbeitet: neues Vault unter `/home/claude/Obsidian-Vaults/Le-Havre-Audioguide/` angelegt (Konvention `~/Obsidian-Vaults/<VaultName>/` aus LXC-201-Vault-Sync-Notiz verifiziert), 14 deutsche Fließtexte (150–330 Wörter, je 1–2 Min. Sprechzeit) geschrieben. Vertiefte Websuche für alle Stationen durchgeführt; die 3 ⚠️-markierten Punkte aus der Aufgabe verifiziert und korrigiert: Maison de l'Armateur (Baujahr ~1790, Bauherr Paul Michel Thibault, 1800 an Reeder Martin Pierre Foäche verkauft — Sklavenhandel-Kontext des Havrer Reederbürgertums vorsichtig eingeordnet statt verschwiegen), Le Volcan (Behauptung „einziges Niemeyer-Bauwerk in Frankreich" widerlegt — Niemeyer baute im Exil auch den PCF-Sitz in Paris und die Bourse du Travail in Bobigny, im Text richtiggestellt), Avenue Foch (80 m breit bestätigt, tatsächlich 10 m breiter als die Champs-Élysées mit 70 m). Noch **nicht** erledigt: 14 mp3-Dateien (TTS-Erzeugung wartet auf Klärung des API-Keys mit dem User), Sync-Einrichtung auf 201/203 | Direkte Fortsetzung der Aufgaben-Notiz; erster Websuche-Fork lieferte laut User-Rückmeldung nur eine Zwischenmeldung statt echter Recherche — Recherche danach direkt im Hauptthread per WebSearch nachgeholt | 🟡 offen |
| 2026-08-17 | [[../Aufgaben/Aufgabe – Audio-Guide Le Havre erstellen (LXC 203)]] (neu), neuer Ordner `Aufgaben/` (Erstanlage in diesem Vault) | Auf User-Auftrag ausformulierte Aufgabe für Claude Code auf LXC 203 angelegt: Audio-Guide-Vault (14 Stationen 0000–0013, TTS via OpenAI-API, Bereitstellung über bestehende Obsidian-Sync-Infrastruktur statt Web-Tunnel) — nach dem in `Knowledge Base/IT@home/Aufgaben/` etablierten Format (Frontmatter `type: Arbeitsauftrag`, Abschnitte Ziel/Ist-Zustand/Was zu tun ist/Wer ausführen darf/Leitplanken/Abnahme). Enthält bereits recherchiertes historisches Material pro POI (⚠️-markiert, wo aus Trainingswissen statt Websuche und vor Verwendung zu verifizieren) sowie explizite Leitplanke gegen ungefragtes Einrichten eines Web-Tunnels. `Aufgaben/` ist ein neuer Ordner in `Unterwegs` (Vorbild aus Knowledge Base übernommen, bisher nicht Teil der geplanten Vault-Struktur in `CLAUDE.md`) | User-Auftrag „Leg die Aufgabe unter dem Vault Unterwegs in Aufgaben ab" nach vorheriger Diskussion von Hosting-/TTS-Optionen | 🟡 offen |
| 2026-08-17 | [[../Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]], `Stadtrundgänge/Le Havre/GPX/Le-Havre-Stationen.gpx` (kein `.md`, explizit beauftragt) | Route auf User-Wunsch umgebaut: Station „Quartier Perret / Avenue Foch" ergänzt (fehlte — das ist das eigentliche UNESCO-Ensemble), Parkplatz jetzt Start **und** Ziel, MuMa als Abschluss ans Ende gezogen, Jardins Suspendus komplett aus der Route genommen und nur noch als Auto-Option mit Parkplatzangabe im Text. POI-Übersichtstabelle am Anfang ergänzt. Runde dadurch 9,8 km/89 hm → **7,7 km, flach** (BRouter neu gerechnet), BRouter-URL aktualisiert | Folgeauftrag in derselben Session | 🟡 offen |
| 2026-08-17 | [[../Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]] (neu), [[../Stadtrundgänge/README]], `Stadtrundgänge/Le Havre/GPX/Le-Havre-Stationen.gpx` (kein `.md`, explizit vom User beauftragt) | Neuer Stadtrundgang Le Havre angelegt: 14 Stationen + 3 Parkplätze, Koordinaten per Nominatim/Overpass aus OSM geocodiert (meine ersten Schätzwerte lagen bis zu 870 m daneben, Catène de conteneurs sogar auf der falschen Seite des MuMa → Reihenfolge neu sortiert), Distanzen/Höhenmeter per BRouter berechnet (9,8 km / 89 hm geschlossene Runde), BRouter-Web-URL im Test verifiziert. GPX brauchte zusätzlich einen `<trk>`-Block, weil BRouters Track-Loader reine Wegpunkt-Dateien mit „GeoJSON has no valid layers" ablehnt. Zeile in Stadtrundgänge-README ergänzt | Reiseplanung Normandie vor Ort (Fécamp), User-Auftrag „Mach die .md Datei der Stationen und speichere Sie im Vault" | 🟡 offen |
| 2026-08-12 | [[../CLAUDE.md]], [[../Clippings/Rund um Kornelimünster]], [[../Ressourcen/README]], [[../Wanderungen/Einzeltouren-Übersicht]], [[../Wanderungen/Komoot-Übersicht]], [[../Wanderungen/Touren-Archiv - Gesamtübersicht]], alle 6 Rother-Regionen-Notizen, [[../Wanderungen/Rother-Übersicht]], [[../Wanderungen/Vergessene-Pfade-Übersicht]] | Restliche ~64 Pfadreferenzen auf `Archiv (OneDrive)/` bereinigt (Präfix entfernt bzw. auf `Touren-Archiv - Gesamtübersicht` umgebogen wo sie auf die alte README zeigten); dabei zwei weitere veraltete Touren-Zählungen in `Ressourcen/README.md` gefunden und korrigiert (286→336 Rother-Touren/5→6 Bände, 388→438/391→441 Gesamt-GPX) — beide zeigten noch den Stand vor der Normandie-Ergänzung. Eingefrorene Archiv-Logs (`Änderungshistorie (Archiv Touren)`, `Touren-Journal-Archiv`) bewusst unangetastet | User-Auftrag „ja, mach weiter" (Fortsetzung der OneDrive/Archiv-Eliminierung) | 🟡 offen |
| 2026-08-12 | [[../Wanderungen/README]] | **Fehler-Korrektur:** Beim Flatten von `Archiv (OneDrive)/` wurde `Wanderungen/README.md` versehentlich durch `Archiv (OneDrive)/README.md` überschrieben (Namenskollision beim Batch-Move übersehen). Original per Git-Historie (`Obsidian-Unterwegs`-Repo, Commit von vor 2 Tagen, User hat den Commit selbst rausgesucht) wiederhergestellt; Pfade auf die neue geflachte Struktur angepasst (kein `Archiv (OneDrive)/`-Präfix mehr), fehlende Normandie-Zeile ergänzt (388→438 Touren) | Eigener Fehler, User-Recovery über GitHub-Commit-Historie auf Container 201 | 🟡 offen |
| 2026-08-12 | `Wanderungen/Archiv (OneDrive)/` (Duplikat, kein `.md`), `Rother Wanderführer/` im Vault-Root (kein `.md`) | Nach versehentlicher Sync-Dateiwiederherstellung (User, ~52 Dateien) war `Archiv (OneDrive)/` mit identischen Duplikaten der bereits korrekten Dateien wieder aufgetaucht, plus eine leere `.gpx.md`-Datei fehlplatziert im Vault-Root — beides per md5-Verifikation als reine Duplikate bestätigt und gelöscht | User-Auftrag „räum erst auf" | 🟡 offen |
| 2026-08-12 | [[../Wanderungen/Archiv (OneDrive)/Rother-Bretagne-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-CinqueTerre-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Daenemark-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Neapel-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Mallorca-Übersicht]], [[../Wanderungen/Archiv (OneDrive)/Rother-Normandie-Übersicht]] | Je Region eine `mapview`-Übersichtskarte ergänzt (`path:"<Kürzel>_"`-Query, z. B. `path:"Bret_"` für alle 51 Bretagne-Touren) — zeigt alle Touren der Region auf einer Karte statt 336 Einzel-Embeds; einzelne GPX-Downloadlinks in den Tabellen unverändert gelassen (Referenz-Archiv, kein Einzel-Embed pro Zeile nötig) | User-Auftrag „eine Übersichtskarte pro Region", direkte Fortsetzung der GPX/Map-View-Korrektur bei den Maastricht-Notizen | 🟡 offen |
| 2026-08-12 | [[../Ressourcen/GPX-Setup-Anleitung]], [[../Ressourcen/GPX-Verwaltung]] | Falsche `mapview`-Codeblock-Syntax korrigiert: `{"geoDataUrl": "..."}`/`{"coordinates": [...], "zoom": ...}` existieren im Map-View-Plugin nicht (im Quellcode verifiziert, `src/main.ts`/`src/mapState.ts` — echte Felder sind `query`/`mapZoom`/`mapCenter`/`autoFit`, GPX-Datei über `path:`-Query-Operator ansprechen) | User fragte, warum ein GPX-Wikilink auf Android die Datei statt der Karte öffnet — Recherche ergab: keine Notiz im Vault hatte je einen funktionierenden Embed, weil die dokumentierte Syntax nie existiert hat | 🟡 offen |
| 2026-08-12 | [[../Stadtrundgänge/Maastricht/Maastricht - Kurztour (2-3h) - mit Epochen]], [[../Stadtrundgänge/Maastricht/Maastricht - Langtour (5-6h) - mit Epochen]], [[../Clippings/Rund um Kornelimünster]] | Funktionierenden `mapview`-Codeblock (korrekte Syntax, s.o.) ergänzt — Langtour hatte zuvor gar keinen GPX-Abschnitt im Fließtext, nur Frontmatter | Gleicher Kontext wie oben — Fix auf alle 3 Notizen mit tatsächlich vorhandener GPX-Datei ausgeweitet | 🟡 offen |
| 2026-08-12 | [[../Stadtrundgänge/Maastricht/Maastricht - Highlights (3-4h) - mit Epochen]], [[../Ressourcen/GPX-Verwaltung]] | Toten Verweis auf nicht existierende `Maastricht-Route.gpx` entfernt: `gpx_file`-Frontmatter in der Highlights-Notiz gelöscht, stattdessen Platzhalter-Abschnitt „Route fehlt noch" (inerter Beispiel-Codeblock zum späteren Nachtragen) eingefügt; Tabellenzeile + Ordnerstruktur in `GPX-Verwaltung.md` auf „⏳ Route fehlt noch" korrigiert | User-Bestätigung „Route fehlt noch, Notiz und Tabelle bitte anpassen" | 🟡 offen |
| 2026-08-11 | [[../CLAUDE.md]] | Plugins-Abschnitt aktualisiert: Fehlender Plugin-Code auf X1 gefunden, Root Cause geklärt (`community-plugin`-Kategorie fehlte seit Erstinstallation in `ob sync-config` auf 201/203) und per Live-Fix auf beiden Containern behoben — X1 hat jetzt alle 12 Plugin-Ordner lokal, `Fully synced` verifiziert | Knowledge-Base-Session, User bat um Prüfung + Nachtrag, dann nach Screenshot um Config-Check auf 201/203 „siehe auch alle andere Vaults" → Fix auf alle 7 Vaults ausgeweitet | 🟢 bestätigt |
| 2026-08-11 | [[../.obsidian/community-plugins.json]] (kein `.md`), [[../CLAUDE.md]] | 11 von 12 Plugins auf X1 aktiviert (`community-plugins.json` geschrieben + Obsidian komplett neu gestartet, User bestätigte Neustart); `settings-search` als leerer/unvollständiger Plugin-Ordner auf 203 entdeckt | User-Auftrag „Plugins auf X1 unter Community-Plugins aktivieren" | 🟢 bestätigt |
| 2026-08-11 | [[../CLAUDE.md]] (Status-Zeilen, Task #9 abgeschlossen) | Touren + Urlaub archiviert nach User-Bestätigung „Unterwegs ist verifiziert": Container-201-Kopien read-only + umbenannt, 203 bereinigt, beide GitHub-Repos vom User manuell archiviert (kein `gh`-CLI/Token verfügbar) — Task #9 vollständig abgeschlossen | User-Auftrag „archiviere Touren und Urlaub im Github und nur auf 201 als lokaler Ordner aber ro und mit verändertem Namen", Bestätigung „Erledigt, beide archiviert" | 🟢 bestätigt |
| 2026-08-11 | [[../CLAUDE.md]] (Plugin-Tabelle + Root-Cause-Absatz) | Zusatzbefund per User-Screenshot: `settings-search` v1.3.10 vault-übergreifend inkompatibel mit Obsidian 1.13.6 (Update durch vorherigen Neustart ausgelöst) — betraf `Touren`/`Knowledge Base`, nicht direkt `Unterwegs` (hier nie vollständig installiert). Auf User-Entscheidung „überall deinstallieren" hin in `Touren`/`Knowledge Base` entfernt (nicht in diesem Vault, da hier ohnehin nicht funktionsfähig vorhanden); Tabelle hier bereinigt | User-Auftrag „Plugin überall deinstallieren" | 🟢 bestätigt |

---
