---
tags:
  - aufgabe
  - le-havre
  - audioguide
  - tts
  - lxc203
  - obsidian-sync
type: Arbeitsauftrag
bearbeiter: Claude Code auf LXC 203 (Obsidian-Sync-Reichweite, kein Host-Admin-Zugriff nötig)
status: offen
prioritaet: gering — Reise-Nice-to-have, kein Blocker für den Rundgang selbst
created: 2026-08-17
modified: 2026-08-17
---

# Aufgabe – Audio-Guide „Le Havre" erstellen (LXC 203)

> Diese Aufgabe ist eigenständig verfasst — die ausführende Session kennt die Planungs-Session nicht, in der sie entstand. Aller nötige Kontext steht unten.

---

## 1. Ziel

Der User plant einen Stadtrundgang durch Le Havre (Normandie) zum Thema Perret-Wiederaufbau (UNESCO-Welterbe seit 2005) und Impressionismus. Es gibt bereits eine ausführliche Rundgang-Notiz mit Öffnungszeiten, Adressen, Route und GPX: [[Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]].

**Diese Aufgabe hier ist etwas anderes:** ein separates, kleines Zusatz-Vault mit Audio-Dateien, die der User und seine Frau sich während des Rundgangs unterwegs am Handy anhören können — pro Station eine kurze historische Erzählung, keine praktischen Infos (die stehen schon in der verlinkten Notiz).

**Nutzer-Entscheidungen aus der Planungs-Session (bereits getroffen, nicht mehr offen):**
- Bereitstellung über **Obsidian Sync** (bestehende 201/203-Infrastruktur) — **kein** Web-Tunnel, keine Öffnung des Containers zum Internet
- TTS über eine **Cloud-API** (empfohlen: OpenAI TTS) statt lokal/offline

## 2. Ist-Zustand

- Die Rundgang-Notiz [[Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]] existiert bereits mit 13 Stationen in Laufreihenfolge, GPX-Route, Öffnungszeiten und Parkplätzen.
- Ein Audio-Guide-Vault existiert noch nicht.
- Ob ein OpenAI-API-Key (oder alternativ ElevenLabs) auf Container 203 verfügbar ist, ist **nicht bekannt** — das ist der wahrscheinlichste Blocker beim Start dieser Aufgabe.

## 3. Was zu tun ist

### 3.1 Neues Vault anlegen

Eigenständiges, neues Obsidian-Vault (nicht Unterordner in `Unterwegs`), z. B. `Le-Havre-Audioguide` — Name/exakter Pfad nach der auf 201/203 etablierten Konvention für neue Vaults, siehe Referenz in Abschnitt 5.

```
Le-Havre-Audioguide/
├── 0000 - Einführung.md
├── 0000 - Einführung.mp3
├── 0001 - Catène de conteneurs.md
├── 0001 - Catène de conteneurs.mp3
├── 0002 - Maison de l'Armateur.md
├── 0002 - Maison de l'Armateur.mp3
├── 0003 - Cathédrale Notre-Dame.md
├── 0003 - Cathédrale Notre-Dame.mp3
├── 0004 - Les Halles Centrales.md
├── 0004 - Les Halles Centrales.mp3
├── 0005 - Église Saint-Joseph.md
├── 0005 - Église Saint-Joseph.mp3
├── 0006 - Le Volcan.md
├── 0006 - Le Volcan.mp3
├── 0007 - Appartement témoin Perret.md
├── 0007 - Appartement témoin Perret.mp3
├── 0008 - Hôtel de Ville.md
├── 0008 - Hôtel de Ville.mp3
├── 0009 - Quartier Perret & Avenue Foch.md
├── 0009 - Quartier Perret & Avenue Foch.mp3
├── 0010 - Porte Océane.md
├── 0010 - Porte Océane.mp3
├── 0011 - Plage.md
├── 0011 - Plage.mp3
├── 0012 - Victor by Milot.md
├── 0012 - Victor by Milot.mp3
├── 0013 - MuMa.md
└── 0013 - MuMa.mp3
```

Die Nummern entsprechen exakt der Stationsreihenfolge in [[Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]] (00 Parkplatz ist dort keine eigene Audiostation; 01–13 = Gehreihenfolge, 13 = MuMa als Abschluss).

