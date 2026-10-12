# Isath — NASA Space Apps 2026 Preparation Checklist

## Team: Periapsis

### Challenge
**Interplanetary Survival Guide: Martian Map**

### Primary Role
**Planetary Science & Product Research Lead**

### Core Mission

Make sure Periapsis:

- solves the actual NASA challenge
- uses NASA data meaningfully rather than decoratively
- makes scientifically defensible claims
- understands what every important dataset actually represents
- chooses useful information for a human Mars explorer
- clearly distinguishes facts, measurements, derived values, assumptions and predictions
- can defend its scientific/product decisions to judges
- tells a clear story about why the product matters

You are **not expected to be the main GIS implementation, backend architecture or routing-algorithm engineer**.

You should, however, understand those systems well enough to challenge bad assumptions and explain why the inputs and outputs make scientific sense.

---

# PRIORITY SYSTEM

- **P0 — Essential:** Must know before the hackathon.
- **P1 — Important:** Strongly recommended.
- **P2 — Useful:** Learn if time permits.

---

# P0 — ESSENTIAL

## 1. Understand the Challenge Properly

- [ ] Read the complete official **Interplanetary Survival Guide: Martian Map** challenge brief.
- [ ] Be able to explain the challenge in **30 seconds without reading it**.
- [ ] Identify:
  - [ ] primary user
  - [ ] problem being solved
  - [ ] required output
  - [ ] role of NASA data
  - [ ] scientific component
  - [ ] exploration/safety component
- [ ] Understand the difference between:
  - [ ] a Mars map
  - [ ] a scientific visualization
  - [ ] a route planner
  - [ ] a decision-support tool
- [ ] Be able to explain why simply putting NASA layers on a map would be insufficient.
- [ ] Identify which parts of our eventual idea come from:
  - [ ] the official challenge
  - [ ] NASA data
  - [ ] our own assumptions
  - [ ] our own product design

### Practice

Write a one-page breakdown:

**Problem → User → Data → Processing → Insight → Decision → Action → Outcome**

Do this without designing the final solution in advance.

---

# 2. Mars Surface & Planetary Science Fundamentals

You do not need a planetary-science degree. NASA has inconveniently declined to postpone Mars exploration until we finish university.

You **do** need enough knowledge to interpret terrain and environmental information correctly.

## Mars Fundamentals

- [ ] Basic physical properties of Mars:
  - [ ] gravity
  - [ ] atmosphere
  - [ ] atmospheric pressure
  - [ ] temperature environment
  - [ ] day/sol
  - [ ] seasons
- [ ] Understand major Martian surface features:
  - [ ] craters
  - [ ] plains
  - [ ] dunes
  - [ ] ridges
  - [ ] valleys/channels
  - [ ] cliffs/escarpments
  - [ ] volcanic terrain
  - [ ] sedimentary terrain
- [ ] Understand basic Martian regolith.
- [ ] Understand why terrain morphology matters for exploration.
- [ ] Understand the relationship between:
  - [ ] elevation
  - [ ] slope
  - [ ] roughness
  - [ ] traversability

## Environmental Factors

Understand at a conceptual level:

- [ ] surface temperature
- [ ] atmospheric conditions
- [ ] dust
- [ ] solar illumination
- [ ] radiation exposure
- [ ] terrain hazards
- [ ] visibility
- [ ] thermal conditions

You do **not** need to model all of these.

The important skill is deciding:

> "Do we actually have appropriate data for this variable, and does it matter to our user?"

---

# 3. Planetary Mapping Fundamentals

Abhi/Senula may handle more of the actual GIS and routing implementation.

You still need enough geospatial knowledge to understand what their data means.

Learn:

- [ ] latitude and longitude on Mars
- [ ] longitude conventions:
  - [ ] 0–360°
  - [ ] -180° to +180°
- [ ] basic difference between:
  - [ ] planetocentric coordinates
  - [ ] planetographic coordinates
- [ ] coordinate reference systems
- [ ] map projections
- [ ] why projection choice can distort:
  - [ ] distance
  - [ ] area
  - [ ] shape
- [ ] raster data
- [ ] vector data
- [ ] Digital Elevation Models — DEMs
- [ ] spatial resolution
- [ ] spatial extent
- [ ] pixels/cells
- [ ] interpolation/resampling
- [ ] map layers

### You should be able to answer:

> "What does one pixel in this dataset represent?"

> "What coordinate system is this using?"

> "Can we safely compare this layer with another layer?"

> "Is this resolution sufficient for the claim we're making?"

---

# 4. Learn the Important NASA Mars Data Sources

