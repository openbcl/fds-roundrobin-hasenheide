# VIB Hasenheide FDS-Ringsimulation

## Stufe 1: Semi-blinde Prognoserechnung

**Szenario:** `hep_160_150`  
**Berechnungsart:** Semi-Blind Prediction / semi-blinde Prognoserechnung  
**Software:** Fire Dynamics Simulator (FDS) 6.10.1  
**Status:** Vorbereitung / Call for Participation  
**Träger:** Verein zur Förderung von Ingenieurmethoden im Brandschutz e. V. (VIB)

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

---

## 2. Szenario

Stufe 1 verwendet das Versuchssetup:

```text
hep_160_150
```

Die Kennung bezeichnet ein Versuchssetup mit drei Wiederholungen, nicht ein einzelnes Experiment. Es handelt sich um Poolbrandversuche in einem leerstehenden Wohngebäude. Der Brand befand sich im Raum F1 der Testwohnung „Fluppe“.

| Größe | Beschreibung |
|---|---|
| Szenario-ID | `hep_160_150` |
| Brandraum | F1 |
| Brennstoff | kommerzielles „Heptan“, C7-UVCB-Kohlenwasserstoffgemisch |
| Mögliches FDS-Surrogat | freie Wahl eines C7-Surrogats oder eigener Reaktionsdefinition |
| Wannengeometrie | quadratische Brandwanne |
| Wannengröße | 160 mm × 160 mm |
| Wannentiefe | 100 mm |
| Initiale Brennstoffmasse | 150 g |
| Massenverlust | gemittelte und geglättete Brennstoffmassenkurve aus drei Wiederholungen |
| Wiederholungen | 3 |
| Auswertungsphase | Phase ohne Belüftung |
| Hauptzielgrößen | Temperatur, Lichtextinktion, Rauchwarnmelderaktivierung, Personensicherheit |
| Optische Referenzwellenlänge | 638 nm |
| Rauchwarnmelder | optische Rauchwarnmelder nach DIN EN 14604 |
| FDS-Version | FDS 6.10.1 |

Das relevante Wohnungsmodell besteht aus drei verbundenen Räumen und einem Flur:

- **F1:** Brandraum,
- **F2:** angrenzender Raum,
- **F3:** weiterer angrenzender Raum,
- **FC:** Flur.

Die Innentüren zwischen diesen Bereichen waren entfernt. Die Fenster blieben während der Phase ohne Belüftung geschlossen. Der Zugang zum Treppenraum war durch eine geschlossene Kunststofffolientür abgetrennt.

![Überblick Raum F1](geometry/photos/Overview_F1_labelled.jpg)

![Überblick Raum F2](geometry/photos/Overview_F2.jpg)

![Blick vom Flur FC in Richtung F1/F2](geometry/photos/View_FC-F2.jpg)

---

## 3. Bereitgestellte Eingangsdaten

Die folgenden Informationen werden allen Teilnehmenden einheitlich bereitgestellt und sollen für die Abgabe in Stufe 1 verwendet werden.

| Bereich | Vorgabe |
|---|---|
| Szenario | `hep_160_150` |
| Versuchsbeschreibung | Ablauf, Zündung, Phase ohne Belüftung und spätere Belüftung |
| Randbedingungen | dokumentierte Anfangs- und Umgebungsbedingungen |
| Zeichnungen | Grundriss, Raumhöhen, Schnitte, Raumbezeichnungen und relevante Maße [Grundriss (PDF)](geometry/Floor_plan_overview.pdf) |
| FDS-Version | FDS 6.10.1 |
| FDS-Template | Eingabedatei mit Referenzgeometrie und Sensorpositionen |
| Sensoren | `DEVC`-Einträge für Thermoelemente, optische Messpunkte und Rauchwarnmelderpositionen |
| Massenverlust | gemittelte und geglättete Brennstoffmassenkurve aus drei Wiederholungen |
| Gebäudestruktur | Räume F1, F2, F3 und FC gemäß Zeichnungen und Template |
| Brandort | Mittelpunkt der Brandwanne in Raum F1 |
| Wannenabmessungen | 160 mm × 160 mm × 100 mm |
| Brennstoffinformation | Hauptbestandteile: n-Heptan, Methylcyclohexan und weitere Isomere des Heptans |
| Initiale Brennstoffmasse | 150 g |
| Fensterzustand | geschlossen während der Phase ohne Belüftung |
| Türzustand | Innentüren entfernt; Tür zum Treppenraum geschlossen während der Phase ohne Belüftung |
| Messpositionen | Koordinaten der Thermoelemente, optischen Messpunkte und Rauchwarnmelder |
| Auswertezeitraum | Phase ohne Belüftung |
| Abgabeformat | FDS-Eingabedatei, FDS-Outputdatei, CSV-Ergebnisdateien und Fragebogen |
| Fragebogen-Link | `[NOCH ZU ERGÄNZEN: Link zum Fragebogen]` |
| Anonymisierung | Teilnehmende werden in Zwischenauswertungen anonymisiert |