### 3.2 Format pro Notiz

```markdown
---
title: "<Name>"
tags: [le-havre, audioguide]
created: <heutiges Datum>
poi_number: <0000-0013>
audio: "<Dateiname>.mp3"
---

![[<Dateiname>.mp3]]

<Fließtext, 100–200 Wörter für kurze Stationen, bis 300–400 Wörter für MuMa/Saint-Joseph/Appartement témoin — so lang, wie man dort realistisch verweilt>
```

Der Audio-Embed `![[datei.mp3]]` ist native Obsidian-Funktion, kein Plugin nötig.

### 3.3 Inhaltliche Vorgabe — wichtig

**Nur historisch/interessant, keine Praxis-Infos.** Explizit nicht: Öffnungszeiten, Eintrittspreise, Adressen, Anfahrt, Parkplätze — das steht bereits in [[Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]] und würde in einer Audio-Erzählung nur stören. Ton: erzählend, wie ein Audioguide, nicht wie eine Faktenliste.

### 3.4 Bereits recherchiertes Material (Ausgangsbasis, gegenchecken wo markiert)

**0000 Einführung:** Le Havre wurde im September 1944 durch alliierte Bombardierung fast vollständig zerstört (ca. 5.000 zivile Todesopfer, ~80 % der Innenstadt). Auguste Perret baute die Stadt 1945–1964 komplett neu, aus Sichtbeton, auf einem einheitlichen 6,24-m-Raster. Seit 2005 UNESCO-Welterbe — eine Seltenheit für Nachkriegsarchitektur des 20. Jh., gewürdigt für den „innovativen Umgang mit dem Potenzial von Beton" und die Kohärenz des gesamten Wiederaufbauplans als städtebauliche Komposition. Vor dem Krieg war Le Havre einer der großen transatlantischen Passagierhäfen Frankreichs.

**0001 Catène de conteneurs:** Vincent Ganivet, 2017, ein Doppelbogen aus gestapelten, bemalten Frachtcontainern — Kunst, die direkt auf die Kernindustrie des Hafens (Containerumschlag) verweist. Entstand im Rahmen von „Un Été Au Havre" zum 500. Stadtjubiläum.

**0002 Maison de l'Armateur:** Reederhaus, erbaut um 1790 ⚠️ *(genauer Bauherr/Name gegenchecken — im Zusammenhang mit dem Le Havrer Handelsbürgertum, Dreieckshandel)*. Oktogonaler Lichtschacht über fünf Stockwerke, die Treppe windet sich spiralförmig darum. Gilt als eines der besten Beispiele bürgerlicher Wohnarchitektur des 18. Jh. in Frankreich — und als einer der ganz wenigen Vorkriegsbauten der Innenstadt, die 1944 überstanden haben.

**0003 Cathédrale Notre-Dame:** Mischung aus Gotik und Renaissance, im Krieg beschädigt, aber erhalten — einer der wenigen Vorkriegsbauten im Zentrum. Der Turm diente historisch einlaufenden Schiffen als Landmarke.

**0004 Les Halles Centrales:** Markthallen als Treffpunkt des Alltagslebens.

**0005 Église Saint-Joseph:** Perrets Meisterwerk, 107 m Betonturm. Als Mahnmal für die ca. 5.000 im Bombardement getöteten Einwohner gedacht und zugleich als Landmarke für heimkehrende Seeleute — fast wie ein Leuchtturm. Innen ein Lichtschacht, gefüllt mit 12.768 farbigen Glasstücken von Marguerite Huré, nach Himmelsrichtung gestaffelt — das Licht wandert mit der Sonne durch den Raum. Perret starb 1954, die Kirche wurde von seinem Atelier fertiggestellt.