You don't need to memorize NASA's entire data archive. That would be a fairly depressing use of October.

You need to know the major datasets relevant to our challenge.

---

## MOLA — Mars Orbiter Laser Altimeter

Learn:

- [ ] what MOLA measured
- [ ] elevation/topography
- [ ] what a MOLA DEM represents
- [ ] spatial resolution
- [ ] units
- [ ] limitations
- [ ] how elevation can produce:
  - [ ] slope
  - [ ] terrain profiles
  - [ ] terrain difficulty information

Know when MOLA is appropriate and when higher-resolution terrain data is required.

---

## CTX — Context Camera

Learn:

- [ ] what CTX imagery shows
- [ ] approximate scale/resolution
- [ ] why it is useful for regional terrain context
- [ ] difference between imagery and elevation data
- [ ] relationship between CTX imagery and CTX-derived DEMs

---

## HiRISE

Learn:

- [ ] what HiRISE imagery provides
- [ ] why its resolution is valuable
- [ ] what kinds of small-scale terrain features can become visible
- [ ] difference between:
  - [ ] HiRISE images
  - [ ] HiRISE-derived DEMs
- [ ] limitations of coverage

---

## THEMIS

Learn:

- [ ] basic purpose of THEMIS
- [ ] thermal infrared observations
- [ ] thermal properties of terrain
- [ ] concept of thermal inertia
- [ ] why thermal information may matter to surface interpretation

---

## NASA Planetary Data System — PDS

This is especially important.

- [ ] Understand what NASA PDS is.
- [ ] Learn how datasets are organised.
- [ ] Learn how to inspect:
  - [ ] metadata
  - [ ] instrument information
  - [ ] units
  - [ ] timestamps
  - [ ] coordinate information
  - [ ] documentation
- [ ] Understand that downloading a NASA file does **not automatically mean you understand what it contains**.

NASA PDS includes products such as CTX/HiRISE-derived elevation models, including DEMs distributed in geospatial formats such as GeoTIFF.

---

# 5. NASA Dataset Evaluation

For **every dataset we seriously consider**, be able to fill this out:

## Dataset Evaluation Template

### Dataset
`Name:`

### Mission
`Mission / spacecraft:`

### Instrument
`Instrument:`

### Measurement
`What was actually measured?`

### Units
`Units:`

### Spatial Resolution
`Resolution:`

### Temporal Resolution
`Temporal characteristics:`

### Geographic Coverage
`Coverage:`

### Missing Data
`Missing regions / gaps:`

### Processing
`Raw observation / processed product / derived product:`

### Uncertainty
`Known uncertainty / precision:`

### Intended Use
`How could this help a Mars explorer?`

### Limitations
`What can we NOT conclude from this dataset?`

### Product Relevance
`Why should this layer exist in our product?`

---

# 6. Scientific Data Reasoning

Learn the distinction between:

- [ ] observed variable
- [ ] derived variable
- [ ] proxy
- [ ] assumption
- [ ] model output
- [ ] prediction
- [ ] recommendation

### Example

**Observed / dataset value**

Elevation.

↓

**Derived**

Slope.

↓

**Model**

Terrain difficulty score.

↓

**Product output**

Suggested route.

These are **not the same type of information**.

Be able to trace a recommendation backwards:

> recommendation → model → derived variables → NASA observations

---

# 7. Uncertainty & Scientific Honesty

One of your biggest responsibilities.

Learn how to recognise:

- [ ] measurement uncertainty
- [ ] limited spatial resolution
- [ ] temporal mismatch
- [ ] incomplete coverage
- [ ] missing data
- [ ] outdated observations
- [ ] assumptions
- [ ] uncertain classifications
- [ ] extrapolation

Be able to stop the team from saying:

> "This route is safe."

when what our evidence actually supports is:

> "This route has a lower estimated terrain-risk score under these assumptions."

That distinction matters.

---

# 8. Marswalk / EVA Operational Thinking

Understand the problem from the explorer's perspective.

Imagine an astronaut preparing for a Marswalk.

Questions to understand:

- [ ] Where am I going?
- [ ] Why am I going there?
- [ ] How far is it?
- [ ] How difficult is the terrain?
- [ ] What hazards exist?
- [ ] What scientifically interesting locations exist?
- [ ] What route alternatives exist?
- [ ] What environmental conditions matter?
- [ ] What information should be visible before departure?
- [ ] What information matters during the Marswalk?
- [ ] What information is irrelevant noise?

Understand the distinction between:

### Pre-Marswalk Planning

- route selection
- destination comparison
- hazard inspection
- science-target selection

### During Marswalk

