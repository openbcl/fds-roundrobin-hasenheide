# Frequently Asked Questions – VIB Hasenheide FDS Round-Robin Study

Questions shall be sent in writing to the project coordination:

```text
hasenheide@bcl-leipzig.de
```

Answers that are relevant to all participants are published here anonymously.
Only information documented in this repository or in an official release is binding.

---

## Q1 – FDS version

**Q: Can I use the latest nightly build (test version) of FDS 6.11.0?**

No. Only the official release version of FDS 6.11.0 shall be used. This ensures comparability of results across all submissions.

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
