# Greywater Irrigation and Seed Germination: A Randomized Experiment

Practicum experiment for **Experimental Research: Design, Analysis, and Interpretation** (GU4724), Columbia University, Fall 2026.

**Author:** Xingyi Wang
**Status:** Main experiment running. Planted on the night of October 12, 2026 (Day 0); final measurement on Day 7 (October 19, 2026).
**Last updated:** October 18, 2026

> Items marked **TODO** are details still to be filled in or confirmed. This README is a running log: it records what was planned, what was actually done, and every change made along the way.

---

## 1. Research question

**Does irrigating with simulated household greywater reduce the germination and early growth of crops that Syrian refugees grow in camp gardens, compared with tap water?**

### Motivation

Syrian refugees in Jordan's Zaatari camp grow herbs, tomatoes and cucumbers despite limited water and poor desert soil ([InfoMigrants](https://www.infomigrants.net/en/post/26724/these-refugees-are-growing-vegetables-in-the-desert)). Because water is scarce, some camp gardens irrigate with greywater, household wastewater excluding toilet sewage, as in Domiz camp in northern Iraq ([NPR](https://www.npr.org/sections/thesalt/2018/02/22/587708405/community-and-vegetables-grow-side-by-side-in-syrian-refugee-camp-gardens)). Greywater contains detergents and salts that may harm young plants. This experiment tests whether that harm occurs at the seed and seedling stage.

### Why an experiment

Comparing real gardens that do and do not use greywater would be confounded: households that reuse greywater may face tighter water rations, poorer soil or different crops. Randomly assigning water type to otherwise identical containers isolates its causal effect.

The study involves **no human subjects**. Units are seed containers, and all outcomes are physical measurements.

---

## 2. Design summary

| Element | Choice |
| --- | --- |
| Units | 48 containers, 10 seeds each (480 seeds) |
| Crops (blocks) | Cucumber (containers 1–24) and molokhia (containers 25–48) |
| Treatments | 5 arms: tap water, dish soap at 10 and 20 mL/L, laundry detergent at 10 and 20 mL/L |
| Allocation per crop | 8 tap water, 4 per detergent arm |
| Assignment | Complete random assignment within each crop (block randomization) |
| Co-primary outcomes | Germination share and mean hypocotyl length, both on Day 7 (see Amendment 1 in `prereg.md`) |
| Inference | Randomization inference, 10,000 simulated assignments |
| Deviations | Logged; intention-to-treat analysis |

---

## 3. Materials

| Item | Details |
| --- | --- |
| Cucumber seeds | **TODO:** variety, seller, lot number, packed-for year |
| Molokhia seeds | Egyptian spinach / jute mallow (*Corchorus olitorius*). **TODO:** seller, lot number |
| Containers | 50 identical clear plastic containers with lids. **TODO:** size |
| Growing medium | Paper towels. **TODO:** brand; how each was folded |
| Dish soap | **TODO:** brand and product name |
| Laundry detergent | **TODO:** brand and product name |
| Measuring tools | 10 mL syringe, ruler (mm), bottles for solutions |
| Water | Tap water |

No fertilizer was used. Seeds contain enough stored nutrients for germination and early growth, and fertilizer would add salts that confound the detergent treatment.

---

## 4. Pilot test (October 8–12, 2026)

### Purpose

1. Check that both seed types germinate.
2. Find the water volume that wets a paper towel without standing water.
3. Choose the detergent doses for the main experiment.

### What was planned vs. what was done

The original plan tested 0.5, 1 and 2 mL/L of each detergent on cucumber only. This was changed before the pilot started:

- **Higher doses.** A typical dishwashing basin is roughly 0.3 to 1.5 mL/L (a rough estimate, not a measurement). Doses well above this were chosen to represent concentrated greywater under water scarcity.
- **Molokhia added.** Both crops receive the same dose in the main experiment, so both were tested.
- **Fewer containers.** To save containers for the main study, both crops shared each detergent container in the pilot.

### Pilot setup (started the night of October 8, 2026)

**Water volume:** 3 mL per container, chosen as the volume that fully wets the towel without pooling.

| Container | Seeds | Solution | Volume |
| --- | --- | --- | --- |
| P1 (main-study container) | 10 cucumber | Tap water | 3 mL |
| P2 (main-study container) | 10 molokhia | Tap water | 3 mL |
| Cup 1 (substitute container) | 5 cucumber + 5 molokhia | Dish soap 10 mL/L | 3 mL |
| Cup 2 (substitute container) | 5 cucumber + 5 molokhia | Dish soap 20 mL/L | 3 mL |
| Cup 3 (substitute container) | 5 cucumber + 5 molokhia | Laundry detergent 10 mL/L | 3 mL |
| Cup 4 (substitute container) | 5 cucumber + 5 molokhia | Laundry detergent 20 mL/L | 3 mL |

