---
tags:
  - claude
  - projekt
created: 2026-08-10
modified: 2026-08-12
---

# CLAUDE.md — Unterwegs-Vault

Projekt-Instruktionen für Claude Code beim Arbeiten im Unterwegs-Vault.

## Was ist dieses Vault?

Neuer Vault als Merge von `Urlaub` + `Touren` (beide LXC-203-Geschwister-Ordner) — Reiseplanung, Wanderungen, Stadtrundgänge, Sehenswürdigkeiten und ein geplantes Urlaubstagebuch, das die anderen Kategorien direkt verlinken kann (Hauptgrund für den Merge: Cross-Vault-Wikilinks funktionieren in Obsidian nicht). Details zur Entscheidungsfindung: `memory/project-unterwegs-vault-struktur.md` und `memory/project-touren-vault-soll-git-bekommen.md` im Cross-Vault-Root (`/home/claude/Obsidian-Vaults`).

**Status (2026-08-11):** Vault-Shell (Task #3), Claude-Vorbereitung + Plugins (Task #6), Content-Migration (Task #4), Link-/Konventions-Fixes (Task #5) und Stilllegung Urlaub/Touren (Task #9) abgeschlossen (User-Bestätigung „Unterwegs ist verifiziert" am 2026-08-11) — Inhalte aus `Urlaub/` und `Touren/` sind als **Kopie** übernommen. Die Quell-Vaults sind jetzt vollständig archiviert: auf Container 201 read-only umbenannt (`<Vault> (Archiv 2026-08-11)`), auf 203 vollständig entfernt, beide GitHub-Repos vom User manuell archiviert („Archive this repository", kein `gh`-CLI/Token in dieser Session verfügbar). X1 + Smartphone schaltet der User selbst ab. Details: [[Knowledge Base/IT@home/Infrastruktur/Proxmox/LXC 201 – Vault-Sync (obsidian-headless + Git-Backup)|LXC 201 – Vault-Sync]] Abschnitt 5. Die vault-präfixierten Excalidraw-/README-Pfade (`Touren/Wanderungen/…`, `Touren/Stadtrundgänge/…`) sind auf die neue Vault-Struktur (`Wanderungen/…`, `Stadtrundgänge/…`) korrigiert. Noch offen: `Regionen/` ist ein neues Organisationskonzept ohne Vorlage in den Quell-Vaults und noch nicht angelegt; uneinheitliches Frontmatter-Schema zwischen `Wanderungen`/`Stadtrundgänge`/`Übernachtungen` (`tags`/`created`/`modified`) und `Einpacklisten` (`title`/`erstellt`/`reise`/`zeitraum`) ist erkannt, aber noch nicht vereinheitlicht; zwei tote Wikilinks in `Stadtrundgänge/README.md` (`Maastricht - Kurztour (2-3h)`, `Maastricht - Altstadt Highlights` ohne „mit Epochen"-Suffix) zeigen auf nicht existierende Dateien — vermutlich bereits vor dem Merge in Touren kaputt, nicht migrationsbedingt.

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
| `tag-wrangler` | Tags umbenennen/mergen/durchsuchen |

Bewusst **nicht** übernommen: `obsidian-git` (projektweit seit 2026-08-04 deaktiviert, Backup läuft über `git-backup-unterwegs.timer` auf Container 201), `drawio`/`drawio-obsidian` (redundant zu `drawio-editor`), `obsidian-local-rest-api` (unvollständig installiert in Touren, keine `manifest.json`), `obsidian42-brat` (User-Entscheidung 2026-08-10), `settings-search` (seit Obsidian 1.13.6 vault-übergreifend inkompatibel, überall deinstalliert — User-Entscheidung 2026-08-11, siehe unten).

**Behoben (2026-08-11):** Auf ThinkPad X1 fehlte `.obsidian/plugins/` für `Unterwegs` zunächst komplett (kein Ordner, keine `community-plugins.json`) — betraf u. a. aktiv genutzte `obsidian-map-view`-Einbettungen in `Ressourcen/GPX-Setup-Anleitung.md`, `Ressourcen/GPX-Verwaltung.md`, `Stadtrundgänge/README.md`, `Stadtrundgänge/Template - Stadtrundgang.md`, `Wanderungen/Template - Wanderung.md`. Root Cause: `ob sync-status` zeigte auf **beiden** Headless-Clients (201, 203) `Configs: …, community-plugin-data` — **`community-plugin` (Plugin-Code, `.js`/`.css`/`manifest.json`) fehlte**, seit der allerersten Vault-Einrichtung auf 201/203 (2026-08-03) fälschlich weggelassen (Zuordnungsfehler, Details `[E3]`/`[S14]` in [[Knowledge Base/Obsidian/Obsidian Sync – Headless Client (obsidian-headless)|Obsidian Sync – Headless Client]] bzw. [[Knowledge Base/IT@home/Infrastruktur/Proxmox/LXC 201 – Vault-Sync (obsidian-headless + Git-Backup)|LXC 201 – Vault-Sync]]). Container 203 hatte die 12 Plugin-Ordner lokal (aus `Urlaub`/`Touren` kopiert), pushte sie aber nie zur Sync-Cloud. **Fix:** `community-plugin` per `ob sync-config` bei allen 7 Vaults auf 201 **und** 203 ergänzt (nicht nur `Unterwegs` — schließt die Lücke grundsätzlich für künftige Vault-Neuinstallationen), Sync-Service für `Unterwegs` auf 203 neu gestartet, Upload verifiziert (`Fully synced`), 201 hat die Ordner sofort gezogen, X1 hat alle 12 Plugin-Ordner jetzt lokal (`ob sync-status` bestätigt end-to-end). Aktivierung der Plugins unter Einstellungen → Community-Plugins bleibt weiterhin ein manueller Schritt pro Gerät (bewusst nicht gesynct). **Auf X1 erledigt (2026-08-11):** 11 der 12 Plugins über `.obsidian/community-plugins.json` aktiviert + Obsidian komplett neu gestartet (Pflicht, da Plugin-Status nur beim App-Start neu eingelesen wird), Aktivierung per `data.json`-Erzeugung mehrerer Plugins verifiziert. **`settings-search` überall deinstalliert statt nachkopiert (2026-08-11):** Der leere Ordner auf Container 203 (unvollständige Migrationskopie aus `Touren`) wäre ohnehin kein funktionsfähiges Plugin gewesen — Zusatzbefund per User-Screenshot: `settings-search` v1.3.10 lädt seit einem nebenbei ausgelösten Obsidian-Update (1.13.4 → 1.13.6) auf **keinem** Vault des Geräts mehr, auch nicht dort, wo es vollständig installiert war (`Touren`, `Knowledge Base`) — „nicht kompatibel"-Fehler trotz erfüllter `minAppVersion: 0.12.17`, vermutlich weil das seit 3 Jahren unveränderte Plugin (Autor `javalent`) sich nicht mehr mit aktuellen internen Obsidian-APIs verträgt. User-Entscheidung: überall deinstallieren statt auf ein Update zu warten — betrifft `Unterwegs` gar nicht direkt (Plugin war hier nie vollständig installiert), wohl aber `Touren`/`Knowledge Base` (dort Ordner + `community-plugins.json`-Eintrag entfernt, lokal auf X1 sowie direkt auf 201/203). Details: [[Knowledge Base/Obsidian/Vault-Plugins – Übersicht & Gerätekonfiguration|Vault-Plugins – Übersicht]] Auffälligkeit 6.

**Plugins auf Smartphone (Android) aktivieren — Anleitung:** Plugin-**Code** synct seit dem obigen Fix automatisch mit, die **Aktivierung** bleibt aber pro Gerät manuell (analog X1, s.o.):

1. Vault „Unterwegs" öffnen bzw. erstmalig über Sync verbinden (Einstellungen → Sync → Remote-Vault auswählen), vollständig durchsynchronisieren lassen.
2. **Wichtig, sonst kommt der Plugin-Code nicht an:** In den Sync-Einstellungen (Zahnrad-Icon im Sync-Tab) prüfen, dass **„Installed community plugins"** aktiviert ist.
3. Warten bis „Fully synced".
4. Einstellungen → Community-Plugins → Hauptschalter einschalten (Sicherheitswarnung bestätigen), falls noch aus.
5. Alle 11 Plugins aus der Tabelle oben sollten jetzt unter „Installierte Plugins" auftauchen — jedes einzeln aktivieren.
6. App danach **komplett neu starten** (voll beenden, nicht nur Hintergrund) — Plugin-Status wird nur beim App-Start neu eingelesen.
7. Fehlt eines: über Community-Plugins → Durchsuchen manuell nachinstallieren.

Heads-up: `drawio-editor` bietet auf Mobile nur Vorschau, kein Editieren (siehe [[Knowledge Base/Obsidian/Draw.io Plugins für Obsidian – Vergleich|Draw.io Plugins – Vergleich]]).

**Behoben (2026-08-12) — GPX-Wikilinks öffneten auf Android die Datei statt der Karte:** Root Cause war kein Android-spezifisches Verhalten, sondern eine falsche `mapview`-Codeblock-Syntax in `Ressourcen/GPX-Setup-Anleitung.md`/`GPX-Verwaltung.md` (`{"geoDataUrl": "..."}`, `{"coordinates": [...]}`) — diese Felder existieren im Map-View-Plugin gar nicht (im Quellcode verifiziert: `src/main.ts`/`src/mapState.ts` kennen nur `query`/`mapZoom`/`mapCenter`/`autoFit`). Dadurch hatte **keine** Tour-Notiz im Vault je einen funktionierenden Embed — nur einen reinen Datei-Wikilink, den Obsidian mangels eigenem GPX-Viewer auf Android an die OS-„Öffnen mit"-Auswahl weiterreicht. Korrekte Syntax (GPX-Datei über den `path:`-Query-Operator, Teilstring genügt): `​```mapview\n{"query": "path:\"Dateiname.gpx\"", "autoFit": true}\n​```` — jetzt in beiden Ressourcen-Notizen sowie in den 3 Tour-Notizen mit tatsächlich vorhandener GPX-Datei (Kurztour, Langtour, `Clippings/Rund um Kornelimünster`) eingebaut. **Ergänzung (2026-08-12):** `Maastricht - Highlights (3-4h) - mit Epochen.md` referenzierte `GPX/Maastricht-Route.gpx` — diese Datei existiert im `GPX/`-Ordner nicht (nur `Maastricht-Kurztour.gpx` + `Maastricht-Langtour.gpx` sind vorhanden). Auf User-Bestätigung („Route fehlt noch, Notiz und Tabelle bitte anpassen") hin bereinigt: `gpx_file`-Frontmatter aus der Highlights-Notiz entfernt, dort stattdessen ein „⏳ Route fehlt noch"-Platzhalterabschnitt mit inertem Beispiel-Codeblock zum späteren Nachtragen; Tabellenzeile + Ordnerstruktur-Diagramm in `GPX-Verwaltung.md` ebenfalls auf „Route fehlt noch" korrigiert (vorher fälschlich „✅ Aktiv"). Damit haben jetzt alle drei Maastricht-Stadtrundgänge-Notizen einen konsistenten „Route & GPX-Daten"-Abschnitt — zwei mit funktionierendem Embed, einer als dokumentierte Lücke.

