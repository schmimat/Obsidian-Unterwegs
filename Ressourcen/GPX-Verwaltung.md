---
title: "GPX-Verwaltung & Route-Downloads"
tags:
  - gpx
  - routen
  - karten
  - download
  - navigation
created: 2026-05-28
modified: 2026-08-12
type: "Referenz"
---

# 🗺️ GPX-Verwaltung & Route-Downloads

Übersicht aller GPS-Routen und deren digitalen Daten im Vault.

---

## 📋 Alle Touren mit GPX-Daten

### 🇳🇱 Maastricht, Niederlande

| Tour | Schwierigkeit | Dauer | Distanz | GPX-Datei | Status |
|------|---------------|-------|---------|-----------|--------|
| [[Stadtrundgänge/Maastricht/Maastricht - Kurztour (2-3h) - mit Epochen\|Kurztour]] | ⭐ Sehr leicht | 2–3 h | 2,5 km | [[Stadtrundgänge/Maastricht/GPX/Maastricht-Kurztour.gpx\|Download]] | ✅ Aktiv |
| [[Stadtrundgänge/Maastricht/Maastricht - Highlights (3-4h) - mit Epochen\|Highlights]] | ⭐ Sehr leicht | 3–4 h | 4 km | — | ⏳ Route fehlt noch |
| [[Stadtrundgänge/Maastricht/Maastricht - Langtour (5-6h) - mit Epochen\|Langtour]] | ⭐⭐ Leicht | 5–6 h | 6 km | [[Stadtrundgänge/Maastricht/GPX/Maastricht-Langtour.gpx\|Download]] | ✅ Aktiv |

---

## 📂 Ordnerstruktur für GPX-Dateien

```
Vault-Root/
├── Stadtrundgänge/
│   └── Maastricht/
│       ├── Maastricht - Kurztour (2-3h) - mit Epochen.md
│       ├── Maastricht - Highlights (3-4h) - mit Epochen.md
│       ├── Maastricht - Langtour (5-6h) - mit Epochen.md
│       └── GPX/
│           ├── Maastricht-Kurztour.gpx
│           └── Maastricht-Langtour.gpx
│           (Highlights-Route fehlt noch)
└── Wanderungen/
    └── [struktur für Wanderungen folgt gleichem Schema]
```

---

## 🔧 GPX mit Obsidian-Plugins anzeigen

### Map View Plugin (empfohlen)

1. **Plugin installieren:**
   - Obsidian Settings → Community Plugins → Browse
   - Suche nach **"Map View"** von dying2live
   - ✅ Install → Enable

2. **GPX-Dateien in Notizen einbinden:**
   ```markdown
   ```mapview
   {"query": "path:\"Maastricht-Kurztour.gpx\"", "autoFit": true}
   ```
   ```
   **Korrigiert (2026-08-12):** Nicht `{"geoDataUrl": "..."}` verwenden — dieses Feld gibt es im Plugin nicht (im Quellcode verifiziert, `src/main.ts`/`src/mapState.ts`). Der `mapview`-Codeblock kennt nur `query`/`mapZoom`/`mapCenter`/`autoFit`; die GPX-Datei wird über den `path:`-Query-Operator angesprochen (Teilstring des Dateinamens genügt). Details: [[Ressourcen/GPX-Setup-Anleitung#✅ Schritt 1: Map View Plugin installieren|GPX-Setup-Anleitung]] Methode B.

3. **Automatische Kartenanzeige:**
   - Notizen mit `coordinates` Frontmatter-Feld zeigen Kartenpins
   - GPX-Dateien werden als eigenständige „Pfad"-Objekte erkannt, sobald sie irgendwo im Vault liegen — das `gpx_file`-Frontmatter-Feld selbst hat für Map View keine Funktion, es dient hier nur als Referenz für uns Menschen/für den `path:`-Query oben

---

## 💾 GPX-Datei Format & Struktur

Jede GPX-Datei enthält:
- **Wegpunkte** (Waypoints) — einzelne markante Orte
- **Tracepoints** (Track) — kontinuierliche Route mit GPS-Koordinaten
- **Metadaten** — Name, Beschreibung, Höhendaten

**Beispiel:** `Maastricht-Kurztour.gpx`
- 📍 Start: Sint Servaasbrug (50.8503°N, 5.6875°E)
- 🎯 Ende: Naturhistorisches Museum (50.8449°N, 5.6880°E)
- 📏 Länge: ca. 2,5 km

---

## 📥 Neue GPX-Dateien importieren

### Option 1: Datei kopieren
```bash
# Windows PowerShell
Copy-Item "C:\Downloads\meine-route.gpx" `
  -Destination ".\Stadtrundgänge\[Region]\GPX\meine-route.gpx"
```

### Option 2: Von Online-Services exportieren

**Komoot:**
1. Tour öffnen → Teilen/Export
2. Format: GPX wählen
3. In den `GPX/` Ordner der entsprechenden Region kopieren

**AllTrails:**
1. Wanderung öffnen → Download
2. GPX-Format wählen
3. In Vault importieren

**Google Maps:**
1. Route planen → Speichern
2. Mit "My Maps" zu GPX exportieren

---

## 🏷️ Frontmatter-Standard für Touren mit GPX

Jede Tour-Notiz sollte folgende Felder enthalten:

```yaml
---
title: "Tour Name"
type: "Stadtrundgang" or "Wanderung"
region: "Name, Land"
difficulty: "Schwierigkeitsstufe"
duration: "x h"
distance: "x km"
elevation_gain: "x m" (bei Wanderungen)
gpx_file: "Ordner/Dateiname.gpx"
coordinates: "LAT°N, LON°E" (Startpunkt)
created: YYYY-MM-DD
modified: YYYY-MM-DD
tags:
  - region
  - type
  - difficulty
---
```

**Beispiel:**
```yaml
---
title: "Maastricht – Kurztour"
type: "Stadtrundgang"
region: "Maastricht, Niederlande"
difficulty: "⭐ Sehr leicht"
duration: "2–3 h"
distance: "2,5 km"
gpx_file: "GPX/Maastricht-Kurztour.gpx"
coordinates: "50.8503°N, 5.6875°E"
---
```

---

## 🎯 Nächste Schritte

- [ ] Map View Plugin installieren
- [ ] Alle Tour-Notizen mit `gpx_file` Feld aktualisieren
- [ ] Wanderungen mit Höhendaten (elevation_gain) hinzufügen
- [ ] Weitere Regionen mit GPX-Dateien erweitern

---

*Zuletzt aktualisiert: 2026-05-28*
