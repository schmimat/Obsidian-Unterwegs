---
tags: [wohnwagen, fahrzeugschein]
created: 2026-06-14
modified: 2026-09-20
---

# Wohnwagen — Fahrzeugdaten

## Hersteller & Modell

| Feld | Wert |
|------|------|
| Hersteller | Bürstner |
| Fahrzeugart | Anhänger Wohnwagen (ANH WOHNWAGEN) |
| Typ-Schlüssel | 4313 |
| Baujahr | 1995 |
| Erstzulassung | 31.01.1996 |
| Kennzeichen | BA NL29 |

## Fahrgestellnummer (FIN/VIN)

`WBU4313TNS2149275`

- `WBU` = Hersteller-Code Bürstner
- `S` (10. Stelle) = Modelljahr 1995

## Abmessungen

| Maß | Wert |
|-----|------|
| Länge | 6.080 mm (6,08 m) |
| Breite | 2.170 mm (2,17 m) |
| Höhe | 2.460 mm (2,46 m) |

## Gewichte

| Bezeichnung | Wert |
|-------------|------|
| Zulässige Gesamtmasse | ❓ bitte aus Fahrzeugschein Feld F.1 ablesen (Vergleichswert Club 465 T 1996: 1.200 kg) |
| Leergewicht | 1.100 kg |

## Ausstattung

| Feld | Wert |
|------|------|
| Schlafplätze | 4 |
| WC | ja |
| Heizung | Truma |
| Kocher | 3-Flammen-Kocher |
| Sitzgruppe | 4er Dinette + Seitensitzgruppe |

## Fahrwerk & Technik

| Feld | Wert |
|------|------|
| Reifen | 185/65R14 84Q |
| Stabilisierungseinrichtung | AL-KO Typ AKS 13 |
| Bremsanlage | Auflaufbremse mit Abreißbremse |

## Kederschiene

| Feld | Wert |
|------|------|
| Innendurchmesser Schiene | 10 mm (Universalstandard) |
| Keder-Durchmesser (original) | 8 mm (ältere Bürstner-Modelle vor ~2000) |
| Keder-Durchmesser (aktueller Standard) | 7 mm |
| Schienenprofil | Ältere Bauform (Kategorie C–F, Baujahre 1990–2005) |
| Untere Kederschiene (Markise) | nicht vorhanden |

**Kompatibilität mit aktuellem Zubehör:**
- Moderne Vorzelte/Markisen mit 7 mm Keder passen, sitzen aber etwas locker
- Clip-on-Adapter neuerer Systeme ggf. nicht kompatibel mit dem Altprofil
- Bei Neuanschaffung: explizit **8 mm Keder** oder „älteres Bürstner-Profil" anfragen

## Sackmarkise — Kompatibilität

Die Kederschiene selbst (10 mm Innendurchmesser) ist bei allen Baujahren gleich — kein Problem. Der kritische Unterschied liegt beim **Keder-Durchmesser des Markisenstoffs**:

| Situation | Folge |
|-----------|-------|
| Neue Markise (7 mm Keder) in alter Schiene (für 8 mm ausgelegt) | Keder sitzt locker → kann bei Wind herausrutschen |
| Zu großer Keder (8 mm) in moderner 7-mm-Schiene | Keder klemmt, lässt sich nicht einschieben |

**Für diesen Wohnwagen (Schiene ausgelegt auf 8 mm):**
- Moderne Sackmarkisen (Dometic, Fiamma, Thule, Wigo) liefern standardmäßig 7 mm Keder
- Risiko: Markise kann sich unter Windlast aus der Schiene lösen

**Lösungsoptionen:**
1. Beim Kauf explizit **8 mm Keder** anfragen
2. **Keder-Adapter** einsetzen (Achtung: Markise sitzt dann weiter von der Wand ab)
3. Schiene selbst nachmessen — falls die Nut **enger als erwartet** ist (näher an 8 mm als an 10 mm), sitzt 7 mm Keder fester und das Herausrutsch-Risiko sinkt

## Stromversorgung

Siehe [[Wohnwagen-Stromversorgung]] — Nespresso Pixie am 12-V-Bordnetz, Wechselrichter, Ladebooster/Solar und Minimalbatterie-Vergleich (LiFePO4 vs. AGM) für eine 1-Tag/Nacht-Überbrückung.

## Defekt: Beleuchtung Toilette flackert (offen, Stand 2026-09-20)

**Symptom:** Leuchtstoffröhre in der Toilette flackert und leuchtet schwach statt normal hell.

**Bereits ohne Erfolg geprüft/getauscht:**
- Komplette Leuchte getauscht → Fehler bleibt (Leuchte selbst also nicht die Ursache)
- Anschlussklemmen gereinigt → Fehler bleibt

**Damit verbleibender Hauptverdacht:** Spannungsversorgung an dieser Stelle — Spannungsabfall über die (30 Jahre alte, dünne) Zuleitung oder eine unter Last einbrechende Bordbatterie. Nächster sinnvoller Test (noch nicht durchgeführt): Spannung unter Last mit Multimeter an drei Punkten vergleichen — Batterie, Sicherungskasten, Leuchte selbst — der größte Spannungssprung markiert die Fehlerstelle.

**Starter-Recherche (2026-09-20):** Die meisten 12-V-Leuchtstoffleuchten dieser Bauzeit sind „Transistorleuchten" mit eingebauter elektronischer Vorschaltung — **kein separater Starter** nötig/vorhanden. Ob das bei dieser Leuchte auch so ist, lässt sich nur durch Öffnen prüfen (kein kleines zylindrisches Starter-Bauteil in der Fassung = Transistorleuchte). Manche ältere 12-V-Leuchten haben stattdessen einen eingebauten 12-V→230-V-Umformer, der eine normale 230-V-Röhre betreibt — falls das hier zutrifft, wäre ein alternder Umformer selbst eine plausible Flacker-Ursache (durch Röhrentausch nicht behebbar).

**Ersatzteil-/LED-Optionen (Recherche 2026-09-20, generischer 12-V-Camping-Markt — Bürstner-Originalersatzteile für ein 1995er Modell nur noch über Fachhändler, für dieses Kleinteil nicht sinnvoll):**

| Produkt | Daten | Preis | Quelle |
|---|---|---|---|
| HABA Röhre für Transistorleuchte 8W 12V | 295 mm, Sockel 8TL, 126 lm warmweiß | 5,00 € | [Camping Langhans](https://www.campinglanghans.de/ersatzteile-shop/ersatzteile-fuer-12-volt-geraete-ersatzteile-fuer-220-volt/ersatzteile-fuer-12-volt220-volt-leuchtmittel/22077/haba-roehre-fuer-transistorleuchte-8w-12-v) |
| Dometic 12V LED-Tube | 47,4 × 2,5 × 2,1 cm, direkt 12-V-DC, kein Vorschaltgerät nötig | ~33 € | [Obelink](https://www.obelink.de/dometic-12v-led-tube.html) |
| Generische 12V-T8-LED-Röhren | diverse Längen | variabel | [eBay](https://www.ebay.de/shop/12v-led-roehre?_nkw=12v+led+r%C3%B6hre), [Reimo](https://www.reimo.com/camping-shop/elektrik-fuer-wohnmobile-batterien/leuchtmittel-kfz-bereich-12v/) |

Vor Bestellung: Röhre ausbauen, Länge + Sockeltyp abgleichen. Echte 12-V-DC-LED-Röhren brauchen keinen Starter/kein Vorschaltgerät — falls die alte Elektronik (Transistor-Vorschaltung oder Umformer) die eigentliche Ursache ist, umgeht eine LED-Röhre das Problem eher als ein reiner Röhrentausch.

**Offen:** Multimeter-Spannungsvergleich (Batterie/Sicherungskasten/Leuchte) noch nicht durchgeführt; Öffnen der Fassung zur Starter-Prüfung noch nicht erfolgt.

## Quellen

- [[BUERSTNER Club 4313 in Bad HonnefRottbitze -  in Bad HonnefRottbitze]] (Vergleichsinserat)
- [[Marktübersicht Sackmarkisen Sonnenschutz und Vorzeltdach für Wohnwagen im Paket]] (Modellübersicht Dometic, Fiamma, Thule, Wigo)
- [Kederschienen und passende Keder — hummelladen.de](https://hummelladen.de/blogs/camping/kederschienen-und-passende-keder) (Kompatibilitätstabelle Innendurchmesser/Keder-Durchmesser)
- [Kederschiene Kederleiste Modell — cara-kedersystem.de](https://cara-kedersystem.de/kederschiene-kederleiste/) (Schienenprofile nach Baujahr, Kategorien A–H)
- [Sackmarkise mit Kederadapter — wohnwagen-forum.de](https://wohnwagen-forum.de/forum/thread/198240-sackmarkise-mit-kederadapter-leichter-montieren/) (Erfahrungsbericht Adapter)

## Zulassungsdokument

| Feld | Wert |
|------|------|
| Dokument-Nr. | BA-S-0-115/17-00055... |
| Zulassungsbehörde | Bamberg |
| Zulassung am | 31.01.1996 |
