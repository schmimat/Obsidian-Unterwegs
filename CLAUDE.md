---
tags:
  - claude
  - projekt
created: 2026-08-10
modified: 2026-11-07
---

# CLAUDE.md — Unterwegs-Vault

Reiseplanung, Reise-Tagebücher, Wanderungen, Stadtrundgänge, Sehenswürdigkeiten und Wohnwagen-Technik. Entstanden 2026-08-10/11 als Merge der inzwischen archivierten Vaults `Urlaub` + `Touren` (Hauptgrund: Cross-Vault-Wikilinks funktionieren in Obsidian nicht). Merge-Verlauf, Plugin-Bugfix-Geschichte und alle früheren Details: `CLAUDE-Archive.md` (Fassung bis 2026-11-02, wörtlich).

## Struktur

```
Unterwegs/
├── Reisen/<Reisename>/{<Reisename>.md, Tagebuch/YYYY-MM-DD.md}
├── Wanderungen/ · Stadtrundgänge/ · Sehenswürdigkeiten/ · Übernachtungen/ · Einpacklisten/
├── Ressourcen/ · Clippings/ · Doku/ · Aufgaben/
├── _template/ · Templates/        (Templates = Fach aus dem PKM-Dirigent-Schrank, nur Recherche-Vorlage.md)
├── _Wohnwagen-Technik/            (Sackmarkise/, Wohnwagen-*.md)
└── OneNote-Archiv/
```

- **Leitprinzip:** Wanderungen/Stadtrundgänge/Sehenswürdigkeiten/Übernachtungen bleiben eigenständiges, wiederverwendbares Wissen und ziehen nicht in Reise-Ordner um. Der Tagebuch-Eintrag verlinkt sie bei der ersten Nennung. Vorbild: `Sehenswürdigkeiten/Prag/` + `Pilsen/` (je Notiz: Gesehen mit Datum-Link, Praktisch/Tipps, Quellenliste, `location` aus Foto-GPS) und `Übernachtungen/Hotel Atlantic (Prag)`.
- **`Regionen/`** (Bindeglied Reise ↔ Wanderung/Stadtrundgang) ist geplant, aber noch nicht angelegt. Entwurf: `memory/project-unterwegs-vault-struktur.md` im Cross-Vault-Root.

## Autonomes Editieren: Änderungshistorie statt Rückfrage

Für **inhaltliche Änderungen an `.md`-Notizen** (Text, Frontmatter-Updates, neue Notizen inkl. Index-Verlinkung, Umbenennen/Verschieben inkl. Link-Fix) fragst du **nicht** einzeln nach. Stattdessen trägst du jede Änderung in [[Doku/Claude – Änderungshistorie]] ein; der User bestätigt/verwirft wöchentlich gesammelt.

**Ausnahmen (weiterhin Rückfrage nötig):** Löschen von Dateien, strukturelle Auffälligkeiten, alles außerhalb von `.md`, der Verschiebe-Befehl selbst (`mv`).

## Sprache & Stil

- **Deutsch** für alle Inhalte (englische Fachbegriffe wie Plugin/Sync bleiben)
- Wikilinks `[[Notiz-Name]]` ohne `.md`-Endung; Embeds (Bild, Audio) immer als reiner Dateiname `![[Name.jpg]]`, nie mit Ordnerpfad
- Frontmatter mit `tags`, `created`, `modified` (bei Bearbeitung `modified` auf heute bumpen); Touren-Vokabular (`region`, `difficulty`, `duration`) für Wanderungen/Stadtrundgänge

## Sync & Backup

Container-201/203-Muster: `obsidian-sync-unterwegs.service` auf 201+203, `git-backup-unterwegs.timer` auf 201 → Repo `Obsidian-Unterwegs`. Kein `obsidian-git`-Plugin (projektweit seit 2026-08-04 aus). Container 203 hat kein `git` und keine Repo-Credentials; Wiederherstellung alter Fassungen über die Commit-Historie auf GitHub.

