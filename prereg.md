# Pre-registration: Greywater Irrigation and Seed Germination

**Author:** Xingyi Wang
**Course:** Experimental Research: Design, Analysis, and Interpretation (GU4724), Columbia University, Fall 2026

## Timing

This plan (Sections 1 to 9) was **written and committed to GitHub on October 13, 2026 (Day 1)**, in commit `552906e`, after the seeds were planted on the night of October 12 (Day 0) and **before any outcome data were recorded or analyzed**. The containers were left undisturbed on Days 1 to 5.

Sections 1 to 9 are kept as committed on October 13, apart from one bracketed note added in Section 3. Every later change is listed in Amendment 1, and the full edit history is visible in the repository.

The design, doses and allocation were fixed before planting; see `README.md` for the full design history, including changes made after the pilot.

---

## 1. Research question

Does irrigating with simulated household greywater reduce the germination and early growth of cucumber and molokhia seeds, compared with tap water?

## 2. Hypotheses

All hypotheses compare each detergent arm with tap water (T0).

- **H1 (dish soap):** dish soap solutions (D10, D20) reduce germination share and seedling length relative to tap water.
- **H2 (laundry detergent):** laundry detergent solutions (L10, L20) reduce germination share and seedling length relative to tap water.
- **H3 (dose):** the 20 mL/L solutions reduce outcomes more than the 10 mL/L solutions of the same detergent. *(Secondary)*
- **H4 (detergent type):** laundry detergent reduces outcomes more than dish soap at the same dose, because laundry detergents typically contain more salts. *(Secondary)*

The pilot found that nearly all seeds germinated even at 20 mL/L, so effects on germination share may be small. All tests are two-sided.

## 3. Design

- **Units:** 48 containers, each holding one folded paper towel and 10 seeds of a single crop.
- **Blocks:** crop. Containers 1–24 hold cucumber; containers 25–48 hold molokhia.
- **Arms:**

| Arm | Solution | Containers per crop |
| --- | --- | --- |
| T0 | Tap water | 8 |
| D10 | Dish soap, 10 mL/L | 4 |
| D20 | Dish soap, 20 mL/L | 4 |
| L10 | Laundry detergent, 10 mL/L | 4 |
| L20 | Laundry detergent, 20 mL/L | 4 |

- **Assignment:** complete random assignment within each crop, using `randomizr::block_ra` with a fixed seed (`assign.R`). Grid positions were also randomized.
- **Watering:** 3 mL at planting; a fixed top-up volume for every container on Days 2, 4, 6, 8, 10 and 12. *(The top-up volume was never set, and no top-ups were given; see Amendment 1.)*
- **Solutions:** made once, in a single 500 mL batch per arm, before planting.

## 4. Outcomes

The unit of analysis is the container (n = 48), because all seeds in a container share the same water.

### Co-primary outcomes

1. **Germination share on Day 7:** number of germinated seeds divided by 10. A seed counts as germinated when its root is at least 2 mm long.
2. **Mean seedling length on Day 7 (mm):** root length plus shoot length (seed to the base of the seed leaves), averaged over all 10 seeds. Seeds that did not germinate count as 0 mm.

Seedling length is measured from overhead photos with a ruler in the frame, using ImageJ/Fiji.

### Secondary outcomes

3. Mean seedling length on Day 14 (mm), defined as above. If any seedling touches a lid before Day 14, all containers are measured on that day instead, and the date is reported.
4. Days to germination: from the daily counts on Days 1–7.

## 5. Estimands

For each detergent arm *k* (D10, D20, L10, L20) and each outcome:

- **Primary estimand:** the average treatment effect of arm *k* relative to tap water, pooled across crops:
  ATE_k = E[Y(k) − Y(T0)], estimated as the average of the two within-crop differences in means, weighted equally because the blocks are equal in size.

- **Secondary estimands:**
  - The same effects estimated separately for each crop.
  - Dose: ATE(D20) − ATE(D10) and ATE(L20) − ATE(L10).
  - Detergent type: the average of the two laundry effects minus the average of the two dish soap effects.

## 6. Analysis plan

### Primary analysis

1. **Estimator:** the blocked difference in means described above, for each of the 4 arms × 2 co-primary outcomes = **8 primary tests**.
2. **Inference:** randomization inference under the sharp null hypothesis that water type has no effect on any container. The assignment is re-drawn 10,000 times with the same procedure and allocation as `assign.R`, and each estimate is recomputed. The two-sided p-value is the share of simulated estimates at least as large in absolute value as the observed estimate.
3. **Multiple comparisons:** p-values for the 8 primary tests are adjusted with the Holm method. Effects are called statistically significant if the Holm-adjusted p-value is below 0.05. Unadjusted p-values are also reported.
4. **Uncertainty:** standard errors and 95% confidence intervals are reported alongside the p-values.

