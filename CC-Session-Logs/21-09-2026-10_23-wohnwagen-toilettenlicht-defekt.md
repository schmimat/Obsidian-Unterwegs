# Session Log: 21-09-2026 10:23 - Wohnwagen Toilettenlicht defekt

## Quick Reference (for AI scanning)
**Confidence keywords:** Wohnwagen, Bürstner Club 4313, Toilette, Leuchtstoffröhre, Flackern, 12V, Starter, Transistorleuchte, Vorschaltgerät, Umformer, LED-Röhre, Dometic 12V LED-Tube, HABA, Ersatzteil, Spannungsabfall, Multimeter, Defektdiagnose, _Wohnwagen-Technik, Änderungshistorie, preserve, compress
**Projects:** Unterwegs-Vault, `_Wohnwagen-Technik/` (Bürstner Club 4313, Baujahr 1995)
**Outcome:** Defekt eingegrenzt (Leuchte + Klemmen als Ursache ausgeschlossen, Verdacht auf Spannungsversorgung), Starter-/Ersatzteil-Recherche durchgeführt und vollständig in der Fahrzeugnotiz + CLAUDE.md dokumentiert; physische Prüfschritte (Multimeter, Fassung öffnen) stehen beim User aus.

## Key Learnings & Solutions

- **Diagnose-Reihenfolge bei 12-V-Defekten im Wohnwagen:** erst Verbraucher (Leuchte/Leuchtmittel), dann Kontakte/Klemmen, dann Versorgung (Spannungsabfall/Batterie). Sind die ersten beiden erfolglos getauscht bzw. gereinigt, ist weiteres Suchen per Sichtprüfung sinnlos — ab da braucht es eine **Messung unter Last**: Spannungsvergleich an drei Punkten (Batterie → Sicherungskasten → Verbraucher), der größte Spannungssprung markiert die Fehlerstelle.
- **Fehlerbild unterscheidet die Ursachenklasse:** „geht gar nicht an" deutet auf Sicherung/Unterbrechung, „flackert und leuchtet schwach" auf Starter, verbrauchte Röhre, alternde Vorschaltelektronik oder Unterspannung. Das Fehlerbild sollte deshalb vor jedem Bauteiltausch erfragt werden.
- **12-V-Leuchtstoffleuchten dieser Bauzeit sind meist „Transistorleuchten"** — elektronische Vorschaltung fest im Leuchtengehäuse, **kein separater Starter** vorhanden oder nötig (Beleg: HABA-Ersatzröhre für Transistorleuchte, Sockel 8TL, explizit „benötigt keinen separaten Starter").
- **Alternative Altbauform:** manche älteren 12-V-Leuchten enthalten einen **12-V→230-V-Umformer**, der eine normale 230-V-Röhre betreibt (Beleg: Wohnwagen-Forum-Thread). Falls das zutrifft, ist der alternde Umformer selbst eine plausible Flacker-Ursache — durch Röhrentausch **nicht** behebbar, nur durch Tausch der kompletten Leuchte oder Umbau.
- **Unterscheidung nur durch Öffnen der Fassung:** rundes, drehbares Steckteil (ca. 15–20 mm Ø, meist silbern, oft Bajonettverschluss) = klassischer Starter; stattdessen sichtbare Platine/Elektronik-Baugruppe im Gehäuse = Transistorleuchte. Zusätzlich lohnt die Sichtkontrolle der Röhrenenden — Schwarz-/Grauverfärbung = verbrauchte Röhre unabhängig vom Starter-Befund.
- **Echte 12-V-DC-LED-Röhren brauchen weder Starter noch Vorschaltgerät** (direkte DC-Speisung, Elektronik in der Röhre). Sie **umgehen** alternde Leuchten-Elektronik, statt sie nur zu ersetzen — deshalb die robustere Langfristlösung, wenn die Vorschaltung/der Umformer verdächtig ist.
- **Vor jeder Bestellung Röhre ausbauen und Länge + Sockeltyp messen** — die Produktdaten passen nur bei exakter Übereinstimmung (HABA 295 mm/Sockel 8TL vs. Dometic 474 mm sind nicht austauschbar).
- **Sicherheitsschritt vor dem Öffnen:** Batterie-Hauptschalter bzw. Sicherung des Stromkreises abschalten — der Wandschalter der Leuchte allein ist keine ausreichende Absicherung gegen Kurzschluss beim Hantieren.

### Recherchierte Bezugsquellen