## Frontmatter-Schema (bewusst uneinheitlich)

Es gibt mehrere Frontmatter-Schemata nebeneinander — **keine Vereinheitlichung geplant**, jede Kategorie behält ihr eigenes Schema. Grund: Die Kategorien haben unterschiedliche Nutzungszwecke (Kern-Notiz vs. Index vs. Packliste vs. Tour-Detail mit Kartendaten); ein gemeinsames Schema würde entweder Felder erzwingen, die die meisten Kategorien nicht brauchen, oder auf kategoriespezifische Zusatzfelder verzichten.

| Schema | Felder | Dateien |
|--------|--------|---------|
| Kern-Content | `tags`, `created`, `modified` (+ optional `location`) | `Übernachtungen/*`, `_Wohnwagen-Technik/*.md` + `Sackmarkise/Analyse – Sackmarkisen für Wohnwagen.md` |
| Index (Archiv-Übersichten) | `title`, `tags`, `created`, `modified`, `type`, `sort_index` (+ optional `region`) | `Wanderungen/Archiv (OneDrive)/README.md`, `Rother-Übersicht.md`, `Komoot-Übersicht.md` |
| Ressourcen/Anleitungen | `title`, `tags`, `created`, `modified`, `type` | `Ressourcen/GPX-Setup-Anleitung.md`, `Ressourcen/Tour-Template.md` |
| Einpacklisten | `title`, `type`, `tags`, `reise`, `zeitraum`, `status`, `erstellt` (kein `created`/`modified`, sondern `erstellt`) | `Einpacklisten/*.md` |
| Tour-Detail „mit Epochen" (reichhaltigstes Schema) | `title`, `tags`, `created`, `modified`, `difficulty`, `duration`, `distance`, `stations`, `epochen_focus`, `type`, `region`, `status`, `gpx_file`, `coordinates` | `Stadtrundgänge/Maastricht/Maastricht - Kurztour/Langtour/Highlights (…) - mit Epochen.md` |
| Vergleichs-Übersicht | wie Tour-Detail, aber ohne `distance`/`stations`/`gpx_file`/`coordinates`, dafür `source` | `Stadtrundgänge/Maastricht/Maastricht - Touren Vergleich MIT EPOCHEN.md` |
| Clippings (Web-Clipper-Standard, automatisch generiert) | `title`, `source`, `author`, `published`, `created`, `description`, `tags: [clippings]` | `Clippings/*.md`, `Stadtrundgänge/Maastricht/Gefundene Touren/*.md` |