### Secondary and supporting analyses

5. **Covariate adjustment:** regress each outcome on arm indicators, crop, and grid row and column. Compare standard errors with the unadjusted estimates.
6. **Balance check:** compare grid positions across arms.
7. **Secondary estimands** (Section 5) and **secondary outcomes** (Section 4) are reported without multiple-comparison adjustment and labeled as secondary.
8. Any analysis not listed in this document is labeled **exploratory**.

## 7. Deviations, missing data and problems

- **Intention to treat:** every container is analyzed in its assigned arm, whatever it actually received.
- **Deviations:** watering errors (wrong solution, missed or extra watering) are logged in `data/log.csv` and reported by arm.
- **Mold, spills and damage:** containers are kept in the analysis. Mold is recorded but not removed, because it may itself be an effect of treatment.
- **No container is dropped, re-planted or replaced.**
- **Missing measurements:** if a measurement is missing (for example, an unusable photo), it is reported, and the main analysis uses all available containers. A sensitivity check sets the missing value to the lowest and highest observed values in that arm.
- **Robustness:** if any containers were reused from the pilot (flagged in `assignment.csv`), the primary analysis is repeated excluding them.

## 8. Blinding

Containers are labeled with IDs only. Codes B to E are mapped to the four detergent arms by a key kept separately until outcome data are entered. Code A, the tap-water arm, is identifiable because it has 8 containers per crop, so blinding is partial.

## 9. Reporting

All pre-registered results are reported whatever their direction or significance, including null results. Any departure from this plan is listed and explained in `README.md`.

---

## Amendment 1 (recorded October 19, 2026)

### Timing

This amendment records events and decisions from the evening of **October 18, 2026 (Day 6)**. The measurement rules below were decided that evening, before the measurement was taken, while containers were labeled with IDs only and codes B to E were still blinded. No results had been compared across arms. This amendment was committed to GitHub on October 19, after the measurement had been taken, so its commit time does not by itself prove the rules came first.

### What happened

1. **Watering.** No top-ups were given on Days 2 and 4, so the pre-registered top-up schedule was not followed. This applied to every container equally. The only watering after planting was on the evening of Day 6, when each container received 3 mL of its own assigned solution, **after** the measurement. Up to the measurement, every container therefore received only the 3 mL given at planting.
2. **Seedlings reached the lids.** On the evening of Day 6, cucumber seedlings in many containers touched the lids. Inspection also showed that roots had grown into the paper towel fibers, and that some seedlings grew upright or became tangled.
3. **Measurement on Day 6.** The final measurement was taken on the evening of Day 6, not on Day 7 as pre-registered, because the seedlings had reached the lids. For each container, in ID order, the whole paper towel with its seedlings was lifted out, laid flat on a table, and each seedling was measured by hand with a flexible tape measure, in mm. **No photos were taken for measurement.**
4. **Lids.** Lids were removed only while measuring and were put back on afterwards, so all containers stayed covered.

### Changes to the pre-registered plan

1. **Seedling length outcome redefined.** The co-primary length outcome is changed from root + shoot length to **hypocotyl length**: from the root-shoot junction (where root hairs stop) to the base of the seed leaves, measured along its curve, in mm. Ungerminated seeds count as 0 mm. This is what was measured.
   - *Reason:* roots had grown into the towel fibers, and pulling them out breaks them. Breakage would likely be worse for longer, healthier roots, so root measurement error would be correlated with treatment and could bias the comparison. The hypocotyl lies on the towel surface and can be measured without pulling the seedling out.
2. **Measurement method.** Hand measurement with a flexible tape measure replaces measurement from photos. Its precision is about 1 mm.
3. **Handling rules** used during measurement, for every container:
   - Upright seedlings were laid flat gently before measuring.
   - Tangled seedlings were separated. If they could not be separated, the group's total hypocotyl length was divided by the number of seedlings and that value was recorded for each, flagged `tangled`.
   - Broken seedlings: the pieces were measured and added, flagged `broken`.
   - An empty seed coat was not used as the starting point.
   These rules were applied to every container.
4. **Timing of the outcomes.** Both co-primary outcomes (germination share and hypocotyl length) are measured on Day 6 instead of Day 7.
5. **Day-14 outcome dropped.** Measurement required lifting out the towels and handling the seedlings, so the Day-6 measurement is the final measurement. No Day-14 outcome will be reported.
6. **Photos.** Photos of all 48 containers taken after the measurement are a visual record only. They are not used to measure outcomes.
7. **Unchanged:** the arms, the 2 mm germination rule, the estimators, randomization inference and the Holm adjustment.