| Produkt | Daten | Preis | Quelle |
|---|---|---|---|
| HABA Röhre für Transistorleuchte 8W 12V | 295 mm, Sockel 8TL, 126 lm warmweiß, 10.000 h | 5,00 € | campinglanghans.de (passt zu Transistorleuchte Alpha 83116/83117, Einbautransistorleuchte 83010) |
| Dometic 12V LED-Tube | 47,4 × 2,5 × 2,1 cm, direkt 12-V-DC, kein Vorschaltgerät | ~33 € | obelink.de |
| Generische 12V-T8-LED-Röhren | diverse Längen | variabel | eBay, Reimo, benweilight |
| LED-Streifen als Alternative | zuschneidbar, diverse Farbtemperaturen | günstig | Empfehlung aus wohnwagen-forum.de |

## Decisions Made

- **Defekt-Dokumentation gehört als Abschnitt in die Fachnotiz des betroffenen Objekts** (`_Wohnwagen-Technik/Wohnwagen-Bürstner-4313.md`), **nicht** nach `Aufgaben/` — letzteres ist für abarbeitbare Claude-Code-Worker-Aufträge reserviert, nicht für körperliche Reparaturen des Users.
- **Struktur des Defekt-Abschnitts festgelegt:** Symptom → bereits erfolglos Geprüftes → verbleibender Verdacht → Recherche-Ergebnis/Bezugsquellen → „Offen"-Zeile mit dem nächsten konkreten Test. Damit ist bei Wiederaufnahme sofort klar, was schon ausgeschlossen ist.
- **Bezugsweg generischer 12-V-Camping-Teilemarkt statt Bürstner-Originalersatzteil** — Originalteile für ein 1995er Modell laufen laut Recherche nur noch über autorisierte Fachhändler, für ein Kleinteil dieser Größenordnung unverhältnismäßig in Aufwand und Preis.
- **Beide Optionen offengehalten (Ersatzröhre ~5 € vs. LED-Umrüstung ~33 €)** statt vorschneller Empfehlung — die Entscheidung hängt am Befund beim Öffnen der Fassung (Starter/Platine/Umformer) und ist ohne diesen nicht sinnvoll zu treffen.
- **Vier Rückfragen zum Dokumentieren gestellt, erst auf „ja" geschrieben** — der Defekt war zunächst nur als Gesprächsinhalt gemeldet, ohne erkennbaren Doku-Auftrag; bei rein mündlich gemeldeten Realweltproblemen wird nicht automatisch eine Notiz angelegt.
- **Datums-Konsistenz bei `/preserve` über Sessiongrenze:** Arbeit fand am 2026-09-20 statt, CLAUDE.md-Update am 2026-09-21 — Frontmatter `modified` und Footer „Zuletzt aktualisiert" beide auf das **Änderungsdatum** (21.), das Session-/Sachdatum (20.) bleibt im Fließtext und in der Abschnittsüberschrift. Vermeidet genau die Datums-Diskrepanzen, die in Vault-Wartung Runde 9 aufgeräumt werden mussten.

## Files Modified & Config

- `_Wohnwagen-Technik/Wohnwagen-Bürstner-4313.md`: neuer Abschnitt „Defekt: Beleuchtung Toilette flackert (offen, Stand 2026-09-20)" nach dem Stromversorgungs-Abschnitt — Symptom, erfolglos Geprüftes (Leuchte getauscht, Klemmen gereinigt), Hauptverdacht Spannungsversorgung mit Multimeter-Testanleitung, Starter-Recherche (Transistorleuchte/Umformer-Unterscheidung), Ersatzteil-/LED-Tabelle mit 3 Bezugsquellen, „Offen"-Zeile. Frontmatter `modified` 2026-08-02 → 2026-09-20.
- `CLAUDE.md`: neuer Abschnitt „`_Wohnwagen-Technik/` — Defektdiagnose am Bürstner 4313 (Muster, Stand 2026-09-20)" vor „Wichtige Dateien & Ordner" (Muster für Defekt-Dokumentation, 4 Erkenntnis-Bullets, Offen-Zeile); neue Tabellenzeile `_Wohnwagen-Technik/` bei „Wichtige Dateien & Ordner"; Footer „Zuletzt aktualisiert" auf 2026-09-21 rotiert (vorheriger Eintrag 2026-09-12 nachgerückt); Status-Zeile um den offenen Defekt ergänzt; Frontmatter `modified` 2026-08-19 → 2026-09-21. **231 → 248 Zeilen** (Richtwert <280 eingehalten, kein Archivieren nötig).
- `Doku/Claude – Änderungshistorie.md`: zwei neue Zeilen oben in Abschnitt 6 (2026-09-20 Fahrzeugnotiz, 2026-09-21 CLAUDE.md-`/preserve`), beide 🟡 offen.
- `CC-Session-Logs/21-09-2026-10_23-wohnwagen-toilettenlicht-defekt.md`: diese Datei.

