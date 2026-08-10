# 📍 GPX-Datei & Stadtplan – Anleitung

---
tags:
  - gpx
  - navigationn
  - maastricht
  - anleitung
created: 2026-05-27
modified: 2026-05-27
---

## 📁 Verfügbare GPX-Dateien

| Datei | Tour | Stationen | Größe |
|-------|------|-----------|-------|
| **Maastricht-Kurztour.gpx** | Kurztour (2–3h) | 8 | ~8 KB |
| **Maastricht-Route.gpx** | Highlights (3–4h) | 15 | ~12 KB |
| **Maastricht-Langtour.gpx** | Langtour (5–6h) | 16 | ~14 KB |

---

## 🗺️ GPX-Datei verwenden

Jede Datei (`Maastricht-*.gpx`) enthält die Route mit allen Stationen und Koordinaten.

### **Option 1: Mit Google Maps (Einfach)**

1. Gehe zu [google.com/maps](https://google.com/maps)
2. Oben links: Hamburger Menü ☰ → **Meine Orte**
3. **Importieren** → Wähle `Maastricht-Route.gpx`
4. Die Route wird als Karte angezeigt mit allen Waypoints ✅

### **Option 2: Mit OpenStreetMap (Kostenlos, offline-freundlich)**

1. Gehe zu [openstreetmap.org](https://openstreetmap.org)
2. Rechts oben: **Share** → **Import GPX**
3. Lade `Maastricht-Route.gpx` hoch
4. Route ist jetzt sichtbar & zoombar

### **Option 3: Mit einer GPS-App (Handy)**

**Android (OrganicMaps – kostenlos & offline):**
1. App: [OrganicMaps](https://organicmaps.app/)
2. Datei auswählen → `Maastricht-Route.gpx`
3. Route wird angezeigt, kan offline navigiert werden ✅

**iOS (Maps+, Alltrails oder ähnlich):**
1. App auswählen (z.B. Maps+ oder Komoot)
2. GPX-Datei importieren
3. Offline Navigation möglich

### **Option 4: Mit Garmin/TomTom GPS-Gerät**

- Datei einfach ins `Activities/` oder `Tracks/` Verzeichnis kopieren
- Gerät liest die .gpx automatisch

---

## 📸 Screenshot des Stadtplans selbst erstellen

Leider kann ich keinen echten Screenshot machen, aber hier ist die **Anleitung zum Selbermachen** (5 Minuten):

### **Schritt 1: OpenStreetMap öffnen**

Gehe zu [openstreetmap.org](https://openstreetmap.org)

### **Schritt 2: Auf Maastricht zoomen**

- Suchfeld oben links: `Maastricht, Netherlands`
- Enter
- Stadtplan ist jetzt im Fenster

### **Schritt 3: Route zeichnen (optional)**

Wenn du die Route manuell zeichnen möchtest (mit den Stationen):
1. Klick auf **"Edit"** (oben links, nur wenn du den Editor kennst) — **ODER**
2. Nutze stattdessen die Werkzeuge auf der rechten Seite

**Einfacher Workaround:** Nutze Google Maps (Option 1 oben) — dort wird die importierte GPX-Route automatisch visualisiert!

### **Schritt 4: Screenshot machen**

- Öffne Google Maps (mit importierter GPX)
- Passe den Zoom an (sodass die ganze Route sichtbar ist)
- **Windows:** `Win + Shift + S` → Bereich wählen → Screenshot
- **Mac:** `Cmd + Shift + 4` → Bereich wählen → Screenshot
- **Linux:** `Gnome Screenshot` oder `Flameshot`

### **Schritt 5: Screenshot in Obsidian einbinden**

1. Screenshot speichern unter: `Touren/Stadtrundgänge/Screenshots/`
2. Benennung: `Maastricht-Stadtplan-Route.png`
3. In der `.md`-Datei einfügen:

```markdown
![[Touren/Stadtrundgänge/Screenshots/Maastricht-Stadtplan-Route.png]]
```

---

## 📄 PDF exportieren

Obsidian kann die `.md`-Datei direkt als PDF exportieren:

### **In Obsidian:**

1. Öffne `Touren/Stadtrundgänge/Maastricht - Altstadt Highlights.md`
2. Oben rechts: **Mehr (⋯)** → **PDF-Export** *(falls Plugin installiert)*
3. Falls nicht vorhanden: **Einstellungen** → **Community Plugins** → Suche **"PDF Export"** → Installieren

### **Alternative: Mit Markdown Editor (z.B. Pandoc)**

```bash
# Installation (falls nicht vorhanden)
# Windows: choco install pandoc
# Mac: brew install pandoc
# Linux: sudo apt install pandoc

# Konvertierung
pandoc "Touren/Stadtrundgänge/Maastricht - Altstadt Highlights.md" -o "Maastricht-Stadtrundgang.pdf"
```

### **Alternative: Im Browser als PDF speichern**

1. Öffne `.md` in einem Online-Markdown-Viewer (z.B. [stackedit.io](https://stackedit.io))
2. Paste den Inhalt
3. **Export** → **PDF**

---

## 📋 Verwendete Tools & Formate

| Tool | Zweck | Download |
|------|-------|----------|
| **Google Maps** | GPX importieren & visualisieren | [maps.google.com](https://maps.google.com) |
| **OpenStreetMap** | Kostenlose Online-Karte | [openstreetmap.org](https://openstreetmap.org) |
| **OrganicMaps** | Offline GPS Navigation | [organicmaps.app](https://organicmaps.app) |
| **Pandoc** | Markdown → PDF Konvertierung | [pandoc.org](https://pandoc.org) |

---

## 🎯 Checkliste vor der Tour

- [ ] GPX-Datei in dein Handy/GPS importiert
- [ ] Screenshot von Google Maps mit Route gemacht
- [ ] PDF zum Ausdrucken erzeugt (optional)
- [ ] Bequeme Schuhe
- [ ] Wasser & Snacks
- [ ] Kamera bereit!

---

**Happy Wandering! 🥾🗺️**
