---
title: "Anleitung – Stadtrundgang mit Audioguide aufbauen & publizieren"
tags: [stadtrundgang, audioguide, anleitung, publish]
created: 2026-08-17
modified: 2026-08-17
type: Anleitung
---

# Anleitung – Stadtrundgang mit Audioguide aufbauen & publizieren

> Allgemeine Referenz für **jeden** Stadtrundgang in `Unterwegs`, der zusätzlich einen gesprochenen Audioguide bekommen soll (nicht nur Le Havre). Beschreibt Architektur, Namenskonvention, Anpassungs-Checkliste und bekannte Fallstricke. Konkretes Referenzbeispiel: [[../Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus|Le Havre]] (erster nach diesem Muster gebauter Rundgang, 2026-08-17).

## 1. Zwei-Vault-Architektur — warum getrennt?

| | `Unterwegs` (dieser Vault) | `Reise-Guides` (eigenständiges Vault daneben) |
|---|---|---|
| **Zweck** | Praktische Routenplanung: Öffnungszeiten, Parken, GPX-Navigation | Audioguide zum Anhören unterwegs (gesprochene Texte + mp3) |
| **Zielgruppe** | Du selbst, über Obsidian Sync | Du + Familie/Mitreisende, über eine **öffentliche, passwortgeschützte** Website |
| **Bereitstellung** | Obsidian Sync (`obsidian-sync-unterwegs.service` auf 201+203) | Obsidian Publish (`ob publish-*`), Site: **https://publish.obsidian.md/reise-guides** |
| **Pfad je Rundgang** | `Stadtrundgänge/<Ort>/` | `Stadtrundgänge/<Ort>/Audioguide/` (im `Reise-Guides`-Vault) |

**Warum getrennt statt einem Vault:** `Reise-Guides` wird komplett veröffentlicht (Publish kennt keine granulare Zugriffssteuerung pro Datei) — alles, was dort liegt, ist potenziell für jeden mit dem Passwort sichtbar. `Unterwegs` bleibt privat. Deshalb leben praktische Infos (Preise, Telefonnummern, Parkplatz-Tipps) **nur** in `Unterwegs`, niemals in `Reise-Guides`.