**Empfehlung — welches Schema für neue Notizen (Stand 2026-08-10, nach Abgleich mit Knowledge Base):**

| Notiz-Typ | Zu verwendendes Schema |
|-----------|------------------------|
| Einfache Content-Notiz (Wanderung, Übernachtung, Wohnwagen-Technik) | Kern-Content: `tags`/`created`/`modified` (+ `location` falls Ort relevant) |
| Index-/Sammelseite | Index-Schema: zusätzlich `sort_index` (+ optional `type: Index`) |
| Domänenspezifische Detail-Notiz mit Fachfeldern (z. B. weitere Stadtrundgänge mit GPS/Distanz/Schwierigkeit) | eigenes erweitertes Schema analog „Tour-Detail mit Epochen" — bewusst nicht auf Kern-Content-Schema reduzieren |
| Packliste/Notiz mit Lebenszyklus-Status | eigenes Schema mit `status`-Feld analog Einpacklisten |
| Web-Clipping | automatisch generierter Web-Clipper-Standard — nie manuell anpassen |

**Konsolidierte Referenznotiz (vaultübergreifend, nicht per Wikilink erreichbar):** `Knowledge Base/Obsidian/Frontmatter-Schema – Konventionen über alle Vaults.md` — enthält dieselbe Analyse plus die verifizierte Kernregel, wann Obsidian YAML-Frontmatter überhaupt parst (Quellenbeleg Obsidian-Forum/Help-Doku), inkl. einer Korrektur eines gegenteiligen Irrtums in Knowledge Base's eigener `CLAUDE.md`.