## Plugins

`calendar`, `colored-tags`, `drawio-editor`, `featured-image`, `notebook-navigator`, `obsidian-excalidraw-plugin`, `obsidian-map-view`, `obsidian-outliner`, `obsidian-style-settings`, `pixel-perfect-image`, `tag-wrangler`. Bewusst nicht: `obsidian-git`, `drawio`/`drawio-obsidian`, `obsidian-local-rest-api`, `obsidian42-brat`, `settings-search` (seit Obsidian 1.13.6 inkompatibel, überall deinstalliert).

- **Plugin-Code synct** (`community-plugin` in `ob sync-config` auf 201+203, seit 2026-08-11). **Aktivierung bleibt je Gerät manuell**, danach Obsidian komplett neu starten. Android: in den Sync-Einstellungen „Installed community plugins“ einschalten. Schritt-für-Schritt-Anleitung im Archiv.
- `drawio-editor` kann auf Mobile nur anzeigen, nicht bearbeiten.

## GPX / Map View

- Der `mapview`-Codeblock kennt nur `query`/`mapZoom`/`mapCenter`/`autoFit` (im Plugin-Quellcode verifiziert). GPX einbinden: `{"query": "path:\"Dateiname.gpx\"", "autoFit": true}` (Teilstring genügt). Eingebaut in den 3 Maastricht-Touren (Highlights ohne eigene GPX, dokumentierte Lücke) und als eine Übersichtskarte je Rother-Region (z. B. `path:"Bret_"`).
- „Focus in Map View“ geht auf Android nur über den Datei-Explorer bzw. die geöffnete Datei, nicht per Long-Press auf einen Wikilink.
- Map-View-Karten leer, obwohl Dateien und Syntax stimmen: veralteter Plugin-Index, Obsidian komplett neu starten.

## Frontmatter-Schema (bewusst uneinheitlich)

Jede Kategorie behält ihr eigenes Schema, keine Vereinheitlichung geplant. Vaultübergreifende Analyse: `Knowledge Base/Obsidian/Frontmatter-Schema – Konventionen über alle Vaults.md`.

| Schema | Felder | Dateien |
|--------|--------|---------|
| Kern-Content | `tags`, `created`, `modified` (+ optional `location`) | `Übernachtungen/*`, `_Wohnwagen-Technik/*.md` |
| Index | zusätzlich `title`, `type`, `sort_index` (+ optional `region`) | Archiv-Übersichten unter `Wanderungen/` |
| Ressourcen/Anleitungen | `title`, `tags`, `created`, `modified`, `type` | `Ressourcen/*` |
| Einpacklisten | `title`, `type`, `tags`, `reise`, `zeitraum`, `status`, `erstellt` | `Einpacklisten/*.md` |
| Reise / Tagebuch | Reise: `title`, `type: reise`, `tags`, `reise`, `zeitraum`, `region`, `created`, `modified` · Tagebuch: `tags: [reisetagebuch]`, `datum`, `reise`, `orte` (+ optional `wanderung`) | `Reisen/**` |
| Tour-Detail „mit Epochen“ | u. a. `difficulty`, `duration`, `distance`, `stations`, `epochen_focus`, `region`, `status`, `gpx_file`, `coordinates` | `Stadtrundgänge/Maastricht/*` |
| Clippings | Web-Clipper-Standard, nie manuell anpassen | `Clippings/*.md` |

- Frontmatter wird nur erkannt, wenn `---` die allererste Zeile ist (keine H1 davor).
- `_template/Seite.md` weicht in der Feldbenennung ab (`Reference link`, `Topics`), bewusst unangetastet.

## Muster