**`Reise-Guides` ist bewusst generisch** (nicht „Le-Havre-Audioguide" o. Ä. benannt) — jeder neue Rundgang bekommt darin einen eigenen Unterordner `Stadtrundgänge/<Ort>/`, statt für jede Reise ein neues Vault + eine neue Publish-Site aufzusetzen.

**Wichtige Konsequenz:** Es gibt pro Rundgang an **zwei Stellen** eine BRouter-Web-Karten-URL — einmal in der `Unterwegs`-Notiz, einmal in der `Reise-Guides`-Übersicht. Beide enthalten dieselbe Wegpunkt-Liste, müssen aber **einzeln** gepflegt werden (kein automatischer Abgleich). Genau das wurde bei Le Havre einmal vergessen (ein neuer Wegpunkt fehlte in der Reise-Guides-Kopie) — siehe [[../Doku/Claude – Änderungshistorie]].

## 2. Nummerierungsschema

- `00` = Parkplatz/Start (Start **und** Ziel, kein Audioguide-Inhalt nötig)
- `01`–`NN` = Hauptstationen in echter Gehreihenfolge
- **Buchstaben-Suffix (`01b`, `03b`, …) für nachträglich eingefügte Zwischenstopps** — bewusst statt Durchnummerieren (0004→0005 usw.), um nicht bei jeder Ergänzung alle Folgedateien umbenennen zu müssen. Der Buchstabe hängt an der **vorherigen** Stationsnummer.
- Optionale Stationen außerhalb der Route (`OPT`, `OPT-P`) bekommen keine Zahlnummer.

## 3. Checkliste: neue Station / Zwischenstopp hinzufügen

### 3a. `Unterwegs` — praktische Route (Pflicht, unabhängig davon ob es einen Audioguide gibt)

1. **Koordinate ermitteln** — Nominatim: `https://nominatim.openstreetmap.org/search?q=<Suchbegriff>&format=json`
2. Rundgang-Notiz — **Übersichtstabelle**: neue Zeile inkl. Google-Maps-Link (Format siehe Abschnitt 5)
3. Dieselbe Notiz — **Detail-Abschnitt** `### NNb. Name` mit Ort/Was/Hinweis ergänzen
4. Dieselbe Notiz — **Frontmatter** `stations:` und `distance:` hochzählen
5. **GPX-Datei**: `<wpt>` UND `<trkpt>` (im `<trk>`-Block) an der richtigen Position einfügen — beide, nicht nur eines
6. **Route neu berechnen** (nicht schätzen!) — BRouter-API direkt aufrufen:
   ```bash
   curl -s "https://brouter.de/brouter?lonlats=LON1,LAT1%7CLON2,LAT2%7C...&profile=hiking-mountain&alternativeidx=0&format=gpx" -o /tmp/route.gpx
   grep -o 'track-length="[0-9]*"' /tmp/route.gpx   # Meter
   ```
   `%7C` = URL-encodetes `|` als Trenner zwischen den Punkten (Alternative: `;` im Browser-Link, s. Abschnitt 3c)
7. Neue Distanz/Gehzeit in der Notiz eintragen (Tabelle **und** Frontmatter)
8. **BRouter-Web-Link** in derselben Notiz aktualisieren (neuer Punkt in der `lonlats=`-Kette)
9. **`Stadtrundgänge/README.md`** — Stationsanzahl in der Übersichtstabelle korrigieren
10. **`Doku/Claude – Änderungshistorie.md`** — Eintrag ergänzen (Pflicht laut Vault-Policy für autonome `.md`-Änderungen)
11. GPX-Datei zählt **nicht** als `.md` → fällt technisch unter „Rückfrage nötig", wird über den normalen Tool-Permission-Dialog abgefragt, keine separate Nachfrage nötig

### 3b. `Reise-Guides` — Audioguide (nur falls die Station auch vorgelesen werden soll)

1. Neue Notiz `Reise-Guides/Stadtrundgänge/<Ort>/Audioguide/NNNN - Name.md`, Format:
   ```yaml
   ---
   title: "..."
   tags: [<ort>, audioguide]
   created: YYYY-MM-DD
   poi_number: "NNNN"
   audio: "NNNN - Name.mp3"
   ---
   ```
   danach `![[NNNN - Name.mp3]]`, dann 150–300 Wörter Fließtext (1–2 Min. Sprechzeit), dann **zwingend** ein `---`-Trenner + `## Quellen` mit Markdown-Links — sonst liest die TTS die URLs mit vor.
2. Recherche **per echter Websuche**, nicht aus Trainingswissen — Fakten vor der Nutzung verifizieren, unsichere Punkte im Artikel (nicht im gesprochenen Text) mit Einschränkung kennzeichnen statt zu erfinden.
3. Optional: separate `NNNN - Name - Artikel.md` für Hintergrundwissen (kein Audio, ausführlicher, eigener Quellen-Abschnitt).
4. **mp3 erzeugen** (Skript liegt **im Vault**, nicht im Scratchpad — Scratchpad-Dateien überleben eine Session nicht):
   ```bash
   export OPENAI_API_KEY='sk-...'   # vom User erfragen, nie raten
   python3 "/home/claude/Obsidian-Vaults/Reise-Guides/_scripts/gen_tts.py" \
     "/home/claude/Obsidian-Vaults/Reise-Guides/Stadtrundgänge/<Ort>/Audioguide" \
     "NNNN - Name.md"
   ```
5. **`<Ort> - Übersicht.md`** (Reise-Guides): Stationstabelle ergänzen **und** — falls sich die Route geändert hat — **BRouter-Link + Distanz/Zeit synchron zur `Unterwegs`-Version nachziehen** (siehe Warnung in Abschnitt 1).
6. Veröffentlichen:
   ```bash
   ob publish --path "/home/claude/Obsidian-Vaults/Reise-Guides" --all --dry-run --json   # erst prüfen
   ob publish --path "/home/claude/Obsidian-Vaults/Reise-Guides" --all --yes --json        # dann pushen
   ```
   Bei `EAI_AGAIN`/`fetch failed`: einfach wiederholen (IPv6 ist auf Container 203 nicht erreichbar, rein transientes Problem, siehe Abschnitt 6). Der Push kann vom Auto-Mode-Klassifikator blockiert werden — dann den User bitten, denselben Befehl über `!`-Präfix selbst auszuführen.
7. `Doku/Claude – Änderungshistorie.md` (in `Unterwegs`) — auch für Reise-Guides-Änderungen protokollieren, da es dafür keine eigene Änderungshistorie gibt.

### 3c. GPX in einen anklickbaren BRouter-Web-Link umwandeln

Reihenfolge exakt wie im `<trk>`-Block der GPX, Format `lon,lat` (nicht `lat,lon`!), Punkte mit `;` getrennt:

```
https://brouter.de/brouter-web/#map=14/<lat-mitte>/<lon-mitte>/standard&lonlats=LON1,LAT1;LON2,LAT2;...&profile=hiking-mountain
```

## 4. Neuen Rundgang von Grund auf anlegen (Kurzfassung)

1. `Unterwegs`: Rundgang-Notiz nach dem etablierten Schema in `Stadtrundgänge/<Ort>/` anlegen (Frontmatter, Stationstabelle inkl. `📍`-Spalte, Detail-Abschnitte, GPX-Datei), Zeile in `Stadtrundgänge/README.md` ergänzen.
2. Falls Audioguide gewünscht: in `Reise-Guides` einen neuen Unterordner `Stadtrundgänge/<Ort>/Audioguide/` anlegen, Stationen nach Schema 3b schreiben, `<Ort> - Übersicht.md` als Einstiegsseite anlegen.
3. Publish-Site existiert bereits (`reise-guides`, ein Vault für alle Reisen) — nur `ob publish --all --yes` nötig, keine neue Site anlegen.
4. Passwortschutz der Publish-Site gilt vault-weit, muss nicht pro Rundgang neu gesetzt werden.

## 5. Google-Maps-Link-Format

```
https://www.google.com/maps?q=LAT,LON
```

Öffnet auf dem Smartphone die Google-Maps-App (falls installiert) direkt auf dem Punkt, von dort per Fingertipp navigierbar. Funktioniert auch im Browser. Kein API-Key nötig, keine Kosten.

## 6. Bekannte Fallstricke

- **IPv6 auf Container 203 ist nicht erreichbar** — führt bei `ob publish`, `ob sync` und OpenAI-API-Aufrufen sporadisch zu `EAI_AGAIN`/`fetch failed`. Kein echtes Problem, einfach wiederholen (2–5 Versuche reichen praktisch immer).
- **Obsidian Publish kennt keine `.gpx`-Dateien** — weder als Link noch als Embed werden sie hochgeladen. Die Route auf der Reise-Guides-Seite läuft deshalb nur über den externen BRouter-Web-Link, nicht über eine eingebettete Karte.
- **Map View (`mapview`-Codeblock) funktioniert auf Obsidian Publish nicht** — Community-Plugins werden dort nicht unterstützt. Auf der `Unterwegs`-Seite (normale App) funktioniert die interaktive Karte weiterhin.
- **Auto-Mode-Klassifikator blockiert manchmal den `ob publish --yes`-Push** — auch nach Chat-Bestätigung. Workaround: User führt denselben Befehl selbst mit `!`-Präfix aus.
- **Der API-Key für TTS wird bei Bedarf vom User im Chat eingefügt** — nie in eine Vault-Datei schreiben, nur transient als Env-Var. Bei `/compress` einer solchen Session vorher prüfen, dass der Key nicht in den rohen Session-Log rutscht.
- **`ob sync` manuell aufzurufen ist meist unnötig** — der kontinuierliche Sync-Dienst auf 203 läuft bereits im Hintergrund und synct Änderungen automatisch (`ob sync` meldet dann „Another sync instance is already running").

## 🔗 Verwandte Notizen

- [[../Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus|Le Havre]] — Referenz-Rundgang, nach diesem Muster gebaut
- `Reise-Guides/Stadtrundgänge/Le Havre/Le Havre - Übersicht.md` — Referenz-Audioguide-Übersicht (anderes Vault, kein Wikilink möglich)
- [[../Doku/Claude – Änderungshistorie]] — Protokoll aller Änderungen
- `Knowledge Base/IT@home/Infrastruktur/Proxmox/LXC 201 – Vault-Sync (obsidian-headless + Git-Backup)` — Sync/Publish-Grundlagen (anderes Vault)