**Abgleich mit Knowledge Base (513 Notizen ausgewertet, 2026-08-10):** Dort existieren mindestens 9 verschiedene Schemata (u. a. Kern-Content `tags/created/modified` [52×, identisch zu Unterwegs], Index mit `sort_index` [9×, identisch], Web-Clipper-Standard [~73×, identisch], domänenspezifische Geräte-/Infrastruktur-Schemata mit Fachfeldern [analog zu „Tour-Detail mit Epochen"], sowie `name/description/metadata` für die Auto-Memory-Dateien selbst). Bestätigt: kategorie-eigenes Schema statt Vereinheitlichung ist ein vaultübergreifend etabliertes, bewusstes Muster — kein Unterwegs-spezifischer Sonderfall.

**Vorsicht bei künftiger `OneNote-Archiv/`-Migration:** In Knowledge Base dominiert zahlenmäßig (139×) das Schema `title`/`updated`/`created` — das ist aber praktisch komplett auf `IT@home/Archiv/…OneNote…/` konzentriert, also ein reines Migrations-Artefakt (nutzt `updated` statt `modified`), kein bewusster Standard. Wenn der noch offene `OneNote-Archiv/`-Zielordner (1:1-Übernahme aus `Urlaub/` geplant) gefüllt wird, ist zu erwarten, dass genau dieses Schema mitkommt — das ist dann ebenfalls erwartetes Import-Artefakt, keine neue Inkonsistenz und kein Anlass, es nachträglich anzugleichen.

**Behobener Sonderfall (kein Schema-Problem, sondern ein Strukturfehler):** In `Wanderungen/README.md`, `Wanderungen/Template - Wanderung.md`, `Stadtrundgänge/README.md`, `Stadtrundgänge/Template - Stadtrundgang.md`, `Stadtrundgänge/Maastricht/GPX/README - GPX & Stadtplan Anleitung.md` stand vor dem `---`-Frontmatter-Block eine H1-Überschrift. Da YAML-Frontmatter in Obsidian nur erkannt wird, wenn `---` die allererste Zeile der Datei ist, wurde `tags`/`created`/`modified` in diesen fünf Dateien **nicht** als echtes Frontmatter geparst (kein Properties-Panel, nicht filterbar/suchbar über Obsidian-Properties) — reiner Fließtext, der wie Frontmatter aussah. Am 2026-08-10 gefixt: Frontmatter-Block an den Dateianfang verschoben, H1-Überschrift folgt jetzt danach; `modified` entsprechend aktualisiert. Herkunft geklärt: Der Bug stammt aus dem ursprünglichen Touren-Vault-Template (dort in 6 Dateien identisch vorhanden, inkl. `Touren/README.md`) und wurde beim Content-Merge 1:1 mitkopiert — kein Migrations-Artefakt.

`_template/Seite.md` weicht zusätzlich in der Feldbenennung ab (`Reference link`, `Topics` groß/mit Leerzeichen statt kleingeschriebener snake_case-Felder wie überall sonst) — ebenfalls unangetastet gelassen.

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
**Status:** Tasks #3, #4, #5, #6, #8, #9 abgeschlossen; Frontmatter-Schema dokumentiert (bewusst uneinheitlich, kein Vereinheitlichungsbedarf), drei tote/fehlerhafte Links in `Stadtrundgänge/README.md` auf die „mit Epochen"-Dateien umgebogen + leere Stub-Datei gelöscht, Frontmatter-Strukturfehler (H1 vor `---`) in 5 README/Template-Dateien gefixt (Vault-weit gegen Knowledge Base/PKM-Dirigent geprüft, dort keine echten Treffer); Urlaub/Touren vollständig archiviert (Container-seitig + beide GitHub-Repos, siehe Status-Zeile oben); offen: `Regionen/`-Konzept, Mehrgeräte-Rollout (Task #7)