- **Batch-Moves in einen gemeinsamen Zielordner:** Kollisionsprüfung im Loop je Datei, nicht nur vorab (2026-08-12 wurde `Wanderungen/README.md` überschrieben).
- **Defekte am Wohnwagen** (Bürstner 4313) als eigener Abschnitt in der Fachnotiz des Objekts, nicht in `Aufgaben/`: Symptom → schon Geprüftes → Verdacht → Bezugsquellen → nächster Test. 12-V-Fehler: erst Verbraucher, dann Kontakte, dann Spannung unter Last messen.

## `Reisen/` — Reise-Tagebücher

Drei Reisen: **Sommerurlaub 2026 – Bretagne & Normandie**, **Rügen & Dänemark 2025** (beide aus Fotos rekonstruiert), **Prag 2026** (30.10.–03.11.2026 mit Pilsen auf der Heimfahrt; Chatverlauf + alle Fotos, vollständig seit 2026-11-06, Word `Prag 2026 - Reiseverlauf.docx` im digiKam-Ordner). **Bretagne bleibt wie sie ist** (knapp, ohne Reisestil-Abschnitt) — User-Entscheidung 2026-11-06. Hauptnotiz mit Tabelle „Reiseverlauf“ (`[[Tagebuch/YYYY-MM-DD\|TT.MM.]]`), danach die Tagesdateien.

**Quelle Fotos:** (1) `Knowledge Base/Fotoverwaltung/Fotoregister_<person>.csv` auf den Zeitraum filtern, liefert Tag → Ort ohne Bildzugriff; Matthias' Register hat von Mai 2024 bis April 2026 kein GPS, dann Claudias nehmen. (2) digiKam-Urlaubsordner `\\10.12.40.242\storage\Bilder\digiKam\Jahre\<Jahr>\<MM.TT-MM.TT>_<Name>` mit Tagesordnern `MM.TT_Ort`. (3) Pro Tag 2–3 Fotos wirklich ansehen. Personenbezogene Details (Adresse, Nachname) nicht übernehmen. (4) Fotos von Tickets, Schildern und Infotafeln liefern Titel und Namen.

**Kamera-Uhr prüfen:** Die Lumix DC-TZ202 (`P103…`, kein GPS) stellt nicht auf Winterzeit um. Abgleich per Foto der Handy-Uhr; Korrektur nur der drei EXIF-Datumsfelder byte-genau im APP1-Segment (Bilddaten per MD5 unverändert), mtime mitziehen (Prag 2026: +1:00:32, 205 JPGs korrigiert). Handy `PXL_…`: Dateiname UTC, EXIF Ortszeit. Im Explorer nach Spalte **„Aufnahmedatum“** sortieren, „Erstelldatum“ ist der Kopierzeitpunkt aufs NAS.

**Bilderkennung durch Claude/Subagent ist mittelmäßig** (Prag: Stiertreppe, Klausen-Synagoge, Kostüm-„Polizei“ vom User korrigiert): vor dem Eintragen Nachbarfotos + GPS ansehen, unsichere Orte als „vermutlich“ und als Frage an den User. Fakten aus dem Chat vor dem Wiederverwenden mit `fakten-pruefer` prüfen (Prag: 38 Aussagen, 0 falsch, 9 ungenau).

**Quelle Claude-Chatverlauf** (Prag 2026): 1:1-Export als `.md` im Reiseordner, Bilder nur als Dateiname (liegen in der Nextcloud). Tagesgerüst aus den `## <Tag>`-Überschriften; der Inhalt steckt vor allem in Claudes Antworten, weil die User-Nachrichten meist nur Fotos sind. Erklärungen aus dem Chat in der Notiz als ungeprüft kennzeichnen, Tage ohne Chat als Platzhalter anlegen. Quelldatei per Dateiname verlinken (`[[Prag-Reise-2026-Chatverlauf|…]]`), so übersteht der Link ein Verschieben.