## Pending Tasks & Errors

- **Offen (User, physisch):** Multimeter-Spannungsvergleich unter Last an drei Punkten (Batterie / Sicherungskasten / Leuchte) — der aussagekräftigste noch ausstehende Test.
- **Offen (User, physisch):** Fassung öffnen (vorher Batterie-Hauptschalter/Sicherung aus), prüfen ob Starter (rundes Steckteil) oder Platine (Transistorleuchte) verbaut ist, dabei Röhrenenden auf Schwärzung kontrollieren.
- **Danach erst entscheidbar:** Ersatzröhre (HABA ~5 €, nur bei passender Länge/Sockel) vs. LED-Umrüstung (Dometic ~33 €) vs. kompletter Leuchtentausch (falls 12→230-V-Umformer die Ursache ist).
- **Indiz-Test ohne Multimeter** (falls keines verfügbar): andere 12-V-Verbraucher (Wasserpumpe, weitere Lampen) gleichzeitig beobachten — werden die auch schwächer, spricht das für Batterie/Hauptleitung statt für die Zuleitung zur Toilette.
- **Fehlgeschlagener Abruf (kein Blocker):** `campen.de`-Forenthread „12 V Leuchtstofflampe def." lieferte HTTP 403 (Bot-Schutz) — die Frage wurde über die anderen drei Quellen (wohnwagen-forum.de, campinglanghans.de, obelink.de) vollständig beantwortet.
- **Keine Erkenntnis zum konkret verbauten Leuchtentyp** — für den Bürstner Club 4313 (1995) ist kein Leuchtenmodell dokumentiert; Bürstner-Ersatzteile laufen nur über autorisierte Händler. Der Typ lässt sich nur durch Öffnen der Fassung bestimmen.

## Key Exchanges

- Einstieg mit „licht im wohnwagen toilette kapput" — bewusst erst Fehlerbild geklärt statt sofort Lösungen zu nennen; die Präzisierung „die leuchtstoffröhre flackert und leutet nicht gut" verschob den Verdacht weg von Sicherung hin zu Starter/Röhre/Vorschaltung.
- Zwei knappe Statusmeldungen des Users („leuchte wurde schon getauscht", „klemmen wurden saubergemacht") schlossen nacheinander Verbraucher und Kontakte aus und führten zur Empfehlung, ohne Multimeter nicht weiterzusuchen.
- Auf „gibt es für die leuchtstoffröhre in der Toilette einen starter? mach eine internet recherche über die ersatzteile, oder alternatiefe led" drei parallele Websuchen plus vier Seitenabrufe — Kernbefund Transistorleuchte (kein Starter) plus der Nebenbefund 12→230-V-Umformer als eigenständige mögliche Flacker-Ursache.
- Nach dreimaligem Angebot bestätigte der User mit „ja" das Dokumentieren; danach Dokumentation + Protokollzeile, anschließend `/preserve` (alle 4 Kategorien) und `/compress`.

## Custom Notes
None

---

## Quick Resume Context

Im Unterwegs-Vault wurde der erste Defekt-Fall im Ordner `_Wohnwagen-Technik/` dokumentiert: die Leuchtstoffröhre in der Toilette des Bürstner Club 4313 (Bj. 1995) flackert und leuchtet schwach. Leuchte und Klemmen sind als Ursache bereits ausgeschlossen (getauscht bzw. gereinigt), der verbleibende Verdacht liegt auf der Spannungsversorgung (Spannungsabfall über die alte Zuleitung oder einbrechende Bordbatterie); die Recherche ergab, dass solche 12-V-Leuchten meist „Transistorleuchten" ohne separaten Starter sind, manche Altbauformen aber einen 12→230-V-Umformer enthalten. Nächste Schritte liegen beim User: Multimeter-Spannungsvergleich unter Last und Öffnen der Fassung zur Starter-/Platinen-Prüfung — danach erst ist die Entscheidung zwischen HABA-Ersatzröhre (~5 €) und Dometic-12-V-LED-Röhre (~33 €) sinnvoll zu treffen. Voller Stand in `_Wohnwagen-Technik/Wohnwagen-Bürstner-4313.md`, Muster + Erkenntnisse in `CLAUDE.md`.