---

## 4. Freie Modellierungsentscheidungen

Die folgenden Modellierungsentscheidungen bleiben bewusst frei. Sie müssen im Fragebogen dokumentiert und begründet werden.

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
| Numerische Einstellungen | soweit mit FDS 6.10.1 plausibel und dokumentiert |
| Personensicherheit | Kriterien für Fluchtbehinderung und Handlungsunfähigkeit |
| Sensitivitäten | optional, zusätzlich zur Hauptprognose |

Jede Abgabe muss eine eindeutig gekennzeichnete **Best-Estimate-Prognose** enthalten. Zusätzliche Sensitivitätsläufe sind willkommen, werden aber getrennt ausgewertet.

---

## 5. FDS-Template

Das bereitgestellte FDS-Template ist die gemeinsame technische Grundlage für Stufe 1. Es enthält:

- die Referenzgeometrie,
- Raum- und Koordinatendefinitionen,
- Thermoelementpositionen als `DEVC`,
- optische Messpositionen als `DEVC`,
- Rauchwarnmelderpositionen als `DEVC`,
- Platzhalter für Brandquelle, Materialien, Mesh und weitere Modellierungsentscheidungen.

Das Template soll sicherstellen, dass alle Teilnehmenden dieselben Mess- und Auswertepositionen verwenden. Die Geometrie darf fachlich begründet angepasst oder verfeinert werden, wenn dies im Fragebogen dokumentiert wird. Brandquelle, Mesh, Materialmodellierung und rauchbezogene Parameter bleiben Teil der freien Modellierungsentscheidungen.

---

## 6. Nicht offengelegte Daten vor Abgabe

Die folgenden Informationen werden vor dem Abgabe-Freeze nicht bereitgestellt:

- gemessene Temperaturzeitreihen,
- gemessene optische Extinktionszeitreihen,
- Rauchwarnmelderaktivierungszeiten,
- Ergebnisse anderer Teilnehmender.

Die bereitgestellte Massenverlustkurve ist eine gemittelte und geglättete Kurve aus drei Wiederholungen. Ihre Umsetzung in FDS, z. B. als HRR-Randbedingung oder als Massenverlustrate, muss von den Teilnehmenden dokumentiert werden.

---

## 7. Zielgrößen

### 7.1 Temperatur

Temperaturen werden in den Räumen F1, F2 und F3 an den vorgegebenen Thermoelementpositionen ausgewertet.

Vorgesehene Auswertehöhen sind:

```text
0.6 m
1.2 m
1.6 m
1.8 m
2.0 m
2.2 m
2.4 m
2.5 m
```

Zusätzlich wird im Brandraum F1 eine Deckentemperatur über der Brandwanne ausgewertet.

### 7.2 Lichtextinktion

Der Extinktionskoeffizient

```text
sigma [1/m]
```

wird an den optischen Messpositionen ausgewertet, insbesondere bei

```text
z = 2.3 m
```

in den Räumen:

```text
F1
F2
F3
```

Alle optischen Ergebnisse sollen auf die Referenzwellenlänge

```text
638 nm
```

bezogen werden.

