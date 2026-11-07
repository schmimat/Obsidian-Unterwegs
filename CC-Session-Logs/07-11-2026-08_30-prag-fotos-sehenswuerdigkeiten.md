# Session Log: 07-11-2026 08:30 - Prag Fotos & Sehenswürdigkeiten

## Quick Reference (for AI scanning)
**Confidence keywords:** Prag 2026, Pilsen, digiKam, Tagesordner, EXIF, Zeitkorrektur, Lumix DC-TZ202, Uhrenfoto, Aufnahmedatum, Fotoabgleich, GPS, Reisetagebuch, Central Gallery, Kafka-Museum, Spanische Synagoge, Stiertreppe, Klausen-Synagoge, Sehenswürdigkeiten, Hotel Atlantic, fakten-pruefer, Word-Reiseverlauf, Bretagne-Vergleich, Smartphone, preserve
**Projects:** Unterwegs (Reisen/Prag 2026, Sehenswürdigkeiten/Prag + Pilsen, Übernachtungen), digiKam `10.30-11.03_Prag-Pilsen`
**Outcome:** Prag 2026 vollständig aus Chat + allen Fotos, Kamerazeit korrigiert, Fotos in Tagesordnern, 9 Sehenswürdigkeiten-/Hotel-Notizen extrahiert und faktengeprüft, Word-Reiseverlauf im Fotoordner.

## Key Learnings & Solutions
- Lumix DC-TZ202 lief nach der Zeitumstellung (25.10.) +1:00:32 vor. Gemessen per Foto der Handy-Uhr, bestätigt über gleiche Motive (Kafka-Kopf). Kein GPS an der Kamera.
- EXIF-Korrektur ohne exiftool/piexif: die drei Datumsstrings (`DateTime`, `DateTimeOriginal`, `DateTimeDigitized`) byte-genau im APP1-Segment ersetzen. Bilddaten per MD5 unverändert, mtime mitziehen. Die Panasonic-MakerNote hatte schon die richtige Zeit, das XMP enthielt kein Datum.
- Pixel `PXL_…`: Dateiname in UTC, EXIF in Ortszeit. Das Explorer-„Erstelldatum“ ist der Kopierzeitpunkt aufs NAS, sortiert wird nach der Spalte „Aufnahmedatum“ (vom User umgesetzt).
- Kontaktbögen (PIL, `im.draft`) je Zeitfenster + Halbstunden-GPS-Mittel reichen für die Tagesrekonstruktion. Ticket-, Schild- und Tafelfotos liefern Titel (Antologia, Hallelujah – Czech Collegium Ensemble, Fiedler-Ausstellung).
- Die Bilderkennung von Subagent und Claude war mittelmäßig: Stiertreppe übersehen („keine Fotos“), Kostüm-Polizei als echt gelesen, Klausen-Synagoge nur „vermutlich“. Nachbarfotos + GPS hätten es geklärt.
- fakten-pruefer, 38 Chat-Aussagen: 25 ✅, 9 ⚠️, 0 ❌, 4 ❓. Wichtigste Korrekturen: „Ochsentreppe“ → Stiertreppe (Býčí schodiště), Pinkas-Bezug zur Wende nur indirekt, Pilsener Rathaus-Sgraffito von 1907–12, Regenschirm-Figur von Michal Trpák.
- Bash-Heredocs mit vielen „“ und Umlauten scheiterten („unexpected EOF“). Lösung: Python-Skripte per Write-Tool in den Scratchpad schreiben.

## Decisions Made
- EXIF der 205 Kamera-JPGs dauerhaft korrigiert, ohne Sicherung (User). Die Videos bleiben unkorrigiert.
- Tagesordner nach Bretagne-Muster: `10.30_Anreise_Altstadt`, `10.31_Strahov_Prager_Burg`, `11.01_Josefstadt_Loreto_Petrin`, `11.02_Neustadt_Spanische_Synagoge`, `11.03_Pilsen_Heimfahrt`, mit MD5-Inventaren vorher und nachher (799 Dateien, 0 Abweichungen).
- Word-Bericht ausführlich (alle Tage) im Stil der Bretagne-Vorlage. Gespeichert im digiKam-Ordner.
- Bretagne bleibt wie sie ist. Prag bekommt das Leitprinzip: Sehenswürdigkeiten und Hotel als eigenständige Notizen, verlinkt aus dem Tagebuch.
- Unterwegs wenig tippen. Das Tagebuch entsteht danach aus Fotos und Rückfragen (User: Chat-Eingabe lenkt ab). Als Memory gespeichert.