**TODO:** molokhia soaking method and time; top-up volume used on pilot Day 2.

### Pilot results

By October 12, almost all seeds had germinated in every container, including at 20 mL/L.

**TODO:** exact germinated counts per container, in `data/pilot.csv`.

### Decisions taken from the pilot

1. **Doses:** keep both 10 and 20 mL/L for both detergents, giving five arms.
2. **Outcomes:** because nearly all seeds germinated even at the highest dose, germination share alone risks a ceiling effect. Day-7 seedling length was therefore added as a second, co-primary outcome alongside germination share. With two co-primary outcomes and four comparisons with tap water, the 8 primary tests are adjusted for multiple comparisons (Holm method).
3. **Pilot containers:** P1 and P2 held only tap water and may be reused after rinsing. **TODO:** record whether they were reused and flag them in `assignment.csv` (`reused` = 1).

---

## 5. Main experiment

### Arms and allocation

The control arm has twice as many containers as each treatment arm, which is efficient when every treatment is compared with the same control.

| Arm | Solution | Cucumber | Molokhia | Total |
| --- | --- | --- | --- | --- |
| T0 | Tap water | 8 | 8 | 16 |
| D10 | Dish soap 10 mL/L | 4 | 4 | 8 |
| D20 | Dish soap 20 mL/L | 4 | 4 | 8 |
| L10 | Laundry detergent 10 mL/L | 4 | 4 | 8 |
| L20 | Laundry detergent 20 mL/L | 4 | 4 | 8 |
| **Total** | | **24** | **24** | **48** |

Each container holds a single crop: containers 1–24 hold 10 cucumber seeds each, and containers 25–48 hold 10 molokhia seeds each.

### Solutions

All solutions were made once, in a single batch, to be used for the whole experiment. This keeps each concentration identical across waterings. For each solution, the detergent was measured with a syringe, added to an empty bottle, and the bottle was filled with tap water to the final volume and swirled gently.

| Solution | Detergent | Final volume |
| --- | --- | --- |
| T0, tap water | None | 500 mL |
| D10, dish soap 10 mL/L | 5 mL dish soap | 500 mL |
| D20, dish soap 20 mL/L | 10 mL dish soap | 500 mL |
| L10, laundry detergent 10 mL/L | 5 mL laundry detergent | 500 mL |
| L20, laundry detergent 20 mL/L | 10 mL laundry detergent | 500 mL |

Bottles are capped and stored away from light at room temperature, and swirled before each use. Each bottle has its own syringe.

**TODO:** date and time the solutions were made.

### Random assignment

Treatments were assigned by complete random assignment within each crop, so each crop has exactly 8 tap-water containers and 4 containers per detergent arm. Grid positions were also randomized, so that position is not tied to treatment.

```r
library(randomizr)
set.seed(20261013)
units <- data.frame(id = 1:48,
                    crop = rep(c("cucumber", "molokhia"), each = 24))
units$code <- block_ra(blocks = units$crop,
                       block_m_each = rbind(c(8, 4, 4, 4, 4),
                                            c(8, 4, 4, 4, 4)),
                       conditions = c("A", "B", "C", "D", "E"))
pos <- sample(1:48)
units$row <- (pos - 1) %/% 8 + 1
units$col <- (pos - 1) %% 8 + 1
table(units$crop, units$code)
write.csv(units, "data/assignment.csv", row.names = FALSE)
```

**TODO:** confirm this exact script and seed were used, and commit `assign.R` and `data/assignment.csv`.

### Blinding

Containers are labeled with IDs only. Codes A to E map to the five arms. Code A, which has 8 containers per crop, is tap water. The mapping of B to E to the four detergent arms is kept in a separate key until analysis.

Blinding is partial: the tap-water arm is identifiable from its larger size, and detergent foam or smell may reveal some treatments.

**TODO:** who holds the key for codes B to E.

### Planting (Day 0, night of October 12, 2026)

1. Molokhia seeds were soaked using the same method as the pilot. **TODO:** method and time.
2. Each container received one folded paper towel and **3 mL** of its assigned solution.
3. 10 seeds were placed in each container, drawn blindly from a mixed bowl for that crop.
4. Lids were closed, and containers were placed in their randomized grid positions.

**TODO:** planting start and end times; any problems during planting.

### Location and environment

All 48 containers sit together on one surface, away from radiators, vents and direct sun, with bright indirect light.

**TODO:** describe the location (room, distance from window, window direction, light source and schedule, approximate temperature).

