---
tags:
  - template
  - recherche
created: 2026-06-14
modified: 2026-06-14
template_version: "1.0"
---

# Recherche: {{Thema}}

> [!info] Dokumente & Versionen dieser Recherche
> **Vollständige Analyse (Ergebnis):** [[{{Analyse-Notiz}}]] — bleibt im `Recherchen/`-Ordner, eingefroren
> **Destillierte Empfehlung (lebende Doku):** [[{{Empfehlungs-Notiz}}]] — im Projekt-Hauptordner, wird gepflegt
> **Template-Version:** `{{template_version}}` · **Recherche-Version:** `{{research_version}}` ({{research_date}})

*Ablageort: `{Projekt}/Recherchen/` — Datei in den Recherchen-Unterordner des jeweiligen Projekts legen, nicht in den Projekt-Root.*
*Ausgefülltes Beispiel: [[Recherche – PKM vs. PCM Begriffslandschaft]]*

---

## Aufgabe *(Schritt 1 — User)*

{{Die Recherche-Aufgabe wörtlich oder sinngemäß. Was soll herausgefunden werden?}}

> [!warning] Anweisung an Claude — Quellen-Ordner festlegen
> Sobald lokale Quellen im Spiel sind — entweder weil die Aufgabe vorhandene Clippings erwähnt, oder weil beim Recherche-Lauf Option A (manueller Download) benötigt wird — **vor dem ersten Speichern fragen:**
>
> ---
> **Für diese Recherche werden lokale Quellen benötigt. Wo sollen sie abgelegt werden?**
>
> **Option 1 — Globaler Ordner:** `Quellen/`
> Alle Recherchen teilen denselben Ordner. Sinnvoll bei wenigen Quellen (1–2) oder wenn die Quellen auch für andere Recherchen relevant sind.
>
> **Option 2 — Eigener Recherche-Unterordner:** `Quellen/{{Recherche-Slug}}/`
> Neuer Unterordner nur für diese Recherche. Empfohlen ab 3 Quellen oder bei thematisch enger, abgeschlossener Recherche.
>
> Antwort: **„Global"** oder **„Eigener Ordner"** (Claude legt den Unterordner dann automatisch an).
> ---
>
> Entscheidung unter **Quellen-Ordner** in der Metadaten-Tabelle eintragen. Alle weiteren Speicher-Anweisungen in dieser Recherche beziehen sich auf diesen Ordner.

---

## Metadaten *(Schritt 2 — AI)*

| Feld | Wert |
|---|---|
| **Analyse Datum** | {{YYYY-MM-DD}} |
| **Analyse Dauer** | {{z.B. ca. 20 Min. Workflow + Nachbearbeitung}} |
| **Methode** | {{z.B. /deep-research Workflow, manuelle Suche, kombiniert}} |
| **Quellen-Ordner** | {{`Quellen/` global · oder · `Quellen/{{Recherche-Slug}}/` eigen}} |
| **Eingesetzte Agenten** | {{Anzahl oder „k.A."}} |
| **Eingesetzte Tokens** | {{Anzahl (ca.) oder „nicht protokolliert"}} |
| **Gefundene Quellen** | {{Gesamt}} ({{automatisch}} automatisch + {{manuell}} manuell nachgeladen) |
| **Ausgewertete Quellen** | {{Anzahl}} |
| **Verifizierte Claims** | {{bestätigt}} von {{gesamt}} (adversariell, 3-Stimmen-Modell) |

*Versionsfelder zusätzlich im Frontmatter pflegen: `template_version`, `research_version`, `research_date` (siehe Abschnitt Versionierung).*

---

## Gefundene Quellen *(Schritte 3 & 4 — AI dokumentiert, User ergänzt manuell)*

*{{automatisch}} automatisch + {{manuell}} manuell nachgeladen. {{ausgewertet}} ausgewertet, {{nicht auswertbar}} nicht abrufbar / übersprungen.*

| Quelle | Herausgeber | Datum | Typ | Kernbeitrag | Bewertung |
|---|---|---|---|---|---|
| [Titel](URL) | Name | YYYY-MM | Typ | Kernbeitrag | ⭐⭐⭐ |

**Legende:** ⭐⭐⭐ Akademisch / peer-reviewed · ⭐⭐ Tech-Journalismus / Praktiker / Content Creator · ⚠️ Produkt-Marketing (mit Eigeninteresse)

### Nicht abrufbare Quellen *(Schritt 4 — User entscheidet, AI dokumentiert)*

*Von {{automatisch}} automatisch gefundenen Quellen waren {{nicht auswertbar}} nicht auswertbar:*

- **Manuell nachgeladen — Option A (User):**
  - `{{Titel}}` → [[{{Dateiname im Quellen-Ordner}}]]
- **Übersprungen — Option B:**
  - `{{URL oder Titel}}` — {{Grund: Paywall / JavaScript-heavy / kein relevanter Inhalt}}

> [!warning] Anweisung an Claude — Pause bei nicht abrufbaren Quellen
> Sobald nicht abrufbare Quellen identifiziert sind: **Auswertung hier stoppen** und folgende Nachricht ausgeben:
>
> ---
> **Folgende Quellen konnten nicht automatisch abgerufen werden:**
>
> - {{URL 1}} — {{Grund, z.B. Paywall}}
> - {{URL 2}} — {{Grund, z.B. JavaScript-heavy}}
>
> **Für jede Quelle bitte wählen:**
>
> **Option A — Manuell herunterladen:**
> *(Falls noch nicht festgelegt: erst Quellen-Ordner-Abfrage oben durchführen)*
> 1. Seite in **Brave oder Chrome** öffnen
> 2. **Obsidian Web Clipper** aktivieren → Zielordner **`{{Quellen-Ordner}}`** wählen → clippen
> 3. Bei PDFs: Datei direkt in **`{{Quellen-Ordner}}`** ablegen
> 4. Wenn fertig: **„Quellen geladen"** eingeben → Claude liest die neuen Dateien und wertet sie aus
>
> **Sonderfall YouTube / Video:** Web Clipper erzeugt automatisch ein Transkript. Ohne Clipper: [youtube-transcript.io](https://youtube-transcript.io) → Text als `.md` in `{{Quellen-Ordner}}`. Andere Plattformen: Untertitel-Export oder Option B.
>
> **Option B — Quelle überspringen:** Antwort: „Überspringen" oder Quelle namentlich nennen → wird unter „Übersprungen" eingetragen.
>
> Beide Optionen können kombiniert werden.
> ---

**Status:** ⏸ Warte auf Entscheidung → nach Option A: neue Dateien einlesen, Tabelle oben ergänzen · nach Option B: Eintrag ergänzen, weiter

---

## Ergebnis & Empfehlung *(Schritt 5 — AI)*

> [!tip] Contamination-Mitigation-Prinzip (Steph Ango, Obsidian-Mitgründer)
> **Rohe Analyse bleibt im „messy" Bereich, nur das destillierte Ergebnis kommt in den sauberen Vault.** Das Ergebnis wird deshalb zweigeteilt:

| Dokument | Ort | Zweck | Lebenszyklus |
|---|---|---|---|
| **[[{{Analyse-Notiz}}]]** | `Recherchen/` (messy) | Vollständige Analyse, alle Tabellen, Fazit | Eingefroren — Snapshot dieser Recherche |
| **[[{{Empfehlungs-Notiz}}]]** | Projekt-Hauptordner (clean) | Destillierte Empfehlung mit Recherche-Verweis | Lebende Doku — wird weiterentwickelt |

**Vorgehen:**
1. **Analyse-Notiz** in `Recherchen/` anlegen — vollständige Auswertung, Tabellen, Quellen-Analyse. Rückverlinkung unter dem Titel: `*Vollständige Analyse zur Recherche [[{{diese Datei}}]]. Destillierte Empfehlung: [[{{Empfehlungs-Notiz}}]].*`
2. **Empfehlung** destillieren: entweder eine neue Notiz im Projekt-Hauptordner **oder** als Abschnitt in eine bestehende Doku einbauen — immer mit Hinweis „basierend auf der Recherche [[{{diese Datei}}]]".

---

## Kurzes Resume *(Schritt 6 — AI, nach Erstellung von Analyse + Empfehlung)*

{{2–4 Sätze: Hauptbefund, wichtigste Erkenntnis, direkte Antwort auf die Ausgangsfrage.}}

---

## Versionierung

Zwei unabhängige Versionsnummern — beide im Frontmatter (`template_version`, `research_version`) und im Info-Block oben:

| Nummer | Bedeutung | Wann erhöhen |
|---|---|---|
| **`template_version`** | Version der verwendeten [[Templates/Recherche-Vorlage\|Recherche-Vorlage]] | Wird gesetzt, nicht erhöht — trägt die Version der Vorlage ein, mit der diese Recherche erstellt wurde |
| **`research_version`** | Durchführungs-Version *dieser* Recherche | +1 bei jeder erneuten Durchführung (Quellen aktualisiert, Frage neu untersucht) |

| Version | Datum | Template | Änderung |
|---|---|---|---|
| 1 | {{YYYY-MM-DD}} | {{template_version}} | Erstdurchführung |

**Bei erneuter Durchführung:** `research_version` +1, neue Zeile hier ergänzen, Analyse-Datei als neuen Snapshot anlegen (`{{Analyse-Notiz}} v2`) oder bestehende mit Versionshinweis aktualisieren. `template_version` auf die dann aktuelle Vorlagen-Version setzen.

---

*Vorlage: [[Templates/Recherche-Vorlage|Recherche-Vorlage (Template)]] (v{{template_version}}) · Schritt 7: In der Recherchen-Übersicht des jeweiligen Projekts eintragen (z.B. [[README#-recherchen]] für das Obsidian-Projekt)*

---

## Changelog der Vorlage *(nur in der Template-Datei pflegen, nicht in Kopien)*

| Template-Version | Datum | Änderung |
|---|---|---|
| 1.0 | 2026-06-14 | Erstversion: 7-Schritt-Workflow, Quellen-Ordner-Abfrage, Option A/B, YouTube-Transkript-Sonderfall, Contamination-Mitigation-Split, Versionierung |

**Versionsschema Template:** `MAJOR.MINOR` — MAJOR bei struktureller Workflow-Änderung (Schritte hinzufügen/entfernen), MINOR bei Feld- oder Wording-Ergänzungen.