### 7.3 Rauchwarnmelderaktivierung

Die Aktivierungszeiten der im Experiment installierten optischen Rauchwarnmelder werden ausgewertet. Die Sensoren waren optische Rauchwarnmelder nach:

```text
DIN EN 14604
```

Sie waren an der Decke in folgenden Bereichen installiert:

```text
F2
FC
F3
```

Die genaue Lage ist im FDS-Template über `DEVC`-Positionen definiert.

Die Teilnehmenden sollen angeben, wie sie die Rauchwarnmelderaktivierung in ihrer Simulation abbilden. Zulässig sind beispielsweise:

- direkte Nutzung eines FDS-Detektormodells,
- Aktivierung über eine selbst definierte optische Dichte oder Extinktionsschwelle,
- Aktivierung über eine andere dokumentierte und begründete Kenngröße.

In Stufe 1 wird keine gemeinsame „richtige“ Aktivierungsschwelle vorgegeben. Die Teilnehmenden müssen Methode und Schwellenwert für ihre Prognose selbst festlegen, begründen und dokumentieren.

### 7.4 Interpretation der Personensicherheit

Die Teilnehmenden sollen ihre Simulationsergebnisse hinsichtlich der Personensicherheit in folgenden Räumen interpretieren:

```text
F1
F2
F3
```

Für jeden Raum soll abgeschätzt werden, ab wann:

- relevante Fluchtbehinderung erreicht wird,
- Handlungsunfähigkeit zu erwarten ist.

Die Bewertungsmethode ist zu dokumentieren. Mögliche Kriterien sind Lichtextinktion bzw. Sichtweite, Temperatur, Rauchschichtlage, CO-Konzentration oder eine kombinierte ingenieurmäßige Beurteilung. Verwendete Kriterien und Grenzwerte müssen im Fragebogen angegeben werden.

Für den Vergleich mit den Experimentaldaten stehen die im FDS-Template vorgegebenen Größen und Positionen im Mittelpunkt. Für die eigene Bewertung der Personensicherheit dürfen die Teilnehmenden jedoch zusätzliche Größen, Sensorpositionen oder abgeleitete Kenngrößen verwenden, sofern diese im Fragebogen dokumentiert werden.

Dazu können beispielsweise Sichtweite, Rauchschichtlage, FED-bezogene Größen, Gaskonzentrationen, Temperaturgrenzwerte an weiteren Höhen oder raumspezifische ingenieurmäßige Kriterien gehören.

---

## 8. Repository-Struktur

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
│   ├── S-02.dxf
│   ├── S-03.dxf
│   ├── S-04.dxf
│   ├── S-05.dxf
│   ├── S-06.dxf
│   └── photos/
├── fds/
│   └── hep_160_150_ParticipantID_RunID.fds
└── docs/
    ├── Call_for_Participation_de.pdf
    ├── Call_for_Participation_en.pdf
    └── faq.md

