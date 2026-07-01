# VIB Hasenheide FDS Round-Robin Study – Stage 1
# Modelling Questionnaire

**Participant ID:** ___________  
**Run ID:** ___________  
**Date of submission:** ___________

Please complete this questionnaire for each submitted run. All answers are treated
anonymously. The questionnaire is a mandatory part of the submission.

---

## Section 1 – General

**1.1** Did you perform this simulation as part of a team or individually?

- [ ] Individually
- [ ] Team (number of persons involved: ___)

**1.2** Professional background (tick all that apply):

- [ ] Research / academia
- [ ] Engineering practice / consulting
- [ ] Authority / approval body
- [ ] Education / teaching
- [ ] Other: ___________

**1.3** Years of regular FDS use:

___________

**1.4** Hardware used for this simulation (e.g. number of CPU cores / MPI processes, RAM, workstation / cluster / cloud):

___________

**1.5** Self-assessed FDS proficiency (1 = basic, 5 = expert):

___________

---

## Section 2 – Justifications for Key Modelling Choices

**2.1** Why did you choose this particular C7 surrogate fuel and &REAC specification?
Briefly justify your choice:

___________

**2.1a** For the following combustion parameters, state the value used and its primary
source. Use the source codes below:

*(A) Published experimental data — (B) Handbook or reference value — (C) FDS
default — (D) Own calculation or estimation — (E) Engineering judgement — (F) Other*

| Parameter | Value used | Source code | Reference / comment |
|---|---|---|---|
| Soot yield [kg/kg] | | | |
| CO yield [kg/kg] | | | |
| Radiative fraction [—] | | | |
| Heat of combustion (`HEAT_OF_COMBUSTION`) [kJ/kg] | | | |
| Mass-specific extinction coefficient [m²/kg] | | | |

**2.2** Why did you choose this mesh resolution? What D*/dx ratio did you target near
the fire source, and what guided this choice?

___________

Did you perform a mesh-independence check?

- [ ] Yes
- [ ] No

**2.3** Why did you choose this wall boundary condition approach (inert / adiabatic /
thermally active)? Provide reference(s) for material properties if applicable:

___________

**2.4** Did you model air leakage? Why or why not, and what was the basis for your
approach?

___________

**2.5** What was the basis for your smoke alarm activation threshold or detector model?
Provide reference(s):

___________

**2.6** Was additional smoothing applied to the prescribed mass curve before deriving
MLRPUA or HRRPUA (i.e. outside of FDS, prior to input)?

- [ ] No
- [ ] Yes — describe method: ___________

---

## Section 3 – Sensitivity Studies

**3.1** Were sensitivity studies performed that are not part of this submission?

- [ ] No
- [ ] Yes — describe what was varied and the main finding:

___________

**3.2** *If applicable (sensitivity run only):* Describe what differs from the
best-estimate run and why:

___________

---

## Section 4 – Tenability Assessment

**4.1** Did you assess tenability (escape impairment and/or incapacitation) based on
your simulation results?

- [ ] Yes
- [ ] No — proceed to Section 5

**4.2** Which criteria and threshold values did you apply? State the height above
floor level (AFF) at which each criterion was evaluated. Provide reference(s):

| Criterion | Threshold | Height AFF [m] | Reference |
|---|---|---|---|
| Smoke layer height | min. ___ m | — | |
| Visibility | ___ m | | |
| Temperature | ___ °C | | |
| Thermal radiation | ___ kW/m² | — | |
| CO concentration | ___ ppm | | |
| CO₂ concentration | ___ % | | |
| O₂ concentration | ___ % | | |
| FED / FEC (ISO 13571) | ___ | | |
| Other: | | | |

**4.3** Based on your simulation, at what time does each room become untenable?
State the limiting criterion. Enter "not reached" if conditions remain tenable
throughout T_END = 1200 s.

| Location | Time [s] | Limiting criterion |
|---|---|---|
| F1 (fire room) | | |
| F2 | | |
| FC (corridor) | | |
| F3 | | |

**4.4** Overall assessment: for which rooms does your simulation suggest that escape
would still be possible at the end of the pre-ventilation phase (t = 1200 s)?

___________

**4.5** Any remarks on the tenability assessment (e.g. assumptions on occupant
location, escape route, post-burnout recovery):

___________

---

## Section 5 – Self-Assessment and Comments

**5.1** How confident are you in your simulation results? (1 = low, 5 = high)

Overall: ___  
Quantitative outputs (temperature, extinction, alarm times): ___  
Tenability assessment: ___

**5.2** Which modelling choice do you consider most influential for your results,
and which is most uncertain?

Most influential: ___________  
Most uncertain: ___________

**5.3** Did you use AI tools (e.g. large language models, AI-assisted coding) in
preparing your submission? If yes, for what purpose?

- [ ] No
- [ ] Yes — describe: ___________

**5.4** Any known issues, limitations, or comments on your submission:

___________

**5.5** Co-authorship: active contributors may be invited as co-authors of a
subsequent scientific publication, subject to the usual authorship criteria.

- [ ] I am, in principle, willing to be named as a co-author.
- [ ] I prefer to decline co-authorship / remain anonymous.

*(Name and affiliation for authorship are handled via the registration contact, so this questionnaire itself remains anonymous.)*