- navigation
- warnings
- location context
- nearby science targets
- changing conditions

---

# 9. Scientific Value vs Operational Safety

A good exploration route may involve trade-offs.

Understand concepts such as:

**Safest Route**

vs

**Shortest Route**

vs

**Most Scientifically Valuable Route**

vs

**Balanced Route**

Learn how multi-objective decisions work conceptually.

You should understand:

- [ ] weighted scoring
- [ ] normalized variables
- [ ] thresholds
- [ ] hard constraints
- [ ] soft preferences
- [ ] trade-offs

You do NOT need to become the primary pathfinding programmer.

You DO need to be able to challenge statements like:

> "Science value should have weight 0.8."

with:

> "Why 0.8?"

---

# 10. Scientific Model Validation

Understand how we can determine whether our system makes sense.

Learn:

- [ ] sanity checks
- [ ] extreme-case tests
- [ ] sensitivity analysis
- [ ] comparison against known terrain
- [ ] parameter testing
- [ ] uncertainty analysis

### Example Sensitivity Test

If:

`Terrain Risk = 0.5 × slope + 0.3 × roughness + 0.2 × another variable`

ask:

- What happens if slope weight becomes 0.3?
- Does the recommended route change dramatically?
- Why were these weights selected?
- Are units normalized?
- Does the model behave sensibly at extreme values?

---

# 11. Research Skills

You will probably be doing more scientific research during the hackathon than almost anyone else.

Learn to research FAST without becoming sloppy.

## Source Priority

Use roughly this hierarchy:

1. NASA
2. NASA Planetary Data System
3. JPL
4. USGS Astrogeology
5. ESA / recognised space-agency partners
6. peer-reviewed scientific literature
7. reputable university/research sources
8. secondary explanations

Avoid treating random blogs as scientific evidence merely because Google placed them first. Humanity already has enough problems.

---

## Research Workflow

For each question:

- [ ] Write the exact question.
- [ ] Find an authoritative source.
- [ ] Record the claim.
- [ ] Record the source.
- [ ] Record important numbers/units.
- [ ] Record assumptions.
- [ ] Record uncertainties.
- [ ] Record whether it affects our product.

---

# 12. Citation & Evidence Management

During the hackathon we should not be searching through 37 browser tabs trying to remember where one elevation number came from.

Maintain something like:

| Claim | Source | Dataset | Confidence | Used Where |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

Learn to keep track of:

- [ ] dataset name
- [ ] mission
- [ ] instrument
- [ ] NASA/PDS source
- [ ] scientific references
- [ ] important limitations

---

# 13. Product Thinking

Your role includes **Product Research**, not just science.

For every proposed feature ask:

### User

Who needs this?

### Problem

What difficulty does it solve?

### Data

What information powers it?

### Decision

What decision becomes easier?

### Action

What can the astronaut do differently?

### NASA Necessity

Why is NASA data required?

### Demo

Can we demonstrate the value clearly?

---

# 14. Feature Filtering

Learn to classify features as:

## Must Have

Required for the product's core workflow.

## High-Value Differentiator

Makes Periapsis meaningfully better.

## Stretch Feature

Useful only if the core system works.

## Distraction

Sounds cool but doesn't improve the challenge solution.

You should actively attack distractions.

---

# 15. Product/Science Critique

Practice asking uncomfortable questions.

For every major feature:

- [ ] Is this actually required?
- [ ] Is the science correct?
- [ ] Do we have data for this?
- [ ] Is the data resolution sufficient?
- [ ] Is the data current enough?
- [ ] Is this directly measured or inferred?
- [ ] Are we overstating accuracy?
- [ ] Does an astronaut actually care?
- [ ] Why does this improve a Marswalk?
- [ ] Can judges understand this quickly?
- [ ] Could we demonstrate this reliably?

---

# P1 — IMPORTANT

# 16. Remote Sensing Fundamentals

Learn basic concepts:

- [ ] passive vs active remote sensing
- [ ] visible imagery
- [ ] infrared imagery
- [ ] thermal infrared
- [ ] radar
- [ ] lidar/laser altimetry
- [ ] spatial resolution
- [ ] spectral resolution
- [ ] temporal resolution

Be able to explain why different instruments tell us different things about Mars.

---

# 17. Martian Geology

Develop basic recognition of:

- [ ] impact geology
- [ ] volcanic terrain
- [ ] sedimentary structures
- [ ] erosional features
- [ ] dunes
- [ ] channels
- [ ] layered deposits
- [ ] fractured terrain

Understand why certain locations may have greater scientific interest than others.

You do NOT need professional geological classification skills.

---