```

---

## 9. Teilnahmeablauf

### Schritt 1: Registrierung

Interessierte Personen, Gruppen oder Organisationen registrieren sich per E-Mail:

```text
hasenheide@bcl-leipzig.de
```

Aus einer Organisation oder Arbeitsgruppe können mehrere Einreichungen erfolgen. Jede geplante Einreichung erhält eine eigene anonyme Teilnehmer-ID, z. B.:

```text
P01
P02
P03
```

### Schritt 2: Datenpaket

Die Teilnehmenden verwenden die aktuelle freigegebene Version dieses Repositories. Verbindlich sind ausschließlich offizielle Releases.

### Schritt 3: Simulation

Jede Gruppe führt mindestens eine Best-Estimate-Simulation des Szenarios `hep_160_150` mit FDS 6.10.1 durch.

Optionale Sensitivitätsläufe können zusätzlich zur Best-Estimate-Prognose eingereicht werden.

### Schritt 4: Fragebogen

Die Teilnehmenden füllen den strukturierten Fragebogen aus:

```text
[NOCH ZU ERGÄNZEN: Link zum Fragebogen]
```

Der Fragebogen erfasst Modellierungsentscheidungen, Annahmen, relevante Metadaten sowie die Bewertung der Personensicherheit in den betrachteten Räumen F1, F2 und F3.

### Schritt 5: Abgabe

Die Abgabe erfolgt als komprimiertes Archiv an die Projektkoordination.

Archivname:

```text
VIB_Hasenheide_Stage1_<ParticipantID>.zip
```

Beispiel:

```text
VIB_Hasenheide_Stage1_P03.zip
```

Das Archiv enthält die FDS-Eingabedatei, etwaige zusätzliche Dateien, die von der FDS-Eingabedatei referenziert werden, die FDS-Outputdatei und CSV-Ergebnisdateien.

Für einen einzelnen Lauf:

```text
submission/
├── *.fds
├── *.out
├── *.csv
└── [optional] additional_files/
```

Für mehrere Läufe:

```text
submission/
├── best_estimate/
├── sensitivity_01/
├── sensitivity_02/
└── sensitivity_03/
```

Die Hauptprognose muss eindeutig als

```text
best_estimate
```

gekennzeichnet sein.

### Schritt 6: Formale Abgabeprüfung

Das Auswertungsteam prüft die Abgabe formal auf Vollständigkeit, Dateistruktur, FDS-Version und Vorhandensein der FDS-Ausgabedateien sowie Konsistenz der `DEVC`-Ausgaben.

### Schritt 7: Abgabe-Freeze

Nach dem Abgabe-Freeze können bei Bedarf dokumentierte technische Korrekturen zugelassen werden. Fachliche oder modellbezogene Änderungen sind danach nicht mehr möglich.

### Schritt 8: Auswertung und Workshop

Nach dem Freeze werden die experimentellen Daten ausgewertet und den anonymisierten Simulationsergebnissen gegenübergestellt. Die Ergebnisse werden in einem Workshop diskutiert. Ziel des Workshops ist die gemeinsame Interpretation, nicht die Rangfolge der Teilnehmenden.

---

## 10. CSV-Ergebnisdateien

Die eingereichten CSV-Dateien sollen die Sensorausgaben aus dem FDS-Template widerspiegeln. Die Spaltennamen ergeben sich daher aus den `DEVC`-IDs im Template.

### 10.1 Dateiname

FDS generiert die Sensorausgabedatei automatisch aus der im Template definierten `CHID`. Bei unveränderter Verwendung der Template-`CHID`-Struktur ergibt sich:

```text
hep_160_150_<ParticipantID>_<RunID>_devc.csv
```

Beispiel für Teilnehmende P03, Best-Estimate-Lauf:

```text
hep_160_150_P03_best_estimate_devc.csv
```

Diese Datei ist in jeder Abgabe verpflichtend. Bei mehreren Läufen muss jedes Unterverzeichnis eine eigene `_devc.csv`-Datei enthalten.

### 10.2 Spaltenstruktur

Die erste Spalte ist stets `Time` (in Sekunden). Die weiteren Spalten entsprechen den `DEVC`-IDs aus dem Template in der Reihenfolge der Einträge in der FDS-Eingabedatei.

**Temperaturprofile** — 8 Höhen je Raum (0,6 / 1,2 / 1,6 / 1,8 / 2,0 / 2,2 / 2,4 / 2,5 m):

| ID-Muster | Raum | Spaltennamen |
|---|---|---|
| `TC_F1_<h>` | F1 | `TC_F1_0_6`, `TC_F1_1_2`, …, `TC_F1_2_5` |
| `TC_F2_<h>` | F2 | `TC_F2_0_6`, `TC_F2_1_2`, …, `TC_F2_2_5` |
| `TC_F3_<h>` | F3 | `TC_F3_0_6`, `TC_F3_1_2`, …, `TC_F3_2_5` |

Höhennotation: Dezimalpunkt wird durch Unterstrich ersetzt, z. B. 0,6 m → `0_6`, 2,5 m → `2_5`.

**Extinktionskoeffizientenprofile** — gleiche Positionen wie Temperaturprofile:

| ID-Muster | Raum |
|---|---|
| `EXT_F1_<h>` | F1 |
| `EXT_F2_<h>` | F2 |
| `EXT_F3_<h>` | F3 |

**Deckenthermocouples:**

| Spaltenname | Ort |
|---|---|
| `TC_Ceiling_F1` | F1, über Brandwanne |

**Optische Messpositionen** (exakte Positionen der experimentellen Messgeräte):

| Spaltenname | Raum | Höhe [m] |
|---|---|---|
| `EXT_DEVC_F1_2_3` | F1 | 2,3 |
| `EXT_DEVC_F2_1_5` | F2 | 1,5 |
| `EXT_DEVC_F2_1_9` | F2 | 1,9 |
| `EXT_DEVC_F2_2_1` | F2 | 2,1 |
| `EXT_DEVC_F2_2_3` | F2 | 2,3 |
| `EXT_DEVC_F3_2_3` | F3 | 2,3 |

**Rauchwarnmelderpositionen** (Extinktionskoeffizient an der Decke):

| Spaltenname | Raum |
|---|---|
| `SD_F2_EXT` | F2 |
| `SD_FC_EXT` | FC |
| `SD_F3_EXT` | F3 |

### 10.3 Hinweise

- Die `DEVC`-Einträge im Template dürfen nicht umbenannt oder entfernt werden. Einheitliche Spaltennamen über alle Abgaben sind Voraussetzung für automatisiertes Post-Processing und den Vergleich.
- Zusätzliche `DEVC`-Einträge der Teilnehmenden (z. B. für Sensitivitätsausgaben oder Personensicherheitskenngrößen) dürfen als weitere Spalten enthalten sein. Sie beeinflussen die Pflichtspalten nicht.
- Die von FDS generierte `_devc.csv`-Datei verwendet einen zweizeiligen Header: Die erste Zeile enthält die `DEVC`-IDs, die zweite Zeile die physikalischen Einheiten. Beide Zeilen müssen in der eingereichten Datei vorhanden sein.
- Die Rauchwarnmelder-`DEVC`-Einträge (`SD_F2_EXT`, `SD_FC_EXT`, `SD_F3_EXT`) enthalten einen Platzhalter `SETPOINT=...`. Dieser ist durch den selbst gewählten Aktivierungsschwellenwert in 1/m zu ersetzen. Mit definiertem `SETPOINT` trägt FDS die Aktivierungszeit automatisch in die `.out`-Datei unter „DEVICE Activation Times" ein. Die `_devc.csv` enthält weiterhin unverändert die kontinuierliche Extinktionskoeffizienten-Zeitreihe.

---

## 11. Inhalte des Fragebogens

Der Fragebogen erfasst unter anderem:

- Teilnehmer-ID,
- Organisation bzw. Arbeitsgruppe, sofern für die interne Koordination gewünscht,
- Einverständnis zur Co-Autorenschaft bei einer wissenschaftlichen Veröffentlichung,
- verwendete Werkzeuge für Modellierung und Nachbearbeitung, z. B. PyroSim, Python oder fdsreader,
- Nutzung oder Anpassung des bereitgestellten FDS-Templates,
- Meshstrategie und fachliche Begründung,
- Umsetzung des vorgegebenen Massenverlusts,
- verwendetes Brennstoff- bzw. Reaktionsmodell,
- gewählte Rußausbeute,
- gewählte CO-Ausbeute,
- gewählter Strahlungsanteil,
- verwendeter massenspezifischer Extinktionskoeffizient,
- Annahmen zu Leckagen,
- Wand- und Materialmodellierung,
- Modellierung bzw. Interpretation der optischen Rauchwarnmelder nach DIN EN 14604,
- Kriterien für Fluchtbehinderung und Handlungsunfähigkeit in F1, F2 und F3,
- wichtigste Unsicherheiten aus Sicht der Teilnehmenden.

---

## 12. Empfohlene optionale Sensitivitäten

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

## 13. Vorläufiger Zeitplan

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

## 14. Anonymisierung, Veröffentlichung und Autorenschaft

Die Abgaben werden zunächst intern durch das Auswertungsteam ausgewertet. In Berichten und Präsentationen werden Gruppen anonymisiert dargestellt, z. B.:

```text
P01
P02
P03
```

Bei einer wissenschaftlichen Veröffentlichung können aktive Teilnehmende als Co-Autorinnen und Co-Autoren geführt werden, sofern sie zustimmen und die üblichen Voraussetzungen für eine Autorenschaft erfüllen. Autorenschaft und Reihenfolge werden vor Einreichung transparent abgestimmt.

Geplante Projektergebnisse sind:

- interner VIB-Bericht,
- Workshop-Präsentation,
- optionale wissenschaftliche Veröffentlichung,
- optionales öffentliches Benchmark-Datenpaket nach Abschluss der Studie.

Eine Veröffentlichung einzelner FDS-Dateien oder detaillierter Teilnehmendenergebnisse erfolgt nur nach separater Freigabe.

---

## 15. Rückfragen und verbindliche Antworten

Rückfragen sollen schriftlich an die Projektkoordination gerichtet werden:

```text
hasenheide@bcl-leipzig.de
```

Antworten, die für alle Teilnehmenden relevant sind, werden anonymisiert veröffentlicht in:

```text
docs/faq.md
```

Verbindlich sind ausschließlich Informationen, die in diesem Repository oder in einem offiziellen Release dokumentiert sind.

---

## 16. Versionierung

Verbindlich für die Teilnahme ist der jeweils freigegebene GitHub-Release:

```text
https://github.com/openbcl/fds-roundrobin-hasenheide
```

---

## 17. Kontakt

Projektkoordination:

```text
Manuel Osburg
Lukas Arnold

hasenheide@bcl-leipzig.de
```

---

## 18. Checkliste für die Abgabe

Vor der Abgabe bitte prüfen:

- [ ] Best-Estimate-Lauf ist eindeutig gekennzeichnet.
- [ ] FDS 6.10.1 wurde verwendet.
- [ ] FDS-Eingabedatei `*.fds` ist enthalten.
- [ ] FDS-Outputdatei `*.out` ist enthalten.
- [ ] CSV-Ergebnisdateien `*.csv` sind enthalten.
- [ ] CSV-Spalten entsprechen den `DEVC`-IDs im FDS-Template.
- [ ] Zusätzliche Dateien, die von der FDS-Eingabedatei referenziert werden, sind enthalten.
- [ ] Zusätzliche Größen, Sensorpositionen oder abgeleitete Kenngrößen für die Bewertung der Personensicherheit sind dokumentiert.
- [ ] Es wurden keine experimentellen Zielmessdaten verwendet.
- [ ] Das Archiv folgt der Namenskonvention.
- [ ] Der Fragebogen ist ausgefüllt: `[NOCH ZU ERGÄNZEN: Link zum Fragebogen]`.
- [ ] Das Archiv wurde an `hasenheide@bcl-leipzig.de` gesendet.

---

## 19. Kurzbeschreibung

Stufe 1 der VIB Hasenheide FDS-Ringsimulation ist eine semi-blinde FDS-Prognosestudie für das Brandszenario `hep_160_150`. Die Teilnehmenden erhalten eine gemeinsame Szenariobeschreibung, Geometrie, Randbedingungen, Messpositionen, eine gemittelte und geglättete Massenverlustkurve sowie ein FDS-Template. Experimentelle Temperaturen, optische Extinktionsdaten und Rauchwarnmelderaktivierungszeiten bleiben bis zur Abgabe verborgen. Zentrale Modellierungsentscheidungen wie Gitterauflösung, Brandquellenumsetzung, Rußausbeute, Strahlungsanteil, Leckageannahmen, Wandmodellierung, Rauchwarnmelder-Schwellen und Kriterien zur Bewertung der Personensicherheit bleiben frei und müssen dokumentiert werden. Ziel ist die Quantifizierung der Streuung von FDS-Prognosen und die Identifikation dominanter Einflussgrößen für Rauchtransport, Temperaturentwicklung, Lichtextinktion, Rauchwarnmelderaktivierung und Personensicherheit.
