# Frequently Asked Questions – VIB Hasenheide FDS Round-Robin Study

Questions shall be sent in writing to the project coordination:

```text
hasenheide@bcl-leipzig.de
```

Answers that are relevant to all participants are published here anonymously.
Only information documented in this repository or in an official release is binding.

---

## Q1 – FDS version

**Q: Which FDS version should I use — and may I use a nightly (test) build?**

Use an official release — **FDS 6.11.0 or 6.11.1** — not a nightly or test build, so that results stay comparable. Version 6.11.1 is a bug-fix patch of 6.11.0 with no intended change to the physics; we **recommend 6.11.1**, because it corrects a wall-boundary interaction present in 6.11.0 (see Q13), and it is the version to use if your model is affected by that interaction. Please record the exact version you used in your questionnaire.

---

## Q2 – Sharing of submitted results

**Q: Will the submitted results be shared with the participants?**

During the evaluation, all submissions are compiled and compared in anonymised form. Each participant receives the anonymised comparison of all submissions — for example in the evaluation report — so that everyone can see how the predictions scatter relative to each other and to the experimental data. Identifiable single-participant results are not shared with other participants.

---

## Q3 – Other models (zone models, other CFD codes)

**Q: Can other models, such as zone models or other CFD codes, be used?**

No. Stage 1 is specifically an FDS intercomparison: the provided template, the prescribed `DEVC` outputs and the automated post-processing are tied to FDS, and comparability requires that all participants use FDS 6.11.0. Zone models or other CFD codes are therefore not part of this exercise. Whether a broader cross-code comparison is undertaken at a later stage remains open, but it is outside the scope of Stage 1.

---

## Q4 – Conditions for participation

**Q: Are there any specific conditions (organisational, financial, etc.) for taking part?**

No. Participation is voluntary and free of charge — there is no fee and no contract. The only requirements are to use FDS 6.11.0, to follow the submission format and to complete the questionnaire. Participation is open to anyone competent in fire modelling, whether in research or in engineering practice; registration is by email before the registration deadline. Each submission receives an anonymous participant ID, and all results are evaluated anonymously.

---

## Q5 – Participant IDs, submissions and runs

**Q: How do participant IDs, submissions and runs relate, and what if several people from one organisation take part?**

One participant ID corresponds to one submission, and a submission may contain several **runs** — for example a best estimate plus sensitivity variants — of which exactly one is marked as the `best_estimate`. Separate participant IDs are issued for **independent contributions**, i.e. teams or modellers working separately. Multiple independent contributions from the same organisation are welcome, each receiving its own anonymous ID.

---

## Q6 – Provision of the fuel mass-loss data

**Q: Can the individual replicate mass-loss curves be provided, not just the averaged curve?**

For Stage 1 a single averaged, smoothed and normalised mass-loss curve is prescribed, and the heat release rate or mass loss rate shall be derived from it. Prescribing one common fuel mass history is a deliberate scope decision: it removes fire-source/HRR-derivation variability (including the choice of smoothing method), so that Stage 1 isolates smoke transport, stratification, extinction, alarm actuation and tenability. The processing method is documented in `scenario/scenario_description.md` §6. The raw per-replicate data and the processing scripts will be released with the experimental data at Stage 2 (open calculation).

---

## Q7 – Point vs. path extinction

**Q: Why does the template use point extinction rather than a path-integrated (`PATH OBSCURATION`) device?**