# 18. Scientific Points of Interest

Learn how scientists identify potentially interesting locations.

Think about:

- geology
- morphology
- mineralogy
- stratigraphy
- possible past-water evidence
- unusual terrain features

Understand the difference between:

> "interesting-looking terrain"

and

> "scientifically motivated exploration target"

---

# 19. Human Factors & Information Design

A Mars map can contain twenty layers and still be terrible.

Learn basic principles of:

- [ ] information hierarchy
- [ ] cognitive load
- [ ] alert prioritisation
- [ ] map legends
- [ ] meaningful colour scales
- [ ] uncertainty visualisation
- [ ] progressive disclosure
- [ ] context-dependent information

Think:

> What does the explorer need **right now**?

not:

> How many NASA datasets can we fit on the screen before the laptop catches fire?

---

# 20. Data Visualization

Learn how to choose appropriate visualisations for:

- [ ] terrain
- [ ] elevation
- [ ] slope
- [ ] risk
- [ ] scientific interest
- [ ] environmental variables
- [ ] uncertainty
- [ ] route comparison

Understand:

- continuous vs categorical data
- misleading colour scales
- legends
- normalization
- map overlays
- opacity
- visual clutter

---

# 21. Basic Data Analysis in Python

You should be comfortable enough to independently inspect scientific data.

Learn/review:

- [ ] Python
- [ ] NumPy
- [ ] Pandas
- [ ] Matplotlib
- [ ] basic statistics

Be able to:

- [ ] open a dataset
- [ ] inspect rows/arrays
- [ ] inspect metadata
- [ ] calculate basic statistics
- [ ] detect missing values
- [ ] produce a plot
- [ ] compare variables

---

# 22. Git / GitHub Team Workflow

Know enough Git to contribute independently.

- [ ] clone
- [ ] branch
- [ ] pull
- [ ] commit
- [ ] push
- [ ] resolve simple conflicts
- [ ] create/read pull requests
- [ ] inspect changes

Your research/data contributions should also end up in the team's shared repository/documentation rather than living exclusively in your browser history.

---

# 23. API / Data Pipeline Literacy

You don't need to own backend architecture.

Understand:

`NASA Dataset → Download/API → Processing → Derived Data → Backend/API → Frontend Map`

Be able to identify where:

- units change
- coordinates change
- values are normalized
- values are derived
- assumptions enter the system

---

# 24. Presentation & Judge Communication

This is one of your stronger areas, so make it dangerous.

Practice explaining:

### In 15 seconds

What problem are we solving?

### In 30 seconds

Why NASA data is necessary.

### In 60 seconds

How the science works.

### In 2 minutes

How the full product helps an astronaut.

---

Be ready for questions like:

- Why did you choose these datasets?
- Why this location?
- Why these variables?
- How accurate is this?
- How recent is this data?
- What happens where data is missing?
- How did you calculate risk?
- Why these weights?
- Is this NASA data or something you generated?
- Could an astronaut actually use this?
- What is scientifically novel or useful here?
- What are the biggest limitations?

---

# P2 — USEFUL IF TIME ALLOWS

## 25. Additional Mars Missions / Instruments

Become generally familiar with useful Mars missions and instruments such as:

- [ ] Mars Global Surveyor
- [ ] Mars Reconnaissance Orbiter
- [ ] Mars Odyssey
- [ ] Mars Science Laboratory / Curiosity
- [ ] Mars 2020 / Perseverance

Potential instruments/datasets worth recognising:

- [ ] MOLA
- [ ] CTX
- [ ] HiRISE
- [ ] THEMIS
- [ ] MARCI
- [ ] MCS
- [ ] SHARAD
- [ ] MEDA
- [ ] REMS

You don't need detailed knowledge of all of these.

The goal is to know **where to look** if the product suddenly requires a particular variable.

---

# 26. Mars Mission Operations

Learn conceptually about:

- [ ] EVA planning
- [ ] traverse planning
- [ ] mission objectives
- [ ] science targets
- [ ] time constraints
- [ ] energy/resource constraints
- [ ] communication constraints
- [ ] contingency planning

Focus on how these create **product requirements**.

---

# REQUIRED PRACTICE EXERCISES

These matter more than watching another twelve YouTube videos while feeling academically productive.

---

# Exercise 1 — Dataset Investigation

Choose **one NASA Mars dataset**.

Produce a maximum two-page briefing containing:

- [ ] mission
- [ ] instrument
- [ ] measurement
- [ ] units
- [ ] resolution
- [ ] coverage
- [ ] file format
- [ ] uncertainty
- [ ] limitations
- [ ] possible Marswalk use
- [ ] at least one visualization