---

## 6. Daily procedure (Days 1–7)

- **Every day:** photograph the full grid; check for mold, spills or other problems; record room temperature if possible; rotate the whole layout 180 degrees so all containers get equal exposure to the light source.
- **Days 2, 4 and 6:** add the fixed top-up volume to every container, in ID order, each with its own solution. **TODO:** top-up volume in mL.
- **Never:** water one container more or less than the others, replace seeds, remove containers, or move containers between grid positions.

Every watering and problem is recorded in `data/log.csv` (or the Log sheet of `data/measurements_2026-10-18.xlsx`). After the lids were removed on Day 6, any change to watering applies to all containers at once and is logged.

### Schedule

| Date | Day | Task |
| --- | --- | --- |
| Oct 12 | 0 | Planting |
| Oct 13–17 | 1–5 | Daily germination count and photos; top-ups on Oct 14 and 16 |
| Oct 18 | 6 | Top-up; seedlings reach lids; as-is photos; all lids removed; Amendment 1 |
| Oct 19 | 7 | Final measurement: germination share and hypocotyl length; experiment ends |

---

## 7. Outcomes and measurement

| Outcome | Definition | When |
| --- | --- | --- |
| Germination share | Germinated seeds / 10 per container; a seed counts as germinated when its root is at least 2 mm long | Daily, Days 1–7 |
| Hypocotyl length | From the root-shoot junction (where root hairs stop) to the base of the seed leaves, traced along the curve; mean over all 10 seeds per container, in mm; ungerminated seeds count as 0 mm | Day 7 |

Germination share and Day-7 hypocotyl length are **co-primary outcomes**. Days to germination is secondary. The Day-14 outcome was dropped on Day 6 (see Section 9). Full definitions are in `prereg.md`, including Amendment 1.

### Measuring seedlings

On paper towels, seedlings grow flat along the towel, and roots grow into the towel fibers. Hypocotyl length is therefore measured instead of root length or height (Amendment 1):

1. Lay any upright seedlings flat; separate tangled seedlings after wetting the towel.
2. Place the open container on a flat surface with a ruler lying flat beside it.
3. Photograph from directly above at a fixed height, with the container ID and ruler in the frame.
4. In ImageJ/Fiji, set the scale using the ruler (Analyze > Set Scale), then trace each hypocotyl with the segmented-line tool and measure it (Analyze > Measure).
5. Record each seed in `data/measurements_2026-10-18.xlsx` (Seedlings sheet), with a flag for upright, tangled or broken seedlings.

Containers are measured in ID order, 01 to 48, with the same rules for every container.

---

## 8. Analysis plan

Each container is the unit of analysis (48 observations), because all seeds in a container share the same water.

1. **Estimands:** the average effect of each detergent arm compared with tap water, by crop; the dose effect (20 vs. 10 mL/L within each detergent); and the detergent-type effect (laundry vs. dish soap, averaged over doses).
2. **Blocked estimator:** estimate effects separately for each crop, then average them, weighting by block size.
3. **Randomization inference:** under the sharp null of no effect for any container, re-run the assignment 10,000 times with the same allocation and recompute each estimate. The p-value is the share of simulated estimates at least as large in absolute value as the observed one. The 8 primary tests (4 arms × 2 co-primary outcomes) are adjusted with the Holm method.
4. **Covariate adjustment:** regress the outcome on treatment indicators, crop, and grid row and column, and compare standard errors with the unadjusted estimates.
5. **Balance check:** compare grid positions across arms.
6. **Deviations:** analyze every container by its assigned arm (intention to treat). If containers missed or received the wrong solution, report compliance by arm.
7. **Robustness:** re-estimate excluding any reused containers.

A figure will show each container's outcome by arm and crop, with arm means and confidence intervals.

---

## 9. Changes from the original plan

| Original plan | What changed | When and why |
| --- | --- | --- |
| 3 arms: tap water, dish greywater, laundry greywater | 5 arms, with two doses of each detergent | After the pilot, to test dose as well as detergent type |
| Pilot doses 0.5, 1 and 2 mL/L, cucumber only | 10 and 20 mL/L, both crops sharing each container | Before the pilot, to represent concentrated greywater and test both crops with fewer containers |
| Seed weight as a covariate | Dropped; grid position used instead | A 0.1 g kitchen scale cannot weigh 10 small seeds accurately |
| Solutions mixed fresh on every watering day | One batch for the whole experiment | Keeps concentrations identical across waterings |
| Germination share as the only primary outcome | Germination share and Day-7 seedling length as co-primary outcomes, with Holm adjustment | Pilot showed nearly all seeds germinate even at the highest dose |
| Height measured on Day 14 | Length measured from photos | Seedlings grow sideways on paper towels |
| Lids kept on throughout | All 48 lids removed on Day 6, after as-is photos | Seedlings reached the lids (Amendment 1) |
| Seedling length = root + shoot | Hypocotyl length only | Roots grew into the towel; pulling them out would break them in a way likely correlated with treatment (Amendment 1) |
| Day-14 length as a secondary outcome | Dropped; experiment ends after Day 7 | Measuring on Day 7 requires flattening and separating seedlings, which damages them (Amendment 1) |