---

## Raw Session Log

**User:** licht im Wohnwagen toilette kapput

**Assistant:** Prüfte den Ordner `_Wohnwagen-Technik/` (2 Notizen: `Wohnwagen-Bürstner-4313.md`, `Wohnwagen-Stromversorgung.md`, Unterordner `Sackmarkise/`) und las beide vollständig. Ergebnis: kein bestehender Eintrag zur Toilettenbeleuchtung. Antwortete mit fünf Prüfschritten für einen 12-V-Defekt: (1) andere 12-V-Verbraucher testen zur Abgrenzung lokal vs. Bordnetz, (2) Sicherung am Bedienpanel prüfen (Schaudt/Sargent/Nordelettronica), (3) eigenen Kippschalter der Leuchte prüfen, (4) Leuchtmittel/LED-Modul, (5) Wackelkontakt/Korrosion an den Steckkontakten bei einem Fahrzeug von 1995. Fragte, ob der Stand in `_Wohnwagen-Technik/` festgehalten werden soll oder ob es zunächst nur eine Notiz für den User war.

**User:** die leuchtstoffröhre flackert und leutet nicht gut

**Assistant:** Ordnete das Fehlerbild ein (Flackern + schwaches Leuchten ≠ tote Sicherung) und nannte drei Kandidaten: (1) klassischer Starter, falls ein kleines zylindrisches Bauteil verbaut ist — häufigster und günstigster Fall, (2) Röhre am Lebensende, erkennbar an schwarzen Röhrenenden, bei einem 1995er Fahrzeug plausibel, (3) Vorschaltgerät/Wandler bei Leuchten ohne Starter — nicht reparierbar, nur Leuchtentausch. Praktischer erster Schritt: Röhrenenden auf Schwärzung prüfen und feststellen, ob ein Starter verbaut ist. Nebenfaktor: schwache Batteriespannung lässt Leuchtstoffröhren ebenfalls flackern. Erneutes Angebot zur Dokumentation.

**User:** leuchte wurde schon getauscht

**Assistant:** Schloss daraus die Leuchte selbst als Ursache aus und verlagerte den Verdacht auf die Spannungsversorgung. Vier nächste Schritte: (1) Spannung direkt an der Anschlussklemme unter Last messen (Sollwert nahe 12–13 V, unter ~10,5 V erklärt das Fehlerbild), (2) Steckverbindungen/Klemmen auf Oxidation und Übergangswiderstand prüfen, (3) Vergleich Landstrom- vs. Batteriebetrieb zur Abgrenzung Batterie vs. Leitung, (4) prüfen, ob es die am weitesten entfernte Leuchte ist (Spannungsabfall summiert sich bei alter dünner Verkabelung). Angebot, den Stand in der Fahrzeugnotiz festzuhalten.

**User:** klemmen wurden saubergemacht

**Assistant:** Benannte als verbleibenden Hauptverdacht den Spannungsabfall über die Leitungslänge oder eine unter Last einbrechende Bordbatterie und wies darauf hin, dass ohne Multimeter keine weitere Eingrenzung durch Sichtprüfung möglich ist. Beschrieb den Spannungsvergleich unter Last an drei Punkten (Batterie → Sicherungskasten → Leuchte), wobei der größte Spannungssprung die Fehlerstelle markiert. Als Alternative ohne Messgerät: andere 12-V-Verbraucher gleichzeitig beobachten. Erneutes Dokumentationsangebot.

**User:** gibt es für die leuchtstoffröhre in der Toilette einen starter? mach eine internet recherche über die ersatzteile, oder alternatiefe led

