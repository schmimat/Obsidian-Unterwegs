---
tags:
  - claude
  - projekt
created: 2026-08-10
modified: 2026-11-02
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

- **Leitprinzip:** Wanderungen/Stadtrundgänge/Sehenswürdigkeiten bleiben eigenständiges, wiederverwendbares Wissen und ziehen nicht in Reise-Ordner um. Der Tagebuch-Eintrag verlinkt sie.
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

Drei Reisen: **Sommerurlaub 2026 – Bretagne & Normandie**, **Rügen & Dänemark 2025** (beide aus Fotos rekonstruiert), **Prag 2026** (30.10.–03.11.2026, aus einem Claude-Chatverlauf, seit 2026-11-02). Hauptnotiz mit Tabelle „Reiseverlauf“ (`[[Tagebuch/YYYY-MM-DD\|TT.MM.]]`), danach die Tagesdateien.

**Quelle Fotos:** (1) `Knowledge Base/Fotoverwaltung/Fotoregister_<person>.csv` auf den Zeitraum filtern, liefert Tag → Ort ohne Bildzugriff; Matthias' Register hat von Mai 2024 bis April 2026 kein GPS, dann Claudias nehmen. (2) digiKam-Urlaubsordner `\\10.12.40.242\storage\Bilder\digiKam\Jahre\<Jahr>\<MM.TT-MM.TT>_<Name>` mit Tagesordnern `MM.TT_Ort`. (3) Pro Tag 2–3 Fotos wirklich ansehen. Personenbezogene Details (Adresse, Nachname) nicht übernehmen.

**Quelle Claude-Chatverlauf** (Prag 2026): 1:1-Export als `.md` im Reiseordner, Bilder nur als Dateiname (liegen in der Nextcloud). Tagesgerüst aus den `## <Tag>`-Überschriften; der Inhalt steckt vor allem in Claudes Antworten, weil die User-Nachrichten meist nur Fotos sind. Erklärungen aus dem Chat in der Notiz als ungeprüft kennzeichnen, Tage ohne Chat als Platzhalter anlegen. Quelldatei per Dateiname verlinken (`[[Prag-Reise-2026-Chatverlauf|…]]`), so übersteht der Link ein Verschieben.

**Weitere Erkenntnisse:** Word-Reiseverlauf liegt im digiKam-Urlaubsordner, nicht im Vault (Tabellenzeilen mit Wikilinks nicht am ersten `|` splitten). Windows-Python + UNC: Forward-Slash-Pfade, `sys.stdout.reconfigure(encoding="utf-8")`. Handy-Fotos ins Foto-Archiv nur kopieren, mit Vorher/Nachher-Inventar per MD5 und `…_Dokumentation.md` im Urlaubsordner.

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

1. **Prag 2026 vervollständigen:** 30.10. (Anreise), Nachmittag 02.11. (Kafka-Museum, Konzert in der Spanischen Synagoge) und 03.11. (Rückfahrt) nachtragen; optional mit Fotos aus der Nextcloud anreichern.
2. **Wohnwagen:** Toiletten-Leuchte Bürstner 4313 — Spannung unter Last messen, Fassung öffnen (Starter oder Platine), dann Ersatzröhre oder LED. Stand in [[_Wohnwagen-Technik/Wohnwagen-Bürstner-4313]].
3. **`Regionen/`-Konzept** entscheiden, jetzt mit drei Reisen als Anwendungsfall.
4. Rügen 2025 hat noch keinen `Auswahl/`-Ordner mit kuratierten Tagesbestenlisten (Bretagne hat einen).

Zuletzt aktualisiert: 2026-11-02 (/preserve: Prag 2026 angelegt, Datei von 41,9 KB verschlankt, alte Fassung in `CLAUDE-Archive.md`).
