# VIB Hasenheide FDS Round-Robin Study

## Stage 1: Semi-Blind Prediction Exercise

**Scenario:** `hep_160_150`  
**Exercise type:** Semi-blind prediction  
**Simulation code:** Fire Dynamics Simulator (FDS) 6.10.1  
**Status:** Preparation / Call for Participation  
**Organiser:** Verein zur Förderung von Ingenieurmethoden im Brandschutz e. V. (VIB)

---

## 1. Purpose and scope

This FDS round-robin study investigates the variability of numerical predictions for a full-scale compartment fire experiment. The focus is on smoke transport, thermal stratification, optical extinction, smoke alarm actuation and the resulting tenability assessment.

The purpose is not to rank individual participants. The study addresses the following question:

> How large is the variability of FDS predictions for smoke transport, thermal conditions, optical extinction, smoke alarm actuation and tenability in a full-scale compartment fire when all participants use the same experimental setup, geometry, measurement locations, FDS version, template and fuel mass history, but make their own justified engineering modelling choices?

Stage 1 is conducted as a **semi-blind prediction exercise**:

- **blind**, because measured gas temperatures, optical extinction data and smoke alarm actuation times are not disclosed before submission;
- **specified**, because the scenario description, geometry, boundary conditions, FDS version, FDS template, measurement locations and fuel mass history are provided;
- **open with respect to modelling assumptions**, because participants define and justify key modelling choices such as mesh resolution, fire source specification, soot yield, radiative fraction, leakage assumptions and wall boundary conditions.

A later **open calculation** stage is planned. In that stage, experimental data will be disclosed and participants may revise their models, perform sensitivity analyses and investigate the causes of deviations.

---

## 2. Scenario

Stage 1 uses the experimental setup:

```text
hep_160_150
```

The identifier refers to a test setup with three replicate tests, not to one individual experiment. The tests were liquid pool fire experiments conducted in a vacant residential building. The fire was located in room F1 of the test apartment “Fluppe”.

| Item | Description |
|---|---|
| Scenario ID | `hep_160_150` |
| Fire compartment | F1 |
| Fuel | Commercial “heptane”, C7-UVCB hydrocarbon mixture |
| Suggested FDS surrogate fuel | Participant-defined C7 surrogate or user-defined reaction |
| Burner / pan geometry | Square pan |
| Pan size | 160 mm × 160 mm |
| Pan depth | 100 mm |
| Initial fuel mass | 150 g |
| Fuel mass history | Averaged and smoothed fuel mass curve derived from three replicate tests |
| Replicate tests | 3 |
| Evaluation period | Pre-ventilation period |
| Main quantities of interest | Gas temperature, optical extinction, smoke alarm actuation, tenability |
| Optical reference wavelength | 638 nm |
| Smoke alarms | Optical smoke alarms according to DIN EN 14604 |
| FDS version | FDS 6.10.1 |

The relevant apartment layout consists of three interconnected rooms and a corridor:

- **F1:** fire compartment,
- **F2:** adjacent room,
- **F3:** further adjacent room,
- **FC:** corridor.

Internal doors between these areas were removed. Windows remained closed during the pre-ventilation period. The entrance to the stairwell was separated by a closed plastic foil door.

![Overview F1](geometry/photos/Overview_F1_labelled.jpg)

![Overview F2](geometry/photos/Overview_F2.jpg)

![View from FC to F1/F2](geometry/photos/View_FC-F2.jpg)

---

## 3. Provided input data

The following information is provided uniformly to all participants and shall be used for the Stage 1 submission.

