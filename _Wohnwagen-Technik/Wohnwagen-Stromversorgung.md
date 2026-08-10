---
tags: [wohnwagen, strom, batterie, technik]
created: 2026-08-02
modified: 2026-08-03
---

# Stromversorgung Wohnwagen — Powerstation-Lösung für Kaffee, Kühlschrank & Pumpen

Dokumentation der Lösung für eine autarke 1-Tag/Nacht-Überbrückung des Bürstner Club 4313 ohne Landstrom: Nespresso Pixie, eingebauter Kühlschrank, Wasserpumpe/Toilettenspülung. Vorgabe: **Plug-in-Lösung ohne Eingriff in die Wohnwagen-Elektrik** — keine feste Verkabelung, keine Veränderung am Bordnetz.

## Empfehlung im Überblick

| Verbraucher | Betriebsart | Versorgung |
|---|---|---|
| Nespresso Pixie (1.260 W, bis zu 5 Tassen) | 230 V über Powerstation-Steckdose | Powerstation direkt |
| Kühlschrank (Absorberkühlschrank) | **Gas** (nicht elektrisch) | Gaskartusche/-flasche des Wohnwagens |
| Wasserpumpe / Toilettenspülung | 12 V über Bordnetz | Powerstation → CEE-Einspeisedose → eingebautes Bordladegerät |

**Kernaussage:** Eine All-in-one-Powerstation deckt Kaffee sowie Pumpen/Licht komfortabel für eine Nacht ab, ganz ohne Installation. Der Kühlschrank läuft dabei auf **Gas** — seiner vorgesehenen Betriebsart für den Stand ohne Landstrom — weil sein Stromverbrauch im 230-V-Modus (2–4,5 kWh/Tag) die Powerstation sonst nahezu leerziehen würde.

## Nespresso Pixie — technische Eckdaten

| Feld | Wert |
|------|------|
| Leistungsaufnahme | 1.260 W |
| Pumpendruck | 19 bar |
| Standby-Verbrauch | 0 W (schaltet nach ca. 9 Min. automatisch ab) |
| Energieverbrauch/Tasse | ca. 20–30 Wh (Rechengrundlage: 25 Wh) |

**Direkter 12-V-Betrieb ist nicht möglich** — die Pixie braucht 230 V Wechselstrom (bei 12 V wären ~105 A nötig, nicht praktikabel). Sie läuft daher immer über den 230-V-Ausgang der Powerstation.

## Die Powerstation-Lösung

Eine **All-in-one-Powerstation** (LiFePO4-Akku + reiner-Sinus-Wechselrichter + Ladeelektronik in einem Gehäuse) deckt Kaffee, Pumpen und Licht ab. Sie wird einfach in den Wohnwagen gestellt — **keine Veränderung am Bordnetz nötig**.

### Ladeoptionen ohne Umbau

- **230-V-Steckdose** (Campingplatz-Landstrom oder zuhause) — Netzteil liegt bei
- **12-V-Kfz-/Zigarettenanzünder-Buchse** — langsamer (~100–120 W), aber ohne jeden Eingriff nutzbar
- **Solarpanel** (separat, per MC4/DC-Stecker) — ebenfalls ohne Eingriff in die Bordelektrik

### Modellvergleich (passend zur Pixie, 1.260 W Bedarf)

| Modell | Kapazität | AC-Ausgang | Preis | Anmerkung |
|---|---|---|---|---|
| **Jackery Explorer 1000 v2** | 1.070 Wh, LiFePO4 | 1.500 W (3.000 W Spitze) | ab **~494 €** (Geizhals) | 240 W Reserve über Pixie-Bedarf; auch bei Fritz Berger Campingbedarf gelistet |
| EcoFlow Delta 2 | 1.024 Wh, LiFePO4 | 1.800 W (X-Boost bis 2.400 W) | ab **~502 €** (Geizhals) | Mehr Leistungsreserve, schnelleres Laden (80 % in ~50 Min. an 230 V) |

**Empfehlung: Jackery Explorer 1000 v2 (~494 €)** — 1.500 W AC-Ausgang deckt die Pixie mit Reserve ab, keine Installation nötig: einfach in den Wohnwagen stellen, per Steckdose/Kfz-Buchse/Solarpanel laden, bei Bedarf mitnehmen.

## Anschluss ans Bordnetz — 230-V-Einspeisung

Das 230-V-Kabel der Powerstation wird in die **CEE-Einspeisedose** des Wohnwagens (von außen) gesteckt — genau das normale Landstrom-Prinzip vom Campingplatz, die Powerstation ersetzt nur die Steckdose des Platzes.

- **Kühlschrank:** hat einen eigenen 230-V-Heizstab und würde direkt am Wechselstrom laufen — **wird hier aber bewusst nicht genutzt**, siehe Kapazitäts-Check unten. Stattdessen Gasbetrieb.
- **Wasserpumpe / Toilettenspülung:** echte 12-V-Verbraucher, versorgt vom eingebauten Bordladegerät (z. B. Schaudt, Sargent, Nordelettronica), das die eingespeisten 230 V intern in 12 V für das Bordnetz wandelt. Kein Eingriff in die Verkabelung nötig, das ist bereits so verbaut.

### Wirkungsgrad / Wandlungsverluste

| Verbraucher | Wandlungsweg | Verlust |
|---|---|---|
| Kühlschrank (falls 230-V-Modus genutzt würde) | nur 1× Wechselrichter (12 V → 230 V), ~85–90 % Wirkungsgrad | ~10–15 % |
| Pumpen (echte 12-V-Verbraucher) | Wechselrichter (12 V→230 V) **+** Bordladegerät (230 V→12 V) | ~20–35 % (Beispiel: 0,88 × 0,85 ≈ 0,75) |

Der höhere Verlust bei den Pumpen ist praktisch kaum relevant, da sie nur kurz beim Gebrauch laufen (wenige Wh pro Spülung/Wasserzapfen).

## Kühlschrank-Kapazitätsrechnung — warum Gas statt Strom

Der eingebaute Absorberkühlschrank verbraucht im 230-V-Modus deutlich mehr, als eine portable Kompressor-Kühlbox verbrauchen würde:

| Kenngröße | Wert |
|---|---|
| Heizelement 230-V-Modus | ca. 125 W (typisches Beispiel Thetford N4145A) |
| Tagesverbrauch 230-V-Modus | ca. **2–4,5 kWh/24 h** (Absorberkühlschränke sind thermodynamisch ineffizient — hoher Verbrauch für vergleichsweise wenig Kühlleistung) |
| Geschätzter Bedarf für eine Nacht (~10–12 h) | ca. **1.000–1.500 Wh**, je nach Außentemperatur und Kühlbedarf |

Das würde die Jackery Explorer 1000 v2 (1.070 Wh) fast vollständig leerziehen — für die 5 Kaffee am nächsten Morgen (~140 Wh) bliebe kaum Reserve.

**Deshalb: Kühlschrank nachts auf Gas betreiben** (seine vorgesehene Betriebsart für den Stand ohne Landstrom), Powerstation nur für Kaffee + Pumpen/Licht. In dieser Kombination reicht die Jackery Explorer 1000 v2 mühelos mit viel Reserve.

**Nur falls der Kühlschrank zusätzlich zwingend elektrisch (ohne Gas) über Nacht laufen soll:** Dann wäre eine deutlich größere Powerstation nötig (~2.000-Wh-Klasse, z. B. EcoFlow Delta 2 Max oder Jackery Explorer 2000 Plus, ca. 800–1.200 €+) — spürbar teurer und schwerer.

**Wichtig:** Kühlschrank generell nicht im 12-V-Modus betreiben — der ist ungeregelt und zieht sehr hohen Strom (nur zum Temperaturhalten während der Fahrt gedacht, nicht zum Herunterkühlen im Stand). Der 230-V-Modus ist thermostatgeregelt, aber wie oben gezeigt trotzdem zu energiehungrig für die Powerstation im Nachtbetrieb.

## Sonderfall: Kühlschrank auf Dauerplus verdrahtet (läuft auch ohne Zündung)

Bei diesem Gespann ist der Kühlschrank abweichend vom Standard **auf Dauerplus verdrahtet** (läuft auch ohne Zündung) — bewusst in Kauf genommen, mit manuellem Abschalten bei längeren Pausen.

**Hintergrund:** Die 13-polige Anhängersteckdose hat normalerweise zwei getrennte Pins — Pin 9 (Dauerplus, immer aktiv, für schwache Dauerverbraucher wie die Wasserpumpe gedacht) und Pin 10 (geschaltetes Plus, nur bei laufendem Motor, dort hängt normalerweise der Kühlschrank dran) — genau damit der Kühlschrank die Autobatterie im Stand nicht leerzieht. Bei diesem Gespann ist der Kühlschrank stattdessen auf Dauerplus gelegt.

### Wie lange dauert es, bis die Autobatterie den Motorstart gefährdet?

**Formel:** Zeit bis Start unsicher wird ≈ (Batteriekapazität in Ah × 0,5) ÷ Stromaufnahme des Kühlschranks in A

- Nutzbare Reserve: praktisch ~50 % der Nennkapazität (schon deutlich vor der technischen „Leer"-Schwelle von 10,5 V Ruhespannung sackt die Spannung unter Anlasser-Last zu weit ab)
- Absorberkühlschränke ziehen im 12-V-Modus ungeregelt viel Strom: **~14–16 A** üblich (kleinere Modelle ~8–10 A) — genauer Wert steht auf dem Typenschild des Kühlschranks

| Autobatterie | Nutzbar (50 %) | bei 14 A | bei 8 A |
|---|---|---|---|
| 60 Ah (kompakter PKW) | 30 Ah | ~2,1 Std. | ~3,8 Std. |
| 70 Ah (Kombi/Diesel) | 35 Ah | ~2,5 Std. | ~4,4 Std. |
| 90 Ah (größerer SUV/Zugfahrzeug) | 45 Ah | ~3,2 Std. | ~5,6 Std. |

**Grobe Hausnummer: ca. 2–4 Stunden**, abhängig von Batteriegröße/-alter, Außentemperatur (Kälte verschärft) und der exakten Stromaufnahme. Als Sicherheitsmarge empfiehlt sich, eher konservativ nach 1,5–2 Stunden abzuschalten, solange die genauen Werte nicht bekannt sind.

**ToDo — konkrete Werte ermitteln, um die Zeit exakt zu berechnen:**
- [ ] Stromaufnahme des Kühlschranks im 12-V-Modus vom Typenschild ablesen (Angabe „12V ~X A")
- [ ] Kapazität (Ah) der Autobatterie des Zugfahrzeugs nachschlagen (Typenschild Batterie oder Fahrzeugpapiere/Handbuch)
- [ ] Mit obiger Formel die tatsächliche Zeit für dieses Gespann berechnen und hier eintragen

## Anhang: Alternative Festeinbau-Lösung (falls später gewünscht)

Falls doch ein fester Einbau statt der Powerstation gewünscht wird (z. B. für dauerhafte, größere Autarkie), hier die Einzelkomponenten-Variante als Referenz:

### Wechselrichter

| Modell | Leistung | Preis | Anmerkung |
|---|---|---|---|
| **Loadchamp Sinus-Wechselrichter 1500 W, 12 V** | 1.500 W, reiner Sinus | **~154,90 €** | Reicht für die Pixie mit Reserve — günstigste sinnvolle Wahl |
| CREABEST 2000 W (mit 80-A-Ladegerät integriert) | 2.000 W, reiner Sinus | ~349,99 € | Mehr Reserve + eingebautes Ladegerät |
| Reiner-Sinus-Wechselrichter 2000 W (diverse Anbieter) | 2.000 W, reiner Sinus | ~238,67 € | Günstigere Alternative mit mehr Reserve |

### LiFePO4-Batterie (50 Ah)

| Modell | Kapazität | Preis | Anmerkung |
|---|---|---|---|
| **Redodo 12V 50Ah Pro LiFePO4** | 640 Wh, 50-A-BMS | **~156 €** (reduziert von 289,99 €) | 5 Jahre Garantie, passt zum Bedarf |
| LiTime 12V 50Ah LiFePO4 | 640 Wh | Preis aktuell prüfen | 4.000–15.000 Zyklen, 10 Jahre Lebensdauer |

### DC-DC-Ladebooster

| Modell | Ladestrom | Preis | Anmerkung |
|---|---|---|---|
| **Renogy DCC-1212-40** | 40 A | **~137 €** | DIP-Schalter für Lithium-Ladeprofil, kein Zusatzmodul nötig |
| Renogy RBC40D1U (Bluetooth) | 40 A | ~175 € | Wie oben + App-Überwachung |
| Victron Orion-Tr Smart 12/12-30A | 30 A | ~185 € | App-basiert, etabliert in der Camper-Szene |

### Gesamtkosten Festeinbau

| Setup | Komponenten | Preis |
|---|---|---|
| Minimal (Batterie extern laden) | Wechselrichter + LiFePO4-Batterie | ~310 € |
| Mit Nachladung während der Fahrt | + DC-DC-Ladebooster | ~450 € |

Ursprüngliche Berechnungsgrundlage (Energiebedarf für eine portable Kompressor-Kühlbox statt des eingebauten Kühlschranks): 5 Kaffee (~140 Wh) + Kühlbox 24 h (~300 Wh) ≈ 440 Wh, mit Marge 500 Wh — deckt eine 50-Ah-LiFePO4-Batterie knapp mit Reserve ab. Diese Rechnung gilt nur für eine **portable Kühlbox**, nicht für den eingebauten Absorberkühlschrank (siehe Kapazitäts-Check oben).

## Quellen

- [230V + 12V einschalten bei Absorberkühlschrank — Motor-Talk](https://www.motor-talk.de/forum/230v-12v-einschalten-bei-absorberkuehlschrank-t6604797.html)
- [Wohnmobil-Kühlschrank: 12V, Gas oder 230V? — campofant.de](https://campofant.com/ratgeber/wohnmobil-kuehlschrank-12v-gas-oder-230v/)
- [13-polige Anhängersteckdose — Forum Campen.de](https://www.campen.de/threads/876258-13-polige-anhaengersteckdose)
- [AHK Pin 9 und 10 — Motor-Talk](https://www.motor-talk.de/forum/ahk-pin-9-und-10-t5367636.html)
- [Wechselrichter im Wohnmobil: 12V in 230V umwandeln — campofant.de](https://campofant.com/ratgeber/spannungswandler-wechselrichter/)
- [De'Longhi Nespresso Pixie EN 124.S 1260W — eBay](https://www.ebay.de/itm/388510989788)
- [Nespresso Pixie technische Daten — XL Elektro](https://xlelektro.de/kapselmaschinen/nespresso-pixie/)
- [Wie viel Strom verbraucht eine Espressomaschine pro Tasse? — espressomaschinen-berater.de](https://www.espressomaschinen-berater.de/ratgeber/wie-viel-strom-verbraucht-eine-espressomaschine-pro-tasse.html)
- [Kompressor-Kühlbox: Stromverbrauch & Batterie-Laufzeit — planmycamper.de](https://planmycamper.de/ratgeber/kompressor-kuehlbox-stromverbrauch/)
- [Ladebooster Wohnmobil: 30A oder 50A? Vergleich 2026 — planmycamper.de](https://planmycamper.de/ratgeber/bester-ladebooster-dc-dc-camper-test/)
- [DC-DC Wandler, Ladebooster — Renogy](https://de.renogy.com/produkte/batterieladegerat/12v-20-60a-dc-dc/)
- [LiTime 12V 50Ah LiFePO4 Batterie](https://www.litime.de/en/products/litime-12v-50ah-lithium-lifepo4-battery)
- [AGM Wohnmobilbatterien — Batterie24.de](https://batterie24.de/batterien/agm-batterien/agm-wohnmobilbatterien)
- [Loadchamp Sinus Wechselrichter 1500W 12V — winnerbatterien.de](https://www.winnerbatterien.de/Reiner-Sinus-Wechselrichter-1500W-12V-Spannungswandler_2)
- [Wechselrichter Wohnmobil Reiner Sinus — CREABEST](https://creabest.de/collections/wechselrichter-fur-wohnmobil-reiner-sinus)
- [Redodo 12V 50Ah Pro LiFePO4 Batterie (640Wh)](https://www.redodopower.de/en/products/redodo-12v-50ah-pro-lifepo4-battery)
- [Jackery Explorer 1000 v2 — Geizhals Preisvergleich](https://geizhals.de/jackery-powerstation-explorer-1000-v2-solargenerator-a3310706.html)
- [Jackery Explorer 1000 v2 — Fritz Berger Campingbedarf](https://www.fritz-berger.de/artikel/jackery-explorer-1000-v2-tragbare-powerstation-1070-wh-1500-w-505842)
- [EcoFlow Delta 2 — Geizhals Preisvergleich](https://geizhals.de/ecoflow-delta-2-power-station-solargenerator-a2825946.html)
- [Absorber Kühlschrank im 12V Betrieb — Reisemobiltreff](https://www.reisemobiltreff.de/viewtopic.php?t=4587)
- [Starterbatterie — Wikipedia](https://de.wikipedia.org/wiki/Starterbatterie)
- [Stromverbrauch Wohnmobil berechnen — camperpedia.de](https://camperpedia.de/ratgeber/elektrik/stromverbrauch-wohnmobil-berechnen/)
- [Wie viel verbraucht der Camping-Kühlschrank? — Faszination Camping](https://www.faszinationcamping.de/wie-viel-verbraucht-der-camping-kuhlschrank-wir-geben-antworten/)

## Zusammenhang

Betrifft [[Wohnwagen-Bürstner-4313]] (Fahrzeugdaten, Bordnetz).