### Pass Condition

Someone else on the team should be able to understand whether we should use the dataset after reading your briefing.

---

# Exercise 2 — Compare Three Mars Datasets

Compare:

- MOLA
- CTX or HiRISE
- THEMIS

Create:

| Property | MOLA | CTX/HiRISE | THEMIS |
|---|---|---|---|
| Instrument type | | | |
| Measures | | | |
| Resolution | | | |
| Main use | | | |
| Limitation | | | |
| Marswalk relevance | | | |

Then explain how combining them can provide more information than any one dataset alone.

---

# Exercise 3 — Marswalk Decision Exercise

Pick a hypothetical Martian location.

Assume an astronaut must reach a scientific target.

Identify at least:

- [ ] 3 operational factors
- [ ] 2 science-value factors
- [ ] 2 relevant NASA datasets
- [ ] 2 uncertainties
- [ ] 1 major trade-off

Then explain how a decision-support map could help.

Do NOT build the final competition solution.

---

# Exercise 4 — Scientific Claim Audit

Take a hypothetical statement:

> "Route A is the safest route for the astronaut."

Break it down.

Ask:

- What evidence would be required?
- What variables define "safe"?
- What data measures those variables?
- What is derived?
- What assumptions are required?
- What uncertainty remains?
- What wording would be scientifically defensible?

---

# Exercise 5 — Dataset Failure Scenario

Imagine one important dataset:

- has missing pixels
- has lower resolution than expected
- uses different coordinates
- is unavailable during the hackathon

Explain:

1. what breaks
2. what remains usable
3. what fallback data could be used
4. how the limitation should be communicated

---

# Exercise 6 — Five-Minute Judge Defense

Prepare a five-minute explanation covering:

1. Challenge
2. User
3. Scientific problem
4. NASA datasets
5. Why multiple missions are combined
6. How raw data becomes useful information
7. Major assumptions
8. Major limitations
9. User decision enabled
10. Why our approach is useful

Then have Abhi attack it with judge questions.

If an answer becomes:

> "I think..."

go back and find evidence.

---

# EXERCISE 7 — Live Dataset Trial

Time limit: **90 minutes**

You are given an unfamiliar NASA planetary dataset.

Within the time limit:

- [ ] identify the mission/instrument
- [ ] determine what is measured
- [ ] find units
- [ ] determine spatial/temporal characteristics
- [ ] identify at least 2 limitations
- [ ] identify at least 2 possible uses
- [ ] determine whether it is useful for our challenge
- [ ] create one visualization if practical
- [ ] provide authoritative sources
- [ ] give a 3-minute verbal briefing

### Target

**80/100 minimum**

This tests whether you can research under actual hackathon pressure rather than only after three evenings of preparation.

---

# PRE-HACKATHON DELIVERABLES

By November 14, you should have:

- [ ] Strong understanding of the Martian Map challenge
- [ ] Basic Mars planetary-science knowledge
- [ ] Basic planetary GIS literacy
- [ ] Familiarity with MOLA
- [ ] Familiarity with CTX
- [ ] Familiarity with HiRISE
- [ ] Familiarity with THEMIS
- [ ] Familiarity with NASA PDS
- [ ] Ability to evaluate a new dataset quickly
- [ ] Ability to inspect metadata correctly
- [ ] Ability to distinguish observed/derived/assumed information
- [ ] Understanding of uncertainty
- [ ] Understanding of Marswalk user needs
- [ ] Understanding of scientific vs operational trade-offs
- [ ] Basic model-validation knowledge
- [ ] Basic Python scientific-data analysis ability
- [ ] Reliable Git/GitHub workflow
- [ ] Good research/citation workflow
- [ ] Ability to explain NASA-data choices to judges
- [ ] Ability to challenge scientifically weak product ideas
- [ ] Completion of the dataset trial

---

# DEFINITION OF READY

Isath is hackathon-ready when he can be given an unfamiliar proposed feature such as:

> "Use this NASA layer to warn astronauts about dangerous terrain."

and independently determine:

1. **What dataset should we use?**
2. **What does it actually measure?**
3. **What are its units and resolution?**
4. **What processing would be required?**
5. **What can legitimately be derived from it?**
6. **What assumptions would we introduce?**
7. **How uncertain is the result?**
8. **Does an astronaut actually need this information?**
9. **How should the information appear in the product?**
10. **Can we defend the decision to a NASA Space Apps judge?**

The goal is not for Isath to know every fact about Mars.

The goal is for him to be able to rapidly turn:

**NASA science → trustworthy interpretation → product requirement → defensible decision.**