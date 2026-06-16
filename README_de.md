# VIB Hasenheide FDS-Ringsimulation

## Stufe 1: Semi-blinde Prognoserechnung

**Szenario:** `hep_160_150`  
**Berechnungsart:** Semi-Blind Prediction / semi-blinde Prognoserechnung  
**Software:** Fire Dynamics Simulator (FDS) 6.11.0  
**Status:** Vorbereitung / Call for Participation  
**Träger:** Verein zur Förderung von Ingenieurmethoden im Brandschutz e. V. (VIB)  
**Lizenz:** CC BY 4.0 (siehe [LICENSE](LICENSE))

---

## 1. Ziel der Studie

Diese Ringsimulation untersucht die Streuung von FDS-Prognosen für ein reales Brandversuchssetup. Im Mittelpunkt stehen Rauchtransport, Temperaturschichtung, Lichtextinktion, Rauchwarnmelderaktivierung und die daraus abgeleitete Bewertung der Personensicherheit.

Ziel ist nicht die Bewertung einzelner Teilnehmender. Untersucht wird vielmehr die Frage:

> Wie groß ist die Streuung von FDS-Prognosen für Rauchtransport, thermische Bedingungen, Lichtextinktion, Rauchwarnmelderaktivierung und Personensicherheit in einem realen Brandversuchssetup, wenn alle Teilnehmenden denselben Versuchsaufbau, dieselbe Geometrie, dieselben Messpositionen, dieselbe FDS-Version, dasselbe Template und dieselbe Massenverlustkurve verwenden, zentrale ingenieurmäßige Modellierungsentscheidungen aber selbst treffen und begründen?

Stufe 1 ist als **Semi-Blind Prediction** angelegt:

- **blind**, weil gemessene Temperaturen, optische Extinktionsdaten und Rauchwarnmelderaktivierungszeiten vor der Abgabe nicht offengelegt werden;
- **spezifiziert**, weil Szenario, Geometrie, Randbedingungen, FDS-Version, FDS-Template, Sensorpositionen und Massenverlustdaten bereitgestellt werden;
- **offen in den Modellierungsentscheidungen**, weil Teilnehmende zentrale Annahmen wie Gitterauflösung, Brandquellenumsetzung, Rußausbeute, Strahlungsanteil, Leckageannahmen und Wandmodellierung selbst festlegen und begründen.

Eine spätere **Open Calculation** ist geplant. In dieser Stufe werden die experimentellen Daten offengelegt. Danach können Modelle überarbeitet, Sensitivitäten durchgeführt und Abweichungen gezielt analysiert werden.

Durch die Vorgabe der Massenverlustkurve nimmt die Studie die Brandwachstumsprognose bewusst aus dem Untersuchungsumfang heraus und konzentriert sich auf Rauchtransport, thermische Schichtung, Lichtextinktion, Rauchwarnmelderaktivierung und Personensicherheit. Dies ist eine bewusste Entscheidung, um diese Größen von der bekannt großen Unsicherheit der Brandwachstumsmodellierung zu trennen.

Die Ergebnisse charakterisieren die Prognosestreuung für dieses spezifische Szenario und diese Teilnehmerstichprobe. Sie sind nicht als allgemeines Maß für die Zuverlässigkeit von FDS zu verstehen; breitere Schlüsse erfordern die für spätere Stufen geplanten weiteren Szenarien und Teilnehmenden.

---

## 2. Szenario und bereitgestellte Daten

Stufe 1 verwendet das Versuchssetup `hep_160_150` — eine Serie von drei Wiederholungs-Poolbrandversuchen in einem leerstehenden Wohngebäude. Der Brand befand sich im Raum F1 der Testwohnung „Fluppe“. Die vollständige Beschreibung steht in [`scenario/scenario_description.md`](scenario/scenario_description.md).

**Auf einen Blick**

| Größe | Wert |
|---|---|
| Szenario-ID | `hep_160_150` |
| Brandraum | F1 |
| Brennstoff | kommerzielles „Heptan“, C7-UVCB-Gemisch (n-/iso-/cyclische Alkane) |
| Brandwanne | 160 mm × 160 mm × 100 mm, 150 g initiale Brennstoffmasse |
| Wiederholungen | 3 |
| Auswertungsphase | Phase ohne Belüftung |
| Zielgrößen | Temperatur, Lichtextinktion (638 nm), Rauchwarnmelderaktivierung (DIN EN 14604), Personensicherheit |
| FDS-Version | FDS 6.11.0 |

Das Wohnungsmodell besteht aus drei verbundenen Räumen und einem Flur:

- **F1:** Brandraum,
- **F2:** angrenzender Raum,
- **F3:** weiterer angrenzender Raum,
- **FC:** Flur.

Die Innentüren zwischen diesen Bereichen waren entfernt. Die Fenster blieben während der Phase ohne Belüftung geschlossen. Der Zugang zum Treppenraum war durch eine geschlossene Kunststofffolientür abgetrennt.

![Überblick Raum F1](geometry/photos/Overview_F1_labelled.jpg)

![Überblick Raum F2](geometry/photos/Overview_F2.jpg)

![Blick vom Flur FC in Richtung F1/F2](geometry/photos/View_FC-F2.jpg)

| Folientür, geschlossen | Folientür, geöffnet |
|---|---|
| ![Folientür, geschlossen](geometry/photos/Plastic_sheet_door_closed.jpg) | ![Folientür, geöffnet](geometry/photos/Plastic_sheet_door_open.jpg) |

**Einheitlich für alle Teilnehmenden bereitgestellt:**

- Szenariobeschreibung — [`scenario/scenario_description.md`](scenario/scenario_description.md) (Ablauf, Brennstoffzusammensetzung, Umgebungsbedingungen, Instrumentierung, Messhöhen und -positionen).
- Geometrie — Grundriss, Schnitte und DXF-Zeichnungen in [`geometry/`](geometry/) ([Grundriss als PDF](geometry/Floor_plan_overview.pdf)).
- FDS-Template mit Referenzgeometrie und allen Messpositionen als `DEVC` — [`fds/`](fds/).
- Gemittelte und geglättete Massenverlustkurve — [`scenario/mass_loss_hep_160_150.csv`](scenario/mass_loss_hep_160_150.csv).

Diese Informationen bilden eine gemeinsame Basis; detaillierte Werte stehen in der Szenariobeschreibung und im FDS-Template.

---

## 3. Freie Modellierungsentscheidungen

Die folgenden Modellierungsentscheidungen bleiben bewusst frei. Sie müssen im Fragebogen dokumentiert und begründet werden.

Die Wahl des Surrogatbrennstoffs und der Verbrennungsparameter ist selbst Teil der untersuchten Modellierungsstreuung; die Quellen dieser Werte werden im Fragebogen erfasst, damit ihr Beitrag zur Gesamtstreuung separat analysiert werden kann.

| Bereich | Freie Entscheidung |
|---|---|
| Mesh | Zellgrößen, Mesh-Anordnung, Parallelisierung |
| Brandquelle | Umsetzung des vorgegebenen Massenverlusts, HRR-Ableitung, MLRPUA, RAMP-Funktionen. Die bereitgestellte Massenkurve wurde bereits geglättet; die durch numerische Differentiation abgeleitete MLRPUA bzw. HRRPUA sollte auf Plausibilität geprüft und bei Bedarf ebenfalls geglättet werden. |
| Brennstoffmodell | freie Wahl eines C7-Surrogats oder eigener Reaktionsdefinition |
| Rußausbeute | `SOOT_YIELD` |
| CO-Ausbeute | `CO_YIELD` |
| Strahlungsanteil | `RADIATIVE_FRACTION` |
| Wandmodell | inert, thermisch aktiv oder vereinfachte Schichten |
| Leckagen | keine, geschätzt oder parametrisiert |
| Anfangsbedingungen | sofern nicht ausdrücklich im Datenpaket vorgegeben |
| Numerische Einstellungen | soweit mit FDS 6.11.0 plausibel und dokumentiert |
| Personensicherheit | Kriterien für Fluchtbehinderung und Handlungsunfähigkeit |
| Sensitivitäten | optional, zusätzlich zur Hauptprognose |

Jede Abgabe muss eine eindeutig gekennzeichnete **Best-Estimate-Prognose** enthalten. Zusätzliche Sensitivitätsläufe sind willkommen, werden aber getrennt ausgewertet.

Die Best-Estimate-Prognose soll so realistisch wie möglich sein. Dies ist eine Prognoseübung, keine ingenieurmäßige Bemessung: Es sollen keine Sicherheitsfaktoren, bewusst konservativen Annahmen oder Worst-Case-Festlegungen verwendet werden. Ziel ist es, das tatsächliche Brandverhalten so genau wie möglich vorherzusagen.

---

## 4. FDS-Template

Das bereitgestellte FDS-Template ist die gemeinsame technische Grundlage für Stufe 1. Es enthält:

- die Referenzgeometrie,
- Raum- und Koordinatendefinitionen,
- Thermoelementpositionen als `DEVC`,
- optische Messpositionen als `DEVC`,
- Rauchwarnmelderpositionen als `DEVC`,
- Platzhalter für Brandquelle, Materialien, Mesh und weitere Modellierungsentscheidungen.

Das Template soll sicherstellen, dass alle Teilnehmenden dieselben Mess- und Auswertepositionen verwenden. Die Geometrie darf fachlich begründet angepasst oder verfeinert werden, wenn dies im Fragebogen dokumentiert wird. Brandquelle, Mesh, Materialmodellierung und rauchbezogene Parameter bleiben Teil der freien Modellierungsentscheidungen.

---

## 5. Nicht offengelegte Daten vor Abgabe

Die folgenden Informationen werden vor dem Abgabe-Freeze nicht bereitgestellt:

- gemessene Temperaturzeitreihen,
- gemessene optische Extinktionszeitreihen,
- Rauchwarnmelderaktivierungszeiten,
- Ergebnisse anderer Teilnehmender.

Die bereitgestellte Massenverlustkurve ist eine gemittelte und geglättete Kurve aus drei Wiederholungen. Ihre Umsetzung in FDS, z. B. als HRR-Randbedingung oder als Massenverlustrate, muss von den Teilnehmenden dokumentiert werden.

Mit der Offenlegung der experimentellen Daten wird die Auswertung die experimentelle Wiederholbarkeit (Streuung zwischen den Wiederholungen) quantifizieren und als Referenzband berichten, damit die Streuung der Simulationsergebnisse relativ zur experimentellen Unsicherheit und nicht gegen eine einzelne Kurve interpretiert werden kann.

---

## 6. Zielgrößen

Die folgenden Größen werden ausgewertet. Genaue Höhen, Positionen und die Referenzwellenlänge sind in [`scenario/scenario_description.md`](scenario/scenario_description.md) (§8) und in den `DEVC`-Einträgen des FDS-Templates definiert:

- **Temperatur** — Thermoelemente in F1, F2 und F3 an acht Höhen (0,6–2,5 m) sowie ein Deckenthermoelement über der Brandwanne in F1. Das Template verwendet `QUANTITY='THERMOCOUPLE'`, um die strahlungsbeeinflusste Perlenantwort der gemessenen Thermoelemente abzubilden.
- **Lichtextinktion** — Extinktionskoeffizient σ [1/m] an den optischen Messpositionen, Referenzwellenlänge 638 nm.
- **Rauchwarnmelderaktivierung** — optische Rauchwarnmelder (DIN EN 14604) an der Decke in F2, FC und F3.
- **Personensicherheit** — durch die Teilnehmenden bewertet in F1, F2, FC und F3.

### 6.1 Rauchwarnmelderaktivierung

Die Teilnehmenden sollen angeben, wie sie die Rauchwarnmelderaktivierung abbilden. Zulässig sind beispielsweise ein direktes FDS-Detektormodell, eine Aktivierung über eine selbst definierte optische Dichte bzw. Extinktionsschwelle oder eine andere dokumentierte und begründete Kenngröße.

In Stufe 1 wird keine gemeinsame „richtige“ Aktivierungsschwelle vorgegeben. Die Wahl der Aktivierungsmethode und des Schwellenwerts ist Teil der untersuchten Prognose: Die vorhergesagten Aktivierungszeiten werden mit den experimentell gemessenen Aktivierungszeiten verglichen, und die Streuung der gewählten Methoden wird analysiert, nicht entfernt.

### 6.2 Bewertung der Personensicherheit

Für F1, F2, FC und F3 soll abgeschätzt werden, ab wann relevante Fluchtbehinderung erreicht wird und ab wann Handlungsunfähigkeit zu erwarten ist. Die Bewertungsmethode ist zu dokumentieren; mögliche Kriterien sind Lichtextinktion bzw. Sichtweite, Temperatur, Rauchschichtlage, CO-Konzentration oder eine kombinierte ingenieurmäßige Beurteilung.

Die Wahl der Tauglichkeitskriterien und Grenzwerte ist selbst Gegenstand dieser Studie. Die Teilnehmenden legen ihre Kriterien daher selbst fest und begründen sie; die daraus resultierende Streuung der Kriterien und der vorhergesagten Tauglichkeitszeiten ist Teil der beabsichtigten Auswertung und wird mit den experimentellen Daten verglichen. Die Teilnehmenden dürfen zusätzliche Größen, Sensorpositionen oder abgeleitete Kenngrößen verwenden (z. B. Sichtweite, Rauchschichtlage, FED-bezogene Größen, Gaskonzentrationen), sofern diese im Fragebogen dokumentiert werden.

---

## 7. Repository-Struktur

```text
.
├── README.md
├── README_de.md
├── LICENSE
├── CITATION.cff
├── scenario/
│   ├── scenario_description.md
│   └── mass_loss_hep_160_150.csv
├── geometry/
│   ├── Floor_plan_overview.pdf
│   ├── 25103-01_1OG.pdf
│   ├── 25103-01_S01-06.pdf
│   ├── 25103-01_1OG.dxf
│   ├── S-02.dxf … S-06.dxf
│   └── photos/
├── fds/
│   └── hep_160_150_ParticipantID_RunID.fds
└── docs/
    ├── Call_for_Participation_de.pdf
    ├── Call_for_Participation_en.pdf
    ├── submission_format.md
    ├── faq.md
    └── privacy.md
```

---

## 8. Teilnahmeablauf

### Schritt 1: Registrierung

Interessierte Personen, Gruppen oder Organisationen registrieren sich per E-Mail:

```text
hasenheide@bcl-leipzig.de
```

Jeder eigenständige Beitrag (ein Team oder eine Bearbeiterin/ein Bearbeiter, die unabhängig arbeiten) erhält eine eigene anonyme Teilnehmer-ID, z. B. `K7M`, `3QA`, `BV5`. Eine Teilnehmer-ID entspricht einer Einreichung, die mehrere Läufe enthalten kann (eine Best-Estimate-Prognose plus optionale Sensitivitätsläufe); genau ein Lauf wird als `best_estimate` gekennzeichnet. Mehrere eigenständige Beiträge aus derselben Organisation sind willkommen.

### Schritt 2: Datenpaket

Die Teilnehmenden verwenden die aktuelle freigegebene Version dieses Repositories. Verbindlich sind ausschließlich offizielle Releases.

### Schritt 3: Simulation

Jede Gruppe führt mindestens eine Best-Estimate-Simulation des Szenarios `hep_160_150` mit FDS 6.11.0 durch. Optionale Sensitivitätsläufe können zusätzlich eingereicht werden.

### Schritt 4: Fragebogen

Die Teilnehmenden füllen den strukturierten Fragebogen aus (siehe Abschnitt 9), der ab dem Kick-off in diesem Repository bereitsteht.

### Schritt 5: Abgabe

Die Abgabe ist gemäß [`docs/submission_format.md`](docs/submission_format.md) zu packen und zu benennen: ein komprimiertes Archiv mit der/den FDS-Eingabedatei(en), etwaigen referenzierten Zusatzdateien, der FDS-Outputdatei (`.out`) und den CSV-Ergebnisdateien, wobei die Hauptprognose eindeutig als `best_estimate` gekennzeichnet ist.

### Schritt 6: Formale Abgabeprüfung

Das Auswertungsteam prüft die Abgabe formal auf Vollständigkeit, Dateistruktur, FDS-Version und Vorhandensein der FDS-Ausgabedateien sowie Konsistenz der `DEVC`-Ausgaben.

### Schritt 7: Abgabe-Freeze

Nach dem Abgabe-Freeze können bei Bedarf dokumentierte technische Korrekturen zugelassen werden. Fachliche oder modellbezogene Änderungen sind danach nicht mehr möglich.

### Schritt 8: Auswertung und Workshop

Nach dem Freeze werden die experimentellen Daten ausgewertet und den anonymisierten Simulationsergebnissen gegenübergestellt. Die Ergebnisse werden in einem Workshop diskutiert. Ziel des Workshops ist die gemeinsame Interpretation, nicht die Rangfolge der Teilnehmenden.

---

## 9. Fragebogen

Ein strukturierter Fragebogen ist verpflichtender Bestandteil jeder Abgabe. Statt der Werte selbst (die direkt aus der Eingabedatei ablesbar sind) erfasst er die **Begründungen und Quellen** hinter den freien Modellierungsentscheidungen — Brennstoff- und Verbrennungsparameter, Mesh, Wandrandbedingungen, Leckage und Rauchwarnmeldermethode — zusammen mit der Bewertung der Personensicherheit für F1, F2, FC und F3 sowie einigen Angaben zum Teilnehmerkontext. Der Fragebogen steht ab dem Kick-off in diesem Repository bereit.

---

## 10. Empfohlene optionale Sensitivitäten

Die folgenden Sensitivitätsstudien werden empfohlen, sind aber nicht verpflichtend:

| Sensitivität | Beispiel |
|---|---|
| Mesh | grob / mittel / fein |
| Rußausbeute | niedriger / höher |
| Strahlungsanteil | niedriger / höher |
| Leckage | keine / geschätzt |
| Wandmodell | inert / thermisch aktiv |
| Umsetzung des Massenverlusts | alternative HRR- oder MLRPUA-Umsetzungen |

Sensitivitäten sollen nicht zur nachträglichen Auswahl der „besten“ Kurve verwendet werden. Zentrale Vergleichsbasis bleibt die vorab gekennzeichnete Best-Estimate-Prognose.

---

## 11. Vorläufiger Zeitplan

| Phase | Beschreibung | Termin / Frist | Status |
|---|---|---|---|
| Vorbereitung | Repository, Datenpaket und Templates | — | abgeschlossen |
| Registrierung startet | Beginn der Anmeldung | ab 10.05.2026 | offen |
| Registrierungsschluss | Letzter Tag für die Anmeldung | 30.06.2026 | offen |
| Kick-off | Vorstellung von Szenario und Regeln | Einladung nach Registrierungsschluss | offen |
| Simulationsphase | Bearbeitung durch Teilnehmende | nach Kick-off – 30.09.2026 | offen |
| Frist für Rückfragen | Letzter Tag für technische Rückfragen | 15.09.2026 | offen |
| Abgabe-Freeze | Einfrieren aller Abgaben | 30.09.2026 | offen |
| Auswertung Stufe 1 | Vergleich mit Messdaten | tba | offen |
| Workshop | Diskussion der anonymisierten Ergebnisse | tba | offen |
| Open Calculation | spätere Stufe mit offengelegten Messdaten | tba | geplant |

---

## 12. Anonymisierung, Veröffentlichung und Autorenschaft

Die Abgaben werden zunächst intern durch das Auswertungsteam ausgewertet. In Berichten und Präsentationen werden Gruppen anonymisiert dargestellt, z. B. `K7M`, `3QA`, `BV5`.

Bei einer wissenschaftlichen Veröffentlichung können aktive Teilnehmende als Co-Autorinnen und Co-Autoren geführt werden, sofern sie zustimmen und die üblichen Voraussetzungen für eine Autorenschaft erfüllen. Autorenschaft und Reihenfolge werden vor Einreichung transparent abgestimmt.

Geplante Projektergebnisse sind:

- interner VIB-Bericht,
- Workshop-Präsentation,
- optionale wissenschaftliche Veröffentlichung,
- optionales öffentliches Benchmark-Datenpaket nach Abschluss der Studie.

Eine Veröffentlichung einzelner FDS-Dateien oder detaillierter Teilnehmendenergebnisse erfolgt nur nach separater Freigabe.

---

## 13. Rückfragen und verbindliche Antworten

Rückfragen sollen schriftlich an die Projektkoordination gerichtet werden:

```text
hasenheide@bcl-leipzig.de
```

Antworten, die für alle Teilnehmenden relevant sind, werden anonymisiert in [`docs/faq.md`](docs/faq.md) veröffentlicht. Verbindlich sind ausschließlich Informationen, die in diesem Repository oder in einem offiziellen Release dokumentiert sind.

---

## 14. Versionierung

Verbindlich für die Teilnahme ist der jeweils freigegebene GitHub-Release:

```text
https://github.com/openbcl/fds-roundrobin-hasenheide
```

Bei Abweichungen zwischen dem veröffentlichten Call for Participation und diesem Repository ist der aktuelle offizielle Repository-Release maßgeblich.

---

## 15. Kontakt

Projektkoordination:

```text
Manuel Osburg
Lukas Arnold

hasenheide@bcl-leipzig.de
```

Datenschutzinformationen: [`docs/privacy.md`](docs/privacy.md).

---

## 16. Checkliste für die Abgabe

Vor der Abgabe bitte prüfen:

- [ ] Best-Estimate-Lauf ist eindeutig gekennzeichnet.
- [ ] FDS 6.11.0 wurde verwendet.
- [ ] FDS-Eingabedatei `*.fds` ist enthalten.
- [ ] FDS-Outputdatei `*.out` ist enthalten.
- [ ] CSV-Ergebnisdateien `*.csv` sind enthalten.
- [ ] CSV-Spalten entsprechen den `DEVC`-IDs im FDS-Template (siehe [`docs/submission_format.md`](docs/submission_format.md)).
- [ ] Zusätzliche Dateien, die von der FDS-Eingabedatei referenziert werden, sind enthalten.
- [ ] Zusätzliche Größen, Sensorpositionen oder abgeleitete Kenngrößen für die Bewertung der Personensicherheit sind dokumentiert.
- [ ] Es wurden keine experimentellen Zielmessdaten verwendet.
- [ ] Das Archiv folgt der Namenskonvention.
- [ ] Der Fragebogen ist ausgefüllt.
- [ ] Das Archiv wurde an `hasenheide@bcl-leipzig.de` gesendet.

---

## 17. Kurzbeschreibung

Stufe 1 der VIB Hasenheide FDS-Ringsimulation ist eine semi-blinde FDS-Prognosestudie für das Brandszenario `hep_160_150`. Die Teilnehmenden erhalten eine gemeinsame Szenariobeschreibung, Geometrie, Randbedingungen, Messpositionen, eine gemittelte und geglättete Massenverlustkurve sowie ein FDS-Template. Experimentelle Temperaturen, optische Extinktionsdaten und Rauchwarnmelderaktivierungszeiten bleiben bis zur Abgabe verborgen. Zentrale Modellierungsentscheidungen wie Gitterauflösung, Brandquellenumsetzung, Rußausbeute, Strahlungsanteil, Leckageannahmen, Wandmodellierung, Rauchwarnmelder-Schwellen und Kriterien zur Bewertung der Personensicherheit bleiben frei und müssen dokumentiert werden. Ziel ist die Quantifizierung der Streuung von FDS-Prognosen und die Identifikation dominanter Einflussgrößen für Rauchtransport, Temperaturentwicklung, Lichtextinktion, Rauchwarnmelderaktivierung und Personensicherheit.
