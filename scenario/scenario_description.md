# Scenario Description – hep_160_150

## 1. Overview

In December 2025, a series of full-scale compartment fire experiments were conducted in a vacant residential building in Leipzig, Germany. The building, referred to as *Hasenheide*, is a two-storey structure with a basement and an attic.

Experiments were carried out on the first floor in an unfurnished apartment referred to as *Fluppe*. The present scenario (`hep_160_150`) is based on a subset of these experiments involving liquid pool fires using a commercial C7 hydrocarbon fuel.

The purpose of the experiments was to generate reproducible fire conditions in a realistic residential geometry, enabling the study of smoke transport, thermal conditions, optical extinction and smoke alarm actuation.

## 2. Compartment geometry and layout

The test apartment consisted of three interconnected rooms and a corridor:

- **F1:** fire compartment  
- **F2:** adjacent room  
- **F3:** secondary adjacent room  
- **FC:** corridor  

The total net floor area of the connected spaces was approximately 50.67 m².  
The clear room height ranged between 2.52 m and 2.54 m.

All internal doors were removed. The doorway to the stairwell was sealed with a plastic-sheet door.

Each room (F1, F2, F3) had one window. All windows remained closed during the pre-ventilation phase.

## 3. Ventilation conditions

### 3.1 Pre-ventilation phase

- All windows closed  
- No mechanical ventilation  
- Background leakage only  
- Undisturbed fire development  

Duration: 20 minutes

### 3.2 Post-ventilation phase (not part of Stage 1)

- Windows in F1 and F3 opened  
- Cross-ventilation using fan  
- Operator entry with SCBA  

## 4. Building construction

- Walls: clay brick masonry  
- Floors/ceilings: timber beam construction  
- Intermediate layers: slag fill  
- Ceiling underside: timber + plaster  
- Floor finish: timber + linoleum  

Air leakage is expected but not quantified.

## 5. Fire source

### 5.1 Fuel

The fuel used in this scenario was a commercial C7-UVCB hydrocarbon mixture labelled “Heptan”.

Approximate composition of the delivered batch:

- n-heptane: approximately 35.8 wt.%
- methylcyclohexane: approximately 22.9 wt.%
- aromatic content: very low

The fuel should therefore not be interpreted as chemically pure n-heptane. For FDS modelling, participants shall define an appropriate C7 surrogate fuel or reaction model and document their choice in the questionnaire.

### 5.2 Burner

The fire source consisted of a square steel pan located at the centre of room F1.

```text
Pan size:          160 mm × 160 mm
Pan depth:         100 mm
Initial fuel mass: 150 g
Fuel area:         0.0256 m²
```

The FDS template approximates the pan as 150 mm × 150 mm (0.0225 m²) with coordinates snapped to multiples of 0.05 m, compatible with mesh cell sizes that are multiples or fractions of 5 cm. When deriving MLRPUA or HRRPUA from the prescribed fuel mass history, participants shall use the actual fuel area of **0.0256 m²**, not the model geometry.

Ignition was performed manually. Ignition defines:

```text
t = 0 s
```

Immediately after ignition, the operator left the apartment and closed the plastic-sheet door.

## 6. Fuel mass history

The scenario `hep_160_150` is based on three replicate tests:

```text
Hep_160_S1_R1
Hep_160_S1_R2
Hep_160_S1_R3
```

Participants receive a single averaged and smoothed fuel mass curve derived from these replicates.

The fuel mass history is prescribed as input data. Its implementation in FDS, for example as a prescribed heat release rate or as a mass loss rate, is part of the modelling choice and must be documented.

When deriving the mass loss rate per unit area (MLRPUA) or heat release rate per unit area (HRRPUA) by numerical differentiation, participants should verify that the resulting rate curve is free of numerical artefacts. Additional smoothing of the derived rate may be appropriate.

## 7. Initial ambient conditions

The pre-test ambient conditions were measured in room F2 before each experiment.

For the three replicates of `hep_160_150`, the following values were recorded:

| Run | Air temperature [°C] | Relative humidity [%] | Barometric pressure [hPa] |
|---|---:|---:|---:|
| Hep_160_S1_R1 | 11.40 | 69.02 | 993.80 |
| Hep_160_S1_R2 | 12.71 | 70.70 | 993.12 |
| Hep_160_S1_R3 | 12.30 | 79.81 | 992.15 |
| **Mean** | **12.1** | **73.2** | **993.0** |

## 8. Instrumentation

### 8.1 Temperature

Thermocouples were installed in F1, F2 and F3 at the following heights above floor level:

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

An additional thermocouple was installed at ceiling level above the fire in F1.

### 8.2 Optical measurements

Light-extinction measurements were installed at defined locations in the apartment. The relevant optical measurement locations for this scenario are provided in the FDS template and associated measurement-location files.

### 8.3 Smoke alarms

Optical smoke alarms were installed at ceiling level in:

- F2
- FC
- F3

Smoke alarm actuation times were recorded experimentally.

### 8.4 Data acquisition

Experimental data were recorded using a time-synchronised multi-channel data acquisition system.

```text
Sampling rate: 1 Hz
```

## 9. Notes for modelling

Participants should consider the following points when setting up their CFD simulations:

- The geometry represents a real residential building with non-ideal boundaries.
- Air leakage is expected but not quantified.
- The fire source is represented through the prescribed fuel mass history.
- Combustion is expected to be predominantly well-ventilated during the pre-ventilation phase.
- The scenario produces moderate smoke concentrations suitable for optical analysis.
- Smoke alarm actuation thresholds are not prescribed and must be selected, justified and documented by the participants.

The provided data define a common baseline, while key engineering modelling assumptions remain intentionally open.