**0006 Le Volcan:** Oscar Niemeyer, 1982 ⚠️ *(gilt oft als „einziges Niemeyer-Bauwerk in Frankreich" — gegenchecken, ggf. mit Einschränkung erwähnen)*. Weißer Betonkegel als bewusster Kontrast zu Perrets strengem rechtwinkligem Raster ringsum. Enthält Theater und die frei zugängliche Mediathek „Petit Volcan".

**0007 Appartement témoin Perret:** Original möblierte Musterwohnung von 1955, zeigt, wie sich die Bewohner nach der Totalzerstörung ihren neuen Alltag einrichteten — funktionale Nachkriegsmoderne, Einbaumöbel, für die Zeit moderne Küche.

**0008 Hôtel de Ville:** Perrets Rathaus mit Turm, Ankerpunkt und Bezugspunkt des gesamten Wiederaufbaurasters.

**0009 Quartier Perret / Avenue Foch:** Das eigentliche UNESCO-Objekt ist das *Ensemble*, nicht ein Einzelbau. Die Avenue Foch soll breiter angelegt sein als die Champs-Élysées ⚠️ *(Zahl gegenchecken)*, mit durchlaufenden Perret-Wohnblöcken auf demselben 6,24-m-Modul. Rationale, vorfabrizierte Bauweise als pragmatische Antwort auf die akute Wohnungsnot nach 1945.

**0010 Porte Océane:** „Tor zum Meer" — als zeremonieller Abschluss der Avenue Foch gedacht, öffnet die wiederaufgebaute Stadt symbolisch wieder zum Meer, zu ihrer maritimen Identität.

**0011 Plage:** Kiesstrand mit bunten Badekabinen, bei klarer Sicht Blick über die Seine-Mündung Richtung Honfleur/Sainte-Adresse — Freizeitzone direkt neben dem Industriehafen.

**0012 Victor by Milot:** Pommes-Imbiss seit 1927 — hat die Zerstörung 1944 überstanden bzw. besteht als Institution schon länger als die wiederaufgebaute Stadt drumherum, fester Teil der Strandkultur.

**0013 MuMa:** Bau von Guy Lagneau, 1961 eröffnet — das erste in Frankreich nach dem Krieg neu errichtete Museum. Zweitgrößte Impressionisten-Sammlung Frankreichs nach dem Musée d'Orsay. Starke Bestände von Eugène Boudin (aus der Region, Lehrer/Einfluss des jungen Monet) und Raoul Dufy (gebürtiger Le Havrer). Die Glasfassade flutet die Räume bewusst mit genau dem Küstenlicht, das die ausgestellten Maler gemalt haben.

**Wichtig:** Die mit ⚠️ markierten Punkte per Websuche verifizieren, bevor sie als gesprochener „Fakt" verwendet werden — Audioguide-Inhalte sollten stimmen.

### 3.5 TTS-Erzeugung

**Cloud-API, empfohlen: OpenAI TTS** (`tts-1-hd` für gute Qualität, Endpoint liefert direkt `mp3` — keine Konvertierung nötig).

```bash
curl https://api.openai.com/v1/audio/speech \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "tts-1-hd",
    "input": "<Text der Notiz>",
    "voice": "onyx",
    "response_format": "mp3"
  }' \
  --output "0005 - Église Saint-Joseph.mp3"
```

- Stimme: `onyx` oder `nova` sind für erzählenden Ton gut geeignet — gerne selbst probehören und anpassen.
- API-Key muss auf dem Container als Env-Var verfügbar sein (`$OPENAI_API_KEY`) — **falls nicht vorhanden, hier stoppen und beim User nachfragen**, nicht raten oder einen anderen Dienst ungefragt einrichten.
- Kostenschätzung: 14 Dateien × ~150–250 Wörter ≈ 15.000–20.000 Zeichen gesamt → im niedrigen Cent- bis unteren Euro-Bereich. Grobe Schätzung, aktuelle Preise bei OpenAI vor Ausführung prüfen.
- Alternative falls kein OpenAI-Key vorhanden: ElevenLabs (ähnliches Prinzip, anderer Endpoint).

### 3.6 Vault + Sync

1. Neues Vault-Verzeichnis anlegen (Struktur s. o.).
2. In die bestehende Obsidian-Sync-Konfiguration auf 201/203 aufnehmen — gleiches Muster wie bei den anderen Vaults auf diesem Container (`ob sync-config`, `community-plugin`-Kategorie **nicht** nötig für reine Audio-Embeds, das ist Obsidian-Bordmittel). Referenz: `Knowledge Base/IT@home/Infrastruktur/Proxmox/LXC 201 – Vault-Sync (obsidian-headless + Git-Backup)` — dort steht das bereits etablierte Vorgehen für neue Vaults auf diesem Setup. *(Cross-Vault-Wikilink funktioniert in Obsidian nicht — Pfad ist als Klartext angegeben, siehe [[../CLAUDE.md]].)*
3. Sync-Client so konfigurieren, dass beide Handys (User + Ehefrau) das neue Vault erhalten — falls für die Ehefrau noch kein Sync-Zugriff eingerichtet ist, das vorher beim User klären, das ist eine eigene kleine Vorab-Aufgabe.
4. **Kein Webserver, kein Tunnel, keine Portfreigabe** — explizite User-Entscheidung.

## 4. Wer das ausführen darf

**LXC 203** ist für diese Aufgabe vorgesehen — anders als reine Infrastruktur-Aufgaben (Firewall, SSH, Host-Konfiguration), die laut den `Aufgaben/`-Konventionen im Knowledge-Base-Vault ausdrücklich **nicht** von 203 ausgeführt werden sollen. Diese Aufgabe braucht keinen Host-Admin-Zugriff — nur Obsidian-Sync-Reichweite (die 203 ohnehin hat) und einen API-Aufruf gegen eine externe TTS-API. Passt damit zum dokumentierten Einsatzzweck von 203 als Vault-Bearbeiter.

## 5. Leitplanken

- **Kein Web-Tunnel, keine Portfreigabe, keine Öffnung des Containers zum Internet** — explizite User-Entscheidung gegen diese Alternative, nicht selbst revidieren.
- **API-Key nicht vorhanden → nachfragen, nicht raten.** Kein zweiter TTS-Dienst ungefragt einrichten, wenn OpenAI nicht verfügbar ist.
- **⚠️-markierte Fakten (Abschnitt 3.4) vor Verwendung verifizieren** — falsche „historische Fakten" in einem Audioguide sind schlechter als gar keine Angabe.
- **Keine Öffnungszeiten/Preise/Adressen in den POI-Texten** — Abgrenzung zur bestehenden Rundgang-Notiz bewusst einhalten.
- Das ist ein **temporäres Zusatz-Vault** für einen einzelnen Ausflug — muss nicht ins langfristige Frontmatter-Schema der anderen `Unterwegs`-Kategorien passen (siehe Frontmatter-Schema-Abschnitt in [[../CLAUDE.md]] — bewusst uneinheitlich, jede Kategorie hat ihr eigenes Schema).
- Änderungen an dieser Aufgaben-Datei selbst (Statusupdate bei Fertigstellung) unter der normalen Vault-Policy — gehören in [[../Doku/Claude – Änderungshistorie]].

## 6. Abnahme

- [ ] Vault mit 14 Notizen (0000–0013) + 14 mp3-Dateien angelegt
- [ ] Reihenfolge/Nummerierung entspricht der Gehreihenfolge aus [[Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]]
- [ ] Kein Text enthält Öffnungszeiten/Preise/Adressen
- [ ] ⚠️-markierte Fakten verifiziert oder mit Einschränkung umformuliert
- [ ] Vault synct über 201/203 auf beide Handys, mp3s dort offline abspielbar getestet (nicht erst vor Ort merken, dass Mobilfunk in Frankreich fehlt)
- [ ] Kein Webserver/Tunnel/offener Port eingerichtet

## 🔗 Verwandte Notizen

- [[Stadtrundgänge/Le Havre/Le Havre - Perret-Wiederaufbau & Impressionismus]] — die praktische Rundgang-Notiz (Öffnungszeiten, Route, GPX, Parkplätze), Quelle der Stationsreihenfolge
- `Knowledge Base/IT@home/Infrastruktur/Proxmox/LXC 201 – Vault-Sync (obsidian-headless + Git-Backup)` — Vorgehen für neue Vaults auf 201/203 (anderes Vault, kein Wikilink möglich)
- [[../Doku/Claude – Änderungshistorie]] — hier den Fertigstellungsstatus eintragen