## Files Modified & Config
- `Reisen/Prag 2026/Prag 2026.md` und `Tagebuch/2026-10-30` bis `2026-11-03`: Platzhalter gefüllt, Fotoabgleich, Mucha/Warhol, Starbucks, Halloween, Klausen, Stiertreppe, Links, Faktenkorrekturen.
- Neu: `Übernachtungen/Hotel Atlantic (Prag).md`. `Sehenswürdigkeiten/Prag/` mit Kloster Strahov, Prager Burg, Jüdisches Museum Prag, Loreto (Prag), Petřín-Aussichtsturm, Central Gallery (Prag), Kafka-Museum. `Sehenswürdigkeiten/Pilsen/Große Synagoge Pilsen.md`.
- digiKam `\\10.12.40.242\storage\Bilder\digiKam\Jahre\2026\10.30-11.03_Prag-Pilsen\`: 5 Tagesordner, `Vorher_Inventar_Fotos.csv`, `Nachher_Inventar_Tagesordner.csv`, `Fotoverschiebung-Tagesordner_Dokumentation.md`, `Prag 2026 - Reiseverlauf.docx`.
- `CLAUDE.md` (/preserve, 11,8 KB), `CLAUDE-Archive.md` (Block 2026-11-07), `Doku/Claude – Änderungshistorie.md` (7 🟡-Zeilen).
- Memory `~/.claude/projects/C--Users-matth-Obsidian-Vaults-Unterwegs/memory/reise-doku-wenig-smartphone.md`.
- Scratchpad-Skripte (flüchtig): `exif.py`, `fix.py` (EXIF-Patch), `move.py`, `sheet2.py`, `pick.py`, `build.py` (Word-Generator).

## Pending Tasks & Errors
- 3 Kamera-Videos `P1034031/032/142.MP4` haben noch die Zeit +1 h.
- Uhrenfoto `P1034162.JPG` löscht der User. Danach die Zeile in `Fotoverschiebung-Tagesordner_Dokumentation.md` anpassen.
- Hotel-Eckdaten offen (Hausnummer Na Poříčí, Preis, Parken).
- `Auswahl/`-Ordner für Prag (und Rügen) fehlt. Das `Regionen/`-Konzept ist offen, mit Prag/Pilsen als Fall.
- Der Word-Generator `build.py` lag nur im Scratchpad. Bei neuen Änderungen über `office-export` neu bauen (Vorlage `Sommerurlaub 2026 - Reiseverlauf.docx`).
- Doppelte 02.11.-Zeilen in der Änderungshistorie (aus der Vorsession) bleiben fürs Wochen-Review.
- Im Chatverlauf-Export steht weiter „Ochsentreppe“ (Originalexport, bewusst unverändert).

## Key Exchanges
- „Mach den Bericht zum Prag urlaub zum Ordner“ → „schau zuerst das neueste Foto an und mach einen Zeitabgleich“ → Uhrenfoto entdeckt, +1:00:32.
- User-Korrekturen: Mucha- und Warhol-Etage, Ochsentreppe-Foto `PXL_20261031_153305901`, Starbucks, Halloween-Kostüme, „Wieso konntest du die Klausensynagoge nicht erkennen?“.
- Vergleich Bretagne/Prag: Prag ist das bessere Tagebuch, Bretagne die bessere Wissensstruktur. Der User wählte Prag nachziehen und Bretagne lassen.

## Custom Notes
None

---

## Quick Resume Context
Prag 2026 ist fertig: Tagebuch aus Chat und allen Fotos, Sehenswürdigkeiten und Hotel als eigene Notizen mit Quellen, Word im digiKam-Ordner. Offen sind nur Kleinigkeiten (Videozeit, Uhrenfoto, Hotel-Eckdaten, Auswahl-Ordner). Arbeitsmuster für künftige Reisen stehen in `Unterwegs/CLAUDE.md` unter „Reisen“: Kamera-Uhr prüfen, Bilderkennung gegenprüfen, wenig tippen unterwegs.

---

## Raw Session Log

**User:** /resume
**Claude:** Lädt CLAUDE.md-Kontext und die letzten 3 Logs (Prag-Reisetagebuch 02.11., Wartung 23.10., Wohnwagen-Toilettenlicht 21.09.). Bericht mit offenen Punkten.

**User:** "\\10.12.40.242\storage\Bilder\digiKam\Jahre\2026\10.30-11.03_Prag-Pilsen" Mach den Bericht zum Prag urlaub zum Ordner.
**Claude:** Ordner flach mit ~800 Dateien (207 P103 Lumix, 592 PXL Pixel). EXIF-Zeit und GPS ausgelesen, Halbstunden-Zeitleiste gebaut, u. a. Pilsen am 03.11. von 11:40 bis 14:32.

**User:** schau zuerst das neueste Foto an und mach einen Zeitabgleich
**Claude:** `P1034162.JPG` (06.11.) zeigt die Handy-Uhr 19:15:12, die Kamera speicherte 20:15:44 → +1:00:32. Kein GPS an der Kamera. Gegenprobe über Kafka-Kopf und Straße an der Josefstadt bestätigt −1 h während der Reise. Gefragt: EXIF dauerhaft korrigieren?

**User:** Korrigier die EXIF-Zeiten der 207 Kamerafotos dauerhaft. keine Sicherung notwendig.
**Claude:** Byte-Patch der drei EXIF-Datumsfelder, Test an einer Kopie, dann 205 JPGs ohne Fehler korrigiert. MD5 der Bilddaten gleich, mtime verschoben. Videos nicht geändert. Hinweis: digiKam-Metadaten neu einlesen, Kamera-Uhr umstellen.

**User:** Mach zuerst die Ordner mit den Beschreibungen des Tages und verschiebe die Fotos zum Tag
**Claude:** Bretagne-Muster übernommen. 5 Tagesordner, 799 Dateien verschoben, Vorher-/Nachher-Inventar mit MD5 (0 Abweichungen), Dokumentation geschrieben. Uhrenfoto bleibt im Hauptordner.

**User:** Ja leg los
**Claude:** Kontaktbögen für 30.10., 02.11. nachmittags und 03.11. angesehen. Tagebuch ergänzt: Abendspaziergang 30.10.; 02.11. mit Kafka-Museum, Spanischer Synagoge mit Konzert und Kafka-Kopf bei Nacht; 03.11. Pilsen (Rathaus, Bartholomäus, Große Synagoge, Tyl-Theater). Übersicht und Historie aktualisiert.

**User:** Mach dein Word Dokument und speichere es.
**Claude:** Agent office-export erzeugte `Prag 2026 - Reiseverlauf.docx` im digiKam-Ordner (Querformat wie die Bretagne-Vorlage, 2 Tabellen, Tagesabschnitte). Selbst geprüft.

**User:** Das foto mit der Uhr lösch ich
**Claude:** Ok. Nach dem Löschen wird die Doku-Zeile angepasst.

**User:** Warum ist die Sortierung im Explorer nach erstellungsdatum nicht richtig, sondern nur nach änderungsdatum?
**Claude:** Das Erstelldatum ist der Kopierzeitpunkt aufs NAS (06.11. 19:26–19:44). Das Änderungsdatum entspricht der Aufnahmezeit. Empfehlung: Spalte „Aufnahmedatum“.

**User:** Ich hab Möglichkeit 1 schon umgesetzt
**Claude:** Passt. Nur die Videos haben keinen sinnvollen Wert.

**User:** Wir waren auch im Mukta Geschoss und im Warhol geschoss, nicht nur im Dali geschoss
**Claude:** Fotos 12:13–13:26 angesehen: Mucha (Kameliendame, Documents décoratifs), Warhol (Marilyn, Sticky Fingers, Bad/Trash). Tagebuch, Übersicht und Word angepasst, Build-Skript um Unterpunkte erweitert.

**User:** Schau die Bilder nochmal durch wo wir überal waren.
**Claude:** Subagent (Opus) glich alle Fotos ab. Selbst an Stichproben gegengeprüft. Ergänzt: Rudolfinum und Palladium am 30.10., Café und Veitsdom innen am 31.10., Národní třída, Kafka-Denkmal, Kampa-Glühwein, Karlsbrücke bei Nacht, Kepler-Haus, Pinkelnde Männer, Moldaukai, Tickettitel. Korrigiert: Reihenfolge der Burgführung, Petřín-Zeit, Abendroute am 02.11. Offene Fragen an den User gestellt.

**User:** es bibt schon ein Foto.
**Claude:** Fotos von 16:33–16:37 zeigen die Plečnik-Treppe (Ochsentreppe) mit Baldachin in die Südgärten. Tagebuch korrigiert.

**User:** PXL_20261031_153305901.MP
**Claude:** Bestätigt: Blick vom Absatz unter dem Baldachin auf die Südgärten. Einbinden angeboten.

**User:** Cafe war das Starbucks
**Claude:** Starbucks am Kafka-Kopf am 02.11. eingetragen.

**User:** Menschenmenge, keine Ahnung → „Anlass unbekannt“. **User:** War keine Polizei in der Menschenmenge, war haloween und irgendeine veranstatltung → korrigiert. **User:** Polizei ist schon ok aber war ein Kostüm, so wie auch das Skelett und einen Lautsprecher. → „Halloween-Veranstaltung, Leute im Polizei- und Skelettkostüm, Lautsprecher“.

**User:** Wiese konnst du die Klausensynagoge nicht erkennen?
**Claude:** Fotos 12:30–12:34 + GPS sind eindeutig Klausen (barockes Gewölbe, Toraschrein, Empore, Eingang am Friedhof). Zugegeben, dass Nachbarfotos und GPS vorher nicht geprüft wurden. Korrigiert.

**User:** /preserve → Dialog abgebrochen. **User:** Vergleiche die Reise und dokumentation der Bretanienreise und der Prag reise. Wie sit deine Einschötzung
**Claude:** Vergleichstabelle. Prag: besseres Tagebuch, Reisestil-Abschnitt, aber 0 Links (Leitprinzip verletzt), keine Auswahl. Bretagne: verlinkt, Auswahl-Ordner, aber knapp, ohne Rückblick. Word-Formate uneinheitlich. Empfehlung: gemeinsames Muster.

**User:** Mach Prag mit Hotel und Sehenswürdigkeiten Bretagne lassen wir so wie es ist. Der Tagebuchstil ist in Prag einfacher … durch die Eingabe schau ich mehr auf das Smartphone --> blöd
**Claude:** Hotel Atlantic und 8 Sehenswürdigkeiten angelegt (Inhalt nur aus Tagebuch/Fotos, GPS als `location`). Links bei Erstnennung, Übersichtsabschnitt, Word ergänzt. Vorschlag zum Smartphone: unterwegs nur fotografieren, Rekonstruktion danach. Als Memory gespeichert.

**User:** Bei früheren Reisen habe ich … den Wikieintrag durchgelesen. In Prag habe ich dich gefragt. Ich hoffe die Infos sind einigermaßen richtig gewesen.
**Claude:** Grundfakten sicher, Einzelheiten riskanter. Faktenprüfung angeboten.

**User:** Ja, lass die Fakten prüfen
**Claude:** fakten-pruefer: 38 Aussagen, 25 ✅, 9 ⚠️, 0 ❌, 4 ❓. Rot am Regenschirm per Foto bestätigt. Korrekturen und Quellenlisten eingearbeitet (Stiertreppe, Pinkas, Fiedler-Titel, Pilsener Rathaus, Masaryčka, Generali, Trpák, Beneš). Nicht Belegbares markiert. Word neu erzeugt.

**User:** /preserve
**Claude:** Alle 4 Kategorien in `Unterwegs/CLAUDE.md` übernommen (11,8 KB). Erledigter Schritt archiviert, Prag-Reste als neuer Schritt 4.

**User:** /compress
**Claude:** Dieses Log.