| Category | Provided information |
|---|---|
| Scenario | `hep_160_150` |
| Test description | Test sequence, ignition, pre-ventilation period and subsequent ventilation |
| Boundary conditions | Documented initial and ambient conditions |
| Drawings | Floor plan, room heights, sections, room names and relevant dimensions [Floor plan (PDF)](geometry/Floor_plan_overview.pdf) |
| FDS version | FDS 6.10.1 |
| FDS template | Input file with reference geometry and measurement locations |
| Instrumentation | `DEVC` entries for thermocouples, optical measurement points and smoke alarm locations |
| Fuel mass history | Averaged and smoothed fuel mass curve derived from the three replicate tests |
| Building layout | Rooms F1, F2, F3 and FC according to drawings and template |
| Fire location | Centre of the pan in room F1 |
| Pan dimensions | 160 mm × 160 mm × 100 mm |
| Fuel information | C7-UVCB mixture of n-alkanes, iso-alkanes and cyclic alkanes (predominantly n-heptane and methylcyclohexane) |
| Initial fuel mass | 150 g |
| Window condition | Closed during the pre-ventilation period |
| Door condition | Internal doors removed; stairwell door closed during the pre-ventilation period |
| Measurement locations | Coordinates of thermocouples, optical measurement points and smoke alarms |
| Evaluation period | Pre-ventilation period |
| Submission format | FDS input file, FDS output file, CSV result files and questionnaire |
| Questionnaire link | `[TO BE ADDED: questionnaire link]` |
| Anonymisation | Participants are anonymised in intermediate evaluations |

---

## 4. Modelling choices left to the participants

The following modelling choices are intentionally left to the participants. They must be documented and justified in the questionnaire.

| Category | Modelling choice |
|---|---|
| Computational mesh | Cell sizes, mesh layout, domain decomposition and parallelisation |
| Fire source specification | Implementation of the provided fuel mass history, HRR derivation, MLRPUA, RAMP functions. The provided fuel mass curve has been smoothed; participants should verify that the MLRPUA or HRRPUA derived by numerical differentiation is also sufficiently smooth and apply additional smoothing if necessary. |
| Fuel / reaction model | Participant-defined C7 surrogate or user-defined reaction |
| Soot yield | `SOOT_YIELD` |
| CO yield | `CO_YIELD` |
| Radiative fraction | `RADIATIVE_FRACTION` |
| Wall boundary conditions | Inert, thermally active or simplified layered constructions |
| Leakage / infiltration | None, estimated or parameterised |
| Initial conditions | Where not explicitly specified in the data package |
| Numerical settings | As long as they are plausible for FDS 6.10.1 and documented |
| Tenability assessment | Criteria for impaired egress and incapacitation |
| Sensitivity analyses | Optional, in addition to the main prediction |

Each submission must contain one clearly identified **best-estimate prediction**. Additional sensitivity cases are welcome but will be evaluated separately.

---

## 5. FDS template

The provided FDS template is the common technical basis for Stage 1. It contains:

- the reference geometry,
- room and coordinate definitions,
- thermocouple locations as `DEVC`,
- optical measurement locations as `DEVC`,
- smoke alarm locations as `DEVC`,
- placeholders for the fire source, material properties, mesh and other modelling choices.

The template is intended to ensure that all participants use the same measurement and evaluation locations. The geometry may be adapted or refined if this is technically justified and documented in the questionnaire. Fire source specification, mesh, material properties and smoke-related parameters remain part of the free modelling choices.

---

## 6. Data not disclosed before submission

The following information is not provided before the submission freeze:

- measured gas temperature time series,
- measured optical extinction time series,
- smoke alarm actuation times,
- results from other participants.

The provided fuel mass history is an averaged and smoothed curve derived from three replicate tests. Its implementation in FDS, for example as a prescribed heat release rate or as a mass loss rate, must be documented by the participants.

---

## 7. Quantities of interest

### 7.1 Gas temperature

Gas temperatures are evaluated in rooms F1, F2 and F3 at the specified thermocouple locations.

Measurement heights:

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

In addition, a ceiling gas temperature above the pan is evaluated in the fire compartment F1.

### 7.2 Optical extinction

The optical extinction coefficient

```text
sigma [1/m]
```

is evaluated at the optical measurement locations, in particular at

```text
z = 2.3 m
```

in the rooms:

```text
F1
F2
F3
```

All optical results shall refer to the reference wavelength:

```text
638 nm
```

### 7.3 Smoke alarm actuation

The actuation times of the optical smoke alarms installed in the experiment are evaluated. The smoke alarms were optical devices according to:

```text
DIN EN 14604
```

They were installed at the ceiling in:

```text
F2
FC
F3
```

The exact locations are defined in the FDS template via `DEVC` positions.

Participants shall state how smoke alarm actuation is represented in their simulation. Acceptable approaches include, for example:

- direct use of an FDS detector model,
- actuation based on a participant-defined optical density or extinction threshold,
- actuation based on another documented and justified quantity.

No common “correct” actuation threshold is prescribed in Stage 1. Participants must define, justify and document the method and threshold used for their own prediction.

### 7.4 Tenability assessment

Participants shall interpret their simulation results with respect to tenability in the following compartments:

```text
F1
F2
FC
F3
```

For each room, participants shall estimate when:

- conditions relevant to impaired egress are reached,
- incapacitation is expected.

The assessment methodology shall be documented. Possible criteria include optical extinction or visibility, gas temperature, smoke layer height, CO concentration or a combined engineering judgement. The applied criteria and threshold values shall be specified in the questionnaire.

For the common comparison, the quantities and locations defined in the FDS template form the primary basis. However, participants may use additional quantities, sensor locations or derived indicators for their own tenability assessment, provided that these are documented in the questionnaire.

Such additional information may include, for example, visibility, smoke layer height, FED-related quantities, gas concentrations, temperature limits at additional heights or compartment-specific engineering criteria.

---

## 8. Repository structure

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

## 9. Participation workflow

### Step 1: Registration

Interested individuals, teams or organisations register by email:

```text
hasenheide@bcl-leipzig.de
```

Multiple submissions from the same organisation or working group are possible. Each planned submission receives a separate anonymous participant ID, for example:

```text
K7M
3QA
BV5
```

### Step 2: Data package

Participants use the current released version of this repository. Only official releases are binding.

### Step 3: Simulation

Each group performs at least one best-estimate simulation of `hep_160_150` using FDS 6.10.1.

Optional sensitivity cases may be submitted in addition to the best-estimate prediction.

### Step 4: Questionnaire

Participants complete the structured questionnaire:

```text
[TO BE ADDED: questionnaire link]
```

The questionnaire records modelling choices, assumptions, relevant metadata and the tenability assessment for the rooms F1, F2 and F3.

### Step 5: Submission

Submissions are sent as compressed archives to the project coordination.

Archive name:

```text
VIB_Hasenheide_Stage1_<ParticipantID>.zip
```

Example:

```text
VIB_Hasenheide_Stage1_K7M.zip
```

The archive shall contain the FDS input file, any additional files referenced by the FDS input, the FDS output file and CSV result files.

For a single case:

```text
submission/
├── *.fds
├── *.out
├── *.csv
└── [optional] additional_files/
```

For multiple cases:

```text
submission/
├── best_estimate/
├── sensitivity_01/
├── sensitivity_02/
└── sensitivity_03/
```

The main prediction must be clearly identified as:

```text
best_estimate
```

### Step 6: Formal submission check

The evaluation team checks the submission for completeness, file structure, FDS version, presence of FDS output files and consistency of the `DEVC` outputs.

### Step 7: Submission freeze

After the submission freeze, technical corrections may be allowed if necessary and documented. Scientific or modelling changes are no longer accepted.

### Step 8: Evaluation and workshop

After the freeze, the experimental data are evaluated and compared with the anonymised simulation results. The findings are discussed in a workshop. The purpose of the workshop is joint interpretation, not ranking of participants.

---

## 10. CSV result files

The submitted CSV files shall mirror the device outputs defined in the FDS template. The column names are therefore derived from the `DEVC` IDs in the template.

### 10.1 File naming

FDS generates the device output file automatically from the `CHID` defined in the template. Using the template without modification to the `CHID` structure produces:

```text
hep_160_150_<ParticipantID>_<RunID>_devc.csv
```

Example for participant K7M, best-estimate case:

```text
hep_160_150_K7M_best_estimate_devc.csv
```

This file is required in every submission. For multiple cases, each subdirectory must contain its own `_devc.csv` file.