**Pre-registration timing:** `prereg.md` was written and committed on October 13, 2026 (Day 1), after planting but before any outcome data were recorded or analyzed. The design, doses and allocation were fixed before planting; the outcome definitions and analysis plan were formally committed on Day 1. **TODO:** confirm no outcome data had been recorded before the commit.

---

## 10. Limitations

- **External validity:** an indoor setup on paper towels differs from a desert camp garden with soil, heat and real greywater.
- **Simulated greywater:** a fixed recipe improves internal validity but omits food residue, grease and the variable salts of real greywater.
- **Doses:** both doses are above the rough estimate for a typical dishwashing basin, so they represent concentrated greywater rather than average household greywater.
- **Early outcomes only:** germination and 7-day hypocotyl length do not capture root growth, harvest yield or the long-term buildup of salts in soil.
- **Lids removed on Day 6:** evaporation after lid removal may have concentrated the solutions slightly. This applies to all arms equally.
- **Small sample:** 4 containers per detergent arm per crop limits power to detect small effects.
- **Partial blinding:** see Section 5.
- **Behavior is out of scope:** whether households would adopt greywater reuse is a question about people and is left for future research.

---

## 11. Repository structure

```
.
├── README.md              # this file: design and running log
├── prereg.md              # pre-registered hypotheses and analysis plan
├── assign.R               # random assignment script
├── analysis.R             # estimates, randomization inference, figure
├── data/
│   ├── pilot.csv          # pilot setup and results
│   ├── assignment.csv     # container ID, crop, code, grid row and column
│   ├── log.csv            # waterings, temperature, deviations, notes
│   ├── germination.csv    # daily germinated count per container
│   ├── growth.csv         # exported seedling lengths (Day 7)
│   └── measurements_2026-10-18.xlsx  # per-seed measurement record and container summary
└── photos/                # daily photos, named YYYY-MM-DD_grid.jpg or YYYY-MM-DD_id07.jpg
```

Raw data files are never edited after entry; any cleaning happens in code.

### Data formats

`data/germination.csv`
```csv
date,day,id,germinated,notes
2026-10-13,1,01,0,
```

`data/log.csv`
```csv
date,time,id,action,code,volume_ml,temp_c,notes
2026-10-12,22:00,ALL,plant,,3,,Day 0 planting
```

---

## 12. Running log

| Date | Event |
| --- | --- |
| Oct 1, 2026 | Experiment topic chosen; research design drafted |
| Oct 2–5, 2026 | Materials ordered and received |
| Oct 8, 2026 (night) | Pilot started: 2 tap-water containers, 4 detergent cups |
| Oct 12, 2026 | Pilot result: nearly all seeds germinated at every dose; five-arm design finalized |
| Oct 12, 2026 (night) | Solutions prepared; 480 seeds planted in 48 containers (Day 0) |
| Oct 13, 2026 | README written; `prereg.md` committed (co-primary outcomes, analysis plan) |
| Oct 18, 2026 (Day 6) | Cucumber seedlings reached the lids; as-is photos taken; all lids removed; Amendment 1 committed (hypocotyl length, handling rules, Day-14 outcome dropped) |

Add a row for every later event, including waterings, problems and measurements.

---

## Sources

- [InfoMigrants: These refugees are growing vegetables in the desert](https://www.infomigrants.net/en/post/26724/these-refugees-are-growing-vegetables-in-the-desert)
- [NPR: Community and vegetables grow side-by-side in Syrian refugee camp gardens](https://www.npr.org/sections/thesalt/2018/02/22/587708405/community-and-vegetables-grow-side-by-side-in-syrian-refugee-camp-gardens)
- [Lemon Tree Trust: Cooking and gardening with molokhia](https://lemontreetrust.org/news/cooking-and-gardening-with-molokhia/)
- Gerber, Alan S., and Donald P. Green. 2012. *Field Experiments: Design, Analysis, and Interpretation*. New York: W.W. Norton.
- Coppock, Alexander. 2021. "Visualize as you randomize." In *Advances in Experimental Political Science*, ed. James N. Druckman and Donald P. Green, 320–336.
