---
title: "GPX-Integration – Setup & Anleitung"
tags:
  - setup
  - gpx
  - plugins
  - kartendarstellung
  - navigation
created: 2026-05-28
modified: 2026-05-28
type: "Anleitung"
---

# 🗺️ GPX-Integration – Setup & Anleitung

Vollständige Anleitung zur Integration von GPX-Routendaten in Obsidian mit Kartensicht und Navigation.

---

## ✅ Schritt 1: Map View Plugin installieren

Das **Map View Plugin** ist das beste Tool für Kartensicht in Obsidian.

### Installation

1. Öffne **Obsidian → Settings** (⚙️)
2. Navigiere zu **Community Plugins** (linke Sidebar)
3. Klicke auf **Browse** (rechts oben)
4. Suche nach **"Map View"** (von dying2live)
5. Klicke **Install**
6. Nach Installation: **Enable** klicken
7. Settings → **Map View** konfigurieren (optional)

### Alternative Plugins

Falls Map View nicht dein Geschmack ist:
- **Leaflet** — einfache eingebettete Karten
- **Track Map** — spezialisiert auf Wanderrouten
- **Obsidian Maps** — mit Offline-Unterstützung

---

## 📍 Schritt 2: Notizen mit Koordinaten versehen

Jede Tour-Notiz braucht diese Frontmatter-Felder für Kartendarstellung:

```yaml
---
title: "Tourname"
coordinates: "LAT°N, LON°E"
gpx_file: "Ordner/Dateiname.gpx"
---
```

**Beispiel:**
```yaml
coordinates: "50.8503°N, 5.6875°E"
gpx_file: "Stadtrundgänge/Maastricht/GPX/Maastricht-Kurztour.gpx"
```

✅ **Status:** Alle Maastricht-Touren bereits aktualisiert!

---

## 🗺️ Schritt 3: GPX-Dateien in Notizen einbinden

### Methode A: Einfache Verlinkung
```markdown
📥 **Route:** [[Stadtrundgänge/Maastricht/GPX/Maastricht-Kurztour.gpx|Herunterladen]]
```

### Methode B: Map View Code Block
Wenn du Map View installiert hast, kannst du die Route visualisieren:

```markdown
```mapview
{"geoDataUrl": "Stadtrundgänge/Maastricht/GPX/Maastricht-Kurztour.gpx", "height": "400px"}
```
```

Diese Codeblock-Syntax zeigt die Route in der Notiz als interaktive Karte an.

### Methode C: Koordinaten-Pin
Für einzelne Orte (ohne komplette Route):

```markdown
```mapview
{"coordinates": [50.8503, 5.6875], "zoom": 15}
```
```

---

## 📥 Schritt 4: GPX-Dateien korrekt speichern

### Ordnerstruktur

```
Vault-Root/
├── Stadtrundgänge/
│   ├── Maastricht/
│   │   ├── Maastricht - Kurztour.md
│   │   ├── GPX/
│   │   │   ├── Maastricht-Kurztour.gpx ✅
│   │   │   ├── Maastricht-Route.gpx ✅
│   │   │   └── Maastricht-Langtour.gpx ✅
│   └── [Andere Städte]/
│       └── GPX/
└── Wanderungen/
    ├── [Region]/
    └── GPX/
```

**Wichtig:** Jede Region sollte einen eigenen `GPX/` Ordner haben.

---

## 📤 Schritt 5: GPX von außerhalb importieren

### Variante A: Komoot (empfohlen)

1. Öffne deine Tour auf **komoot.de**
2. Klicke auf **Teilen** (Pfeil-Icon)
3. Wähle **Export** → **GPX-Datei**
4. Speichere in den passenden `GPX/` Ordner
5. Füge in der Tour-Notiz hinzu:
   ```yaml
   gpx_file: "Stadtrundgänge/[Stadt]/GPX/[Tourname].gpx"
   ```

### Variante B: AllTrails

1. Öffne die Wanderung auf **alltrails.com**
2. Klicke **Download** (Download-Icon)
3. Wähle **GPX** als Format
4. In Vault-Ordner verschieben

### Variante C: Google Maps

1. Öffne deine Route in **Google Maps**
2. Klicke auf **Speichern**
3. Mit **My Maps** öffnen
4. Nutze Tools wie [GPX Converter](https://www.gpxstudio.io/) zur Konvertierung
5. In Vault speichern

### Variante D: Garmin / Fitness-Tracker

1. GPX-Daten von Gerät exportieren
2. In Obsidian `GPX/` Ordner kopieren
3. Tour-Notiz mit Metadaten erstellen

---

## 🎯 Schritt 6: Neue Touren hinzufügen

1. **Template verwenden:** Kopiere [[Ressourcen/Tour-Template]]
2. **Speichere als:** `Wanderungen/[Region]/[Tourname].md`
3. **GPX-Datei:** Kopiere `.gpx` in `Wanderungen/[Region]/GPX/`
4. **Frontmatter ausfüllen:** Koordinaten + gpx_file Feld
5. **Tour-Notiz schreiben:** Stationen, Tipps, Zeiten
6. **Index aktualisieren:** Füge Link zu [[Ressourcen/GPX-Verwaltung]] hinzu

---

## 🔍 Schritt 7: Routen anzeigen & nutzen

### In Obsidian
- Map View lädt GPX automatisch
- Zoom mit Mausrad
- Klick auf Punkte = Informationen

### Unterwegs (Handy)
1. GPX-Datei herunter → auf Handy kopieren
2. Mit **Komoot**, **AllTrails** oder **Maps.me** öffnen
3. Offline-Navigation aktivieren

### Auf Desktop
- Nutze **QGIS** (kostenlos) für detaillierte Analysen
- **GPX Studio** (Online) für schnelle Anpassungen

---

## ✨ Pro-Tipps

### 1. Höhenprofil anzeigen
Map View zeigt automatisch das Höhenprofil von Wanderungen (wenn in GPX enthalten).

### 2. GPX-Dateien editieren
Mit **GPX Editor** (Online) oder **QGIS** kannst du:
- Punkte hinzufügen / löschen
- Route glätten (redundante Punkte entfernen)
- Höhendaten korrigieren

### 3. GPX-Metadaten prüfen
```bash
# Mit einem Text-Editor öffnen und schauen
# oder nutze: https://www.gpxstudio.io/
```

### 4. Automatische Kartenansicht
Im Obsidian Settings kannst du einstellen, dass **alle Notizen mit `coordinates` automatisch mit Karte angezeigt** werden.

---

## 🐛 Häufige Probleme

### Problem: Map View zeigt Route nicht
- **Lösung 1:** Plugin neu starten (Obsidian neustart)
- **Lösung 2:** Pfad zu GPX-Datei prüfen (relative Pfade, keine Leerzeichen vergessen)
- **Lösung 3:** GPX-Datei mit Online-Tool prüfen (https://www.gpxstudio.io/)

### Problem: Koordinaten in falscher Region
- **Lösung:** Frontmatter überprüfen → `coordinates: "LAT°N, LON°E"` im richtigen Format

### Problem: GPX-Datei zu groß / langsamm
- **Lösung:** In GPX Studio aufräumen (redundante Punkte entfernen)

### Problem: Höhendaten fehlen
- **Lösung:** GPX von Komoot/Garmin verwenden (enthalten Elevation)

---

## 📊 Datenformat-Referenz

### Koordinatenformat
```
50.8503°N, 5.6875°E   ✅ Empfohlen
N50° 51' 1.08", E5° 41' 15.00"   ✅ Auch ok
50.8503, 5.6875   ✅ Dezimal (ohne °/N/E auch ok)
```

### GPX-Struktur (vereinfacht)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<gpx version="1.1">
  <metadata>
    <name>Tourname</name>
    <desc>Beschreibung</desc>
  </metadata>
  <wpt lat="50.8503" lon="5.6875">
    <name>Waypoint</name>
  </wpt>
  <trk>
    <name>Route</name>
    <trkseg>
      <trkpt lat="50.8503" lon="5.6875"><ele>100</ele></trkpt>
      ...
    </trkseg>
  </trk>
</gpx>
```

---

## ✅ Checkliste für neue Touren

- [ ] Tour-Notiz erstellt (`Wanderungen/[Region]/[Name].md`)
- [ ] Frontmatter mit: `title`, `region`, `coordinates`, `gpx_file`, `difficulty`, `duration`
- [ ] GPX-Datei in `Wanderungen/[Region]/GPX/` gespeichert
- [ ] Wikilink zu GPX-Datei in Notiz eingefügt
- [ ] Map View Code Block hinzugefügt (optional)
- [ ] Stationen & Sehenswürdigkeiten dokumentiert
- [ ] Praktische Infos: Anreise, Parken, Kosten
- [ ] Link zu [[Ressourcen/GPX-Verwaltung]] hinzugefügt
- [ ] Tags gesetzt (region, schwierigkeit, type)

---

## 📚 Weitere Ressourcen

- **[[Ressourcen/GPX-Verwaltung]]** — Index aller Touren + Downloads
- **[[Ressourcen/Tour-Template]]** — Template für neue Touren
- **Map View Docs:** https://github.com/esm7/obsidian-map-view
- **GPX Validator:** https://www.gpxstudio.io/
- **Komoot:** https://www.komoot.com/
- **AllTrails:** https://www.alltrails.com/

---

*Zuletzt aktualisiert: 2026-05-28*