### 10.2 Column structure

The first column is always `Time` (in seconds). The remaining columns correspond to the `DEVC` IDs defined in the template, in the order they appear in the FDS input file.

**Thermocouple profiles** — 8 heights per room (0.6, 1.2, 1.6, 1.8, 2.0, 2.2, 2.4, 2.5 m):

| ID pattern | Room | Column names |
|---|---|---|
| `TC_F1_<h>` | F1 | `TC_F1_0_6`, `TC_F1_1_2`, …, `TC_F1_2_5` |
| `TC_F2_<h>` | F2 | `TC_F2_0_6`, `TC_F2_1_2`, …, `TC_F2_2_5` |
| `TC_F3_<h>` | F3 | `TC_F3_0_6`, `TC_F3_1_2`, …, `TC_F3_2_5` |

Height notation: the decimal point is replaced by an underscore, e.g. 0.6 m → `0_6`, 2.5 m → `2_5`.

**Extinction coefficient profiles** — same positions as thermocouple profiles:

| ID pattern | Room |
|---|---|
| `EXT_F1_<h>` | F1 |
| `EXT_F2_<h>` | F2 |
| `EXT_F3_<h>` | F3 |

**Ceiling thermocouples:**

| Column name | Location |
|---|---|
| `TC_Ceiling_F1` | F1, above fire pan |

**Optical measurement device positions** (exact experimental instrument locations):

| Column name | Room | Height [m] |
|---|---|---|
| `EXT_DEVC_F1_2_3` | F1 | 2.3 |
| `EXT_DEVC_F2_1_5` | F2 | 1.5 |
| `EXT_DEVC_F2_1_9` | F2 | 1.9 |
| `EXT_DEVC_F2_2_1` | F2 | 2.1 |
| `EXT_DEVC_F2_2_3` | F2 | 2.3 |
| `EXT_DEVC_F3_2_3` | F3 | 2.3 |

**Smoke alarm positions** (extinction coefficient at ceiling):

| Column name | Room |
|---|---|
| `SD_F2_EXT` | F2 |
| `SD_FC_EXT` | FC |
| `SD_F3_EXT` | F3 |

### 10.3 Notes

- Do not rename or remove the `DEVC` entries defined in the template. This ensures consistent column names across all submissions and enables automated post-processing.
- If additional `DEVC` entries are added by the participant (e.g. for sensitivity outputs or tenability indicators), these appear as additional columns and do not affect the required columns listed above.
- The `_devc.csv` file generated by FDS uses a two-line header: the first line contains the `DEVC` IDs, the second line the physical units. Both lines must be present in the submitted file.
- The smoke alarm `DEVC` entries (`SD_F2_EXT`, `SD_FC_EXT`, `SD_F3_EXT`) contain a `SETPOINT=...` placeholder. Replace `...` with the participant-defined activation threshold in 1/m. With `SETPOINT` defined, FDS records the activation time automatically in the `.out` file under "DEVICE Activation Times". The `_devc.csv` continues to contain the continuous extinction coefficient time series unchanged.

---

## 11. Questionnaire contents

The questionnaire records, among other items:

- participant ID and run ID,
- whether the simulation was performed individually or as a team,
- justification and literature references for the C7 surrogate fuel, including soot yield, CO yield, radiative fraction, net heat of combustion and mass-specific extinction coefficient,
- sources for combustion parameters (experimental data, handbook value, FDS default, engineering judgement),
- justification for mesh resolution and target D*/dx near the fire source,
- justification for wall boundary conditions and material properties,
- approach to air leakage modelling and its justification,
- basis and reference for the smoke alarm activation threshold or detector model,
- whether additional smoothing was applied to the prescribed mass curve prior to FDS input,
- sensitivity studies performed but not submitted,
- tenability assessment: criteria, thresholds, assessment heights and times to untenable conditions in F1, F2, FC and F3,
- use of AI tools in the modelling process,
- self-assessed confidence in quantitative outputs and tenability assessment,
- main influential and uncertain modelling choices from the participant’s perspective.

---