**Weitere Erkenntnisse:** Unterwegs möglichst wenig tippen lassen (User 2026-11-06: Chat lenkt vom Erleben ab) — Fotos machen, Tagebuch danach aus Fotos + Rückfragen. Word-Reiseverlauf liegt im digiKam-Urlaubsordner, nicht im Vault (Tabellenzeilen mit Wikilinks nicht am ersten `|` splitten). Windows-Python + UNC: Forward-Slash-Pfade, `sys.stdout.reconfigure(encoding="utf-8")`. Handy-Fotos ins Foto-Archiv nur kopieren, mit Vorher/Nachher-Inventar per MD5 und `…_Dokumentation.md` im Urlaubsordner.

## Reise-Guides-Vault (Audioguides)

- Eigenes Vault `Reise-Guides`, veröffentlicht über Obsidian Publish (passwortgeschützt): https://publish.obsidian.md/reise-guides. Sync auf 201+203 seit 2026-09-29, nicht auf X1. Getrennt von Unterwegs, weil Publish praktisch das ganze Vault veröffentlicht.
- Anleitung mit Kernentscheidungen und Fallstricken: [[Ressourcen/Anleitung - Stadtrundgang mit Audioguide aufbauen & publizieren]], Referenz-Rundgang [[Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]]. Neuer Rundgang: Unterordner `Reise-Guides/Stadtrundgänge/<Ort>/`.
- uMap ist kein Ersatz für bikerouter.de (keine Routenberechnung entlang echter Wege, Datalayer-Format nicht automatisierbar).
- Offen: Live-Test durch die Ehefrau (Login, mp3s offline).

## Wichtige Dateien & Ordner

| Pfad | Inhalt |
|------|--------|
| `CLAUDE-Archive.md` | Frühere Fassungen dieser Datei, wörtlich (nicht automatisch geladen, per Grep durchsuchen) |
| `Doku/Claude – Änderungshistorie.md` | Protokoll autonomer `.md`-Änderungen (wöchentliche Sammelbestätigung) |
| `Doku/Claude – Änderungshistorie (Archiv Touren/Urlaub).md` | Historien der Quell-Vaults bis zum Merge |
| `Aufgaben/` | Arbeitsaufträge für den Claude Code Worker (LXC 203), Format wie `Knowledge Base/IT@home/Aufgaben/` |
| `CC-Session-Logs/` | Session-Logs (`/compress`) |
| `_claude/` + `.claude` (Symlink) | Skills `/compress`, `/preserve`, `/resume` (Master in `PKM-Dirigent/_claude/commands/`) |

Vault-Wartung: `PKM-Dirigent/05 - Vault-Wartung.md` und Fundtabelle `05a - Wartungsfunde.md` (anderer Vault). Modellwahl und feste Agenten: global in `PKM-Dirigent/Cross-Vault/CLAUDE-Global.md`.

## Nächste Schritte

1. **Wohnwagen:** Toiletten-Leuchte Bürstner 4313 — Spannung unter Last messen, Fassung öffnen (Starter oder Platine), dann Ersatzröhre oder LED. Stand in [[_Wohnwagen-Technik/Wohnwagen-Bürstner-4313]].
2. **`Regionen/`-Konzept** entscheiden; konkreter Fall: Prag/Pilsen mit Reise, Sehenswürdigkeiten und Hotel.
3. Rügen 2025 und Prag 2026 haben noch keinen `Auswahl/`-Ordner mit kuratierten Tagesbestenlisten (Bretagne hat einen).
4. **Prag-Reste:** 3 Kamera-Videos (`P1034031/032/142.MP4`) haben noch die Zeit +1 h; Uhrenfoto `P1034162.JPG` löscht der User, dann die Zeile in `Fotoverschiebung-Tagesordner_Dokumentation.md` anpassen; Hotel-Eckdaten (Hausnummer, Preis, Parken) offen.

Zuletzt aktualisiert: 2026-11-07 (/preserve: Prag 2026 vollständig aus Fotos, Sehenswürdigkeiten + Hotel extrahiert, Faktenprüfung, Kamera-Zeitabgleich).