The experimental transmissometers report a path-mean extinction (k = −ln τ / L). Integrating the FDS extinction field along the actual ~1 m optical paths and comparing it with the single-point value at the path centre shows the point value to be an essentially unbiased estimate of the path mean (median deviation −0.1 %, interquartile range [−0.9, +0.7] %, 95th percentile 5.7 % — within the experimental extinction uncertainty). Brief larger deviations occur only at lower heights in F2 when the descending smoke layer crosses the path, and are non-systematic. Point devices are therefore retained. (The field is integrated directly rather than via FDS `PATH OBSCURATION`, which currently truncates multi-mesh beams with descending endpoints — FDS issue #16338.)

---

## Q8 – Which area for MLRPUA / HRRPUA?

**Q: Should MLRPUA / HRRPUA be derived using the physical pan area (0.0256 m²) or the model surface area (0.0225 m²)?**

The model surface area. FDS releases the total rate as (area-specific rate) × (model surface area), and the template fire surface is 150 mm × 150 mm = 0.0225 m². To reproduce the prescribed (measured) total mass loss rate and heat release rate, compute MLRPUA/HRRPUA from the prescribed mass-loss curve and this 0.0225 m² model area. Using the physical pan area (0.0256 m²) with the 0.0225 m² model surface would under-release the total by about 12 %.

---

## Q9 – Walls, mesh boundaries and re-meshing

**Q: Not all walls are defined as `OBST`; some are represented by the mesh boundary. If I change the mesh, do the walls disappear?**

The observation is correct, and the template is intentionally built this way. Internal partitions between rooms are explicit `OBST` obstructions with doorways cut as `HOLE`, and the east walls and (closed) windows are `OBST`. The remaining envelope — the west and south perimeter, the floor, the ceiling, and the re-entrant corners of the L-shaped footprint — is formed by the external boundaries of the per-room meshes, which FDS treats as solid, no-flux walls by default. As shipped, the enclosure is complete.

The computational mesh is a participant choice. The single invariant to keep is that the **outer surface of your mesh system stays on the original wall planes** (the apartment footprint), so that the enclosed geometry — the four rooms, the three doorways, the closed windows and the footprint — is identical regardless of your mesh:

- **Refining the resolution** (`IJK`) on the same extents preserves every wall automatically.
- **Subdividing the meshes inside the footprint** is also safe: you may split a room into several meshes (for example for MPI) or embed refinement meshes; internal mesh-to-mesh interfaces are transparent and neither create nor remove walls, and `OBST` walls and door `HOLE`s are defined in absolute coordinates and survive any subdivision.
- **Changing the outer extent or footprint** (merging into one larger or padded box, extending the domain, or re-tiling so an outer face leaves a wall plane) removes the walls that those boundaries represented. In that case restore the envelope explicitly — keep mesh faces on the original wall planes, or add `OBST` walls and/or assign a boundary surface via `&VENT MB=...` — and verify the enclosure and footprint in Smokeview.

Note on wall properties: the template ships all surfaces as the FDS default (`INERT`); the wall construction and thermal boundary are yours to define. Internal partitions are `OBST` and take a `SURF_ID` directly, but the outer envelope is the domain boundary — to apply your chosen construction there you must assign it explicitly (`&VENT MB='XMIN' SURF_ID='...'`, etc.) or model those walls as `OBST`. Otherwise the perimeter remains default-inert even if your partition walls carry a construction.

---

## Q10 – Which walls are exterior, and is the building heated?

**Q: Which of the walls are exterior walls, and what temperature conditions apply between inside and outside?**

The test apartment *Fluppe* (F1, F2, F3, corridor FC) is one of three flats on this storey; the floor plan (`geometry/Floor_plan_overview.pdf`) shows the neighbouring apartments and the stairwell. Only the façade walls carrying the windows — the east/outer walls of F1, F2 and F3 — are **exterior** walls facing outdoor air. Every other wall of the apartment is **internal to the building**: the walls adjoining the neighbouring (equally vacant, unheated) apartments and the stairwell, and the partitions between the rooms within the apartment.

The building was **unheated** during the campaign, so inside and outside were in thermal equilibrium (**isothermal**); §7 records that room surfaces can be taken as essentially at the pre-test ambient temperature (~12 °C). For the pre-ventilation phase every wall therefore backs onto a space at about ambient temperature, with no heating-driven stack effect. The exterior-vs-interior distinction matters mainly for leakage paths (Q12) — leakage leaves the apartment both to the outdoors and into the adjoining building spaces — not for the initial thermal boundary.

---

## Q11 – What are the wall thicknesses?

**Q: Where do I find the wall thicknesses?**

They are dimensioned on the floor plan in the data package (`geometry/Floor_plan_overview.pdf` and the DXF drawings `geometry/*.dxf`). The wall `OBST` thicknesses in the FDS template are grid-snapped approximations of these dimensions (aligned to the 0.05 m reference grid). If you model heat conduction into the walls, note that the **thermal** thickness is a property of your wall surface/material definition and can be set to the architectural value independently of the `OBST` geometric thickness.

---

## Q12 – Building fabric and air leakage

**Q: Can you say more about the building fabric, to help estimate the air leakage?**

The construction is described in §4: solid clay-brick masonry (exterior walls and interior partitions alike; period construction, no stud/drywall), lime/gypsum plaster on the masonry, timber-beam floors and ceilings with slag-fill infill, plaster-on-reed ceiling soffit, linoleum over painted floorboards; double glazing (timber frames in F1/F2, PVC in F3), closed throughout. Two conditions bear on leakage: the building had been vacant for a prolonged period with no recent maintenance, and it is period solid-masonry construction. Envelope air leakage is therefore expected to be non-negligible but is **not quantified** in Stage 1 — its magnitude and representation (a pressure-zone leakage area, distributed leakage, or geometric openings) remain a modelling choice to justify in your questionnaire. Note that "leakage out of the apartment" includes paths both to the outdoors and into the adjoining building spaces.

---

## Q13 – Wall boundary condition with pressure-zone leakage (FDS 6.11.0)

**Q: Is there anything to watch for when combining leakage with a wall boundary condition?**

Yes. On FDS **6.11.0**, using the pressure-zone leakage model (`&ZONE` with `LEAK_AREA`) together with a **fixed-temperature wall surface** boundary condition silently disables that fixed-temperature boundary condition — the affected walls then do not behave as specified, and no warning is issued. This interaction was identified during the preparation of this study and is **fixed in FDS 6.11.1**.

Note that this includes the **default `INERT` surface**: `INERT` is itself a fixed-temperature boundary, held at the ambient temperature (`TMPA`). A model that uses pressure-zone leakage and simply leaves its walls at the default — without an explicitly defined conducting or adiabatic surface — is therefore also affected; the walls silently stop imposing the ambient temperature. This is easy to overlook precisely because no wall temperature was ever set by hand.

If your model combines pressure-zone leakage with a fixed-temperature wall surface — **including default `INERT` walls** — use **6.11.1** (permitted under Q1). Walls that solve heat conduction (material-based, thermally thick) or are explicitly adiabatic do not use a fixed-temperature boundary and are not affected by this interaction. In all cases, state the exact FDS version in your questionnaire.