## 12. Recommended optional sensitivity analyses

The following sensitivity analyses are recommended but not mandatory:

| Sensitivity | Example |
|---|---|
| Mesh | Coarse / medium / fine |
| Soot yield | Lower / higher |
| Radiative fraction | Lower / higher |
| Leakage | None / estimated |
| Wall boundary conditions | Inert / thermally active |
| Fuel mass history implementation | Alternative HRR or MLRPUA implementations |

Sensitivity analyses shall not be used to select the “best” curve after the fact. The central comparison remains the pre-defined best-estimate prediction.

---

## 13. Preliminary schedule

| Phase | Description | Date / Deadline | Status |
|---|---|---|---|
| Preparation | Repository, data package and templates | — | Completed |
| Registration opens | Start of registration | from 2026-05-10 | Open |
| Registration deadline | Last day for registration | 2026-06-30 | Open |
| Kick-off | Introduction of scenario and rules | invitation after registration deadline | Open |
| Simulation phase | Work by participants | after kick-off – 2026-09-30 | Open |
| Question deadline | Last day for technical questions | 2026-09-15 | Open |
| Submission freeze | Freeze of all submissions | 2026-09-30 | Open |
| Stage 1 evaluation | Comparison with measurement data | tba | Open |
| Workshop | Discussion of anonymised results | tba | Open |
| Open calculation | Later stage with disclosed measurement data | tba | Planned |

---

## 14. Anonymisation, publication and authorship

Submissions are initially evaluated internally by the evaluation team. In reports and presentations, participant groups are anonymised, for example as:

```text
P01
P02
P03
```

If a scientific publication is prepared, active contributors may be invited as co-authors if they agree and meet the usual authorship criteria. Authorship and author order will be discussed transparently before submission.

Planned project outputs include:

- internal VIB report,
- workshop presentation,
- optional scientific publication,
- optional public benchmark data package after completion of the study.

Individual FDS files or detailed participant results will only be published after separate approval.

---

## 15. Questions and official answers

Questions shall be sent in writing to the project coordination:

```text
hasenheide@bcl-leipzig.de
```

Answers that are relevant to all participants will be published anonymously in:

```text
docs/faq.md
```

Only information documented in this repository or in an official release is binding.

---

## 16. Versioning

Participation shall be based on the official GitHub release:

```text
https://github.com/openbcl/fds-roundrobin-hasenheide
```

---

## 17. Contact

Project coordination:

```text
Manuel Osburg
Lukas Arnold

hasenheide@bcl-leipzig.de
```

---

## 18. Submission checklist

Before submission, please check:

- [ ] Best-estimate case is clearly identified.
- [ ] FDS 6.10.1 was used.
- [ ] FDS input file `*.fds` is included.
- [ ] FDS output file `*.out` is included.
- [ ] CSV result files `*.csv` are included.
- [ ] CSV columns correspond to the `DEVC` IDs defined in the FDS template.
- [ ] Additional files referenced by the FDS input are included.
- [ ] Additional quantities, sensor locations or derived indicators used for the tenability assessment are documented.
- [ ] No experimental target data were used.
- [ ] Archive follows the naming convention.
- [ ] Questionnaire is completed: `[TO BE ADDED: questionnaire link]`.
- [ ] Archive is sent to `hasenheide@bcl-leipzig.de`.

---

## 19. Short summary

Stage 1 of the VIB Hasenheide FDS Round-Robin Study is a semi-blind FDS prediction exercise for the compartment fire scenario `hep_160_150`. Participants receive a common scenario description, geometry, boundary conditions, measurement locations, averaged and smoothed fuel mass history and an FDS template. Experimental gas temperatures, optical extinction data and smoke alarm actuation times remain hidden until submission. Key modelling choices such as mesh resolution, fire source specification, soot yield, radiative fraction, leakage assumptions, wall boundary conditions, smoke alarm thresholds and tenability criteria remain open and must be documented. The aim is to quantify the variability of FDS predictions and identify dominant modelling influences for smoke transport, thermal conditions, optical extinction, smoke alarm actuation and tenability assessment.