**Assistant:** Lud `WebSearch`/`WebFetch` per ToolSearch nach und führte drei parallele Suchen aus („12V Leuchtstoffröhre Wohnwagen Starter Ersatzteil", „Bürstner Club 4313 Toilette Lampe Leuchte Ersatzteil", „12V LED Röhre Ersatz Leuchtstoffröhre Wohnwagen Camping"), danach vier parallele Seitenabrufe (wohnwagen-forum.de, campen.de → HTTP 403, obelink.de, campinglanghans.de).

Kernbefunde: Die meisten 12-V-Leuchtstoffleuchten dieser Bauzeit sind „Transistorleuchten" mit eingebauter elektronischer Vorschaltung und benötigen **keinen separaten Starter** (belegt über die HABA-Ersatzröhre, Sockel 8TL, 295 mm, 8W, 126 lm, 5,00 €, passend zu Transistorleuchte Alpha 83116/83117 und Einbautransistorleuchte 83010). Unterscheidung nur durch Öffnen: kein rundes Steckteil sichtbar = Transistorleuchte, drehbarer Zylinder = klassischer Starter. Nebenbefund aus dem Wohnwagen-Forum: manche älteren 12-V-Leuchten arbeiten mit einem eingebauten 12-V→230-V-Umformer für eine normale 230-V-Röhre — dann wäre der alternde Umformer selbst eine plausible Flacker-Ursache, durch Röhrentausch nicht behebbar. LED-Alternativen: Dometic 12V LED-Tube (47,4 × 2,5 × 2,1 cm, ~33 €, direkt 12-V-DC ohne Vorschaltgerät), generische 12V-T8-LED-Röhren (eBay/Reimo/benweilight), LED-Streifen als Umbauvariante. Bürstner-Originalteile für ein 1995er Modell nur über autorisierte Fachhändler — der generische Camping-Teilemarkt ist der praktikablere Weg. Hinweis, vor Bestellung Länge und Sockeltyp zu messen. Antwort mit Quellenliste, erneutes Dokumentationsangebot.

**User:** ja

**Assistant:** Las `Doku/Claude – Änderungshistorie.md` (Struktur und Tabellenformat in Abschnitt 6) und nahm drei Edits vor: (1) neuer Abschnitt „Defekt: Beleuchtung Toilette flackert (offen, Stand 2026-09-20)" in `_Wohnwagen-Technik/Wohnwagen-Bürstner-4313.md` nach dem Stromversorgungs-Abschnitt — Symptom, bereits erfolglos Geprüftes, verbleibender Hauptverdacht mit Multimeter-Testanleitung, Starter-Recherche inklusive Umformer-Sonderfall, Ersatzteil-/LED-Tabelle mit drei Bezugsquellen, Offen-Zeile; (2) Frontmatter `modified` dort auf 2026-09-20; (3) neue Protokollzeile in der Änderungshistorie (Status 🟡 offen).

**User:** Fassung öffnen und nach Starter schauen

**Assistant:** Gab Sicherheitshinweis (Batterie-Hauptschalter/Sicherung abschalten, Wandschalter allein genügt nicht) und beschrieb, worauf beim Öffnen zu achten ist: Abdeckung meist abclipsbar oder mit zwei Schrauben, Röhre seitlich aus den Federkontakten drehen; Starter = zylindrisches Teil ca. 15–20 mm Ø, meist silbern, oft Bajonettverschluss; kein Starter = Platine/Elektronik-Baugruppe fest im Gehäuse (Transistorleuchte); zusätzlich Röhrenenden auf Schwärzung prüfen. Bat um Rückmeldung des Befunds, um gezielt zwischen Starter-Tausch und Ersatzröhre/LED zu entscheiden.

**User:** `/preserve`

**Assistant:** Fragte per AskUserQuestion nach dem Umfang — der User wählte alle vier Kategorien (Status & Entscheidungen, Dateien & Struktur, Muster & Erkenntnisse, Blocker & nächste Schritte). Prüfte die Zeilenzahl (231, kein `CLAUDE-Archive.md` vorhanden) und die Abschnittsstruktur, fügte vor „Wichtige Dateien & Ordner" den neuen Abschnitt „`_Wohnwagen-Technik/` — Defektdiagnose am Bürstner 4313 (Muster, Stand 2026-09-20)" ein (Muster für Defekt-Dokumentation mit Abgrenzung zu `Aufgaben/`, vier Erkenntnis-Bullets, Offen-Zeile), ergänzte die Tabellenzeile `_Wohnwagen-Technik/`, rotierte den Footer auf 2026-09-21, erweiterte die Status-Zeile um den offenen Defekt und bumpte das Frontmatter `modified` auf 2026-09-21. Ergebnis 248 Zeilen (Richtwert <280, kein Archivieren nötig). Trug die CLAUDE.md-Änderung zusätzlich als eigene Zeile in die Änderungshistorie ein.

**User:** `/compress`

**Assistant:** Fragte Umfang (alle vier Kategorien gewählt), eigene Notiz (Skip) und Themenname (`wohnwagen-toilettenlicht-defekt`, akzeptiert) ab und schrieb dieses Session-Log nach `CC-Session-Logs/21-09-2026-10_23-wohnwagen-toilettenlicht-defekt.md`.
