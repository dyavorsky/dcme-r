# Diener, Orme & Yardley (2006) — Dual Response "None" Approaches: Theory and Practice

**Full citation:** Diener, C., Orme, B., & Yardley, D. (2006). "Dual Response 'None' Approaches: Theory and Practice." *2006 Sawtooth Software Conference Proceedings*, Sequim, WA, 157–167.
**Type:** Practitioner conference paper (methods + empirical comparison of estimation setups)
**Length:** 11 pages (157–167)

## One-paragraph summary

The practitioner's how-to companion to Brazell et al. (2006). Defines dual-response (DR) "None" conjoint — each task collects (1) a forced choice among the shown alternatives and (2) a buy/no-buy follow-up — and distinguishes two follow-up formats: **DR-2Max** ("would you actually buy the option you selected?") and **DR-AnyMax** ("would you buy any of the options listed?"). It writes down the corresponding likelihoods explicitly: DR-2Max is (forced-choice MNL) × (binary logit of the chosen alternative vs None), while DR-AnyMax multiplies the forced-choice MNL by the probability the inside goods beat None and *algebraically collapses to a standard MNL that includes None in the denominator*. Because the joint log-likelihood is additive, DR data can be "stacked" as two pseudo-choice-tasks and fed to any standard MNL/HB routine that tolerates varying numbers of alternatives per task. Empirical tests (one simulated + two real datasets) show all setups (Sawtooth CBC/HB v4, custom simultaneous likelihood, stacked MNL-AnyMax, stacked MNL-2Max) give similar hit rates, but MNL-2Max systematically biases the None ASC downward relative to AnyMax. Recommendation: use the 2Max *task* (easier for respondents) with the AnyMax *estimation* likelihood.

## Key contributions relevant to the book

- The cleanest published statement of the **dual-response likelihood algebra** — a great teaching example of building a joint likelihood from two responses and recognizing when it reduces to a standard MNL.
- Shows the **stacked-data trick**: because ln(P1·P2) = ln P1 + ln P2, dual responses can be coded as two separate choice tasks per scenario and estimated with off-the-shelf MNL/HB software — exactly the kind of data-organization insight the book teaches for R implementation.
- Documents that the *only* parameter sensitive to the 2Max vs AnyMax modeling choice is the None ASC; attribute part-worths are robust (pp. 164–165).
- Quantifies efficiency gains from DR: at 12% None incidence, ~25% decrease in model error (equivalent to 180 → 130 respondents); at 33%, ~55% decrease (290 → 130 respondents) (p. 159, citing Uldry et al. 2002).
- Practical checklist for when to use DR (p. 167).

## Models & notation

All utilities are linear-in-parameters logit; FC = set of shown ("forced choice") alternatives, FC0 = the None/Other alternative, coded with its own ASC β_FC0 (or β_2nd0 in the second stage).

- **Eq. 1 (p. 160), standard single-response MNL with None:** P(i | FC & FC0) = e^{β'x_i} / (Σ_j e^{β'x_j} + e^{β_FC0}).
- **Eq. 2 (p. 160), forced choice (stage 1):** P(i | FC) = e^{β'x_i} / Σ_j e^{β'x_j}.
- **Eq. 3 (p. 160), DR-2Max stage 2 (binary logit, chosen alt vs None):** P(i | 2nd) = e^{β'x_i} / (e^{β'x_i} + e^{β_2nd0}).
- **Eq. 4 (p. 161), DR-2Max joint likelihood:** product of Eq. 2 and Eq. 3.
- **Eq. 6 (p. 161), DR-AnyMax stage 2 (any inside good vs None):** P(FC | 2nd) = Σ_j e^{β'x_j} / (Σ_j e^{β'x_j} + e^{β_2nd0}).
- **Eqs. 7–8 (p. 161), DR-AnyMax joint likelihood:** the forced-choice term cancels against the numerator of Eq. 6, reducing to P(i | DR2) = e^{β'x_i} / (Σ_j e^{β'x_j} + e^{β_2nd0}) — i.e., a standard MNL over inside goods plus None. (Hung et al. 2025 later derive this same expression from a shared-error/"unified" assumption.)
- None coded via ASC; the authors tested dummy vs effects coding, a separate parameter for the first-vs-second response, etc., and found no differences in estimates or accuracy (pp. 165–166).

## Estimation details

- The joint likelihood can be maximized directly (custom ML or HB routine), **or** the data can be stacked: each dual response becomes two rows-of-tasks — stage 1 as a forced-choice task without None; stage 2 either as {chosen alternative, None} (replicates DR-2Max) or as {all alternatives, None} (replicates DR-AnyMax) (pp. 161–162).
- **Redundant-task rule (Table 1, p. 162):** if the respondent said "yes, would buy" in stage 2, the stage-2 task (which includes None) fully contains the stage-1 information, so the stage-1 row block must be dropped to avoid double counting. Sawtooth's CBC/HB v4 automates this stacking and de-duplication (p. 163).
- Estimation requires software that accepts different numbers of alternatives per task within respondent (pp. 161–162).
- Four compared conditions (p. 163): Sawtooth CBC/HB v4; DR-Custom (simultaneous AnyMax LL); MNL-AnyMax (stacked); MNL-2Max (stacked). Results (Table 2, p. 164): hit rates 57–65% across methods and datasets; MNL-2Max has notably worse MAE (e.g., 6.09 vs ~3.0–3.6 in DataSet1).
- **Bias diagnosis (Chart 1, pp. 164–165):** plotting estimates across methods, all coefficients line up except the None ASC — 2Max estimation yields a consistently lower None utility than AnyMax. Which is "right" depends on the data-generating assumption: simulating under AnyMax makes 2Max look downward-biased and vice versa. Intuition: under AnyMax, None competes against J alternatives each with its own error draw, so its ASC must be larger to be chosen at the same rate (p. 165).
- Recommended pairing: **2Max task, AnyMax estimation**; no adverse effects observed from the mismatch (p. 166).

## Relevance to book chapters

- **Choice framework:** contrasts two behavioral stories for the second response (compare None with the single best vs with the whole set) and shows how each maps to a different likelihood.
- **Data organization:** Table 1 (p. 162) is a ready-made illustration of long-format choice data, stacking dual responses, and dropping redundant tasks — directly reproducible in R.
- **Likelihood construction:** Eqs. 1–8 are a compact case study in composing joint likelihoods from sequential responses and simplifying them; also shows why an additive log-likelihood permits estimation with standard software.
- **MNL:** DR-AnyMax = MNL with a None ASC; makes the "outside good as an extra alternative with a constant" idea concrete.
- **HB-MNL:** all comparisons run through Sawtooth CBC/HB; demonstrates practical robustness of HB estimates to data-setup variants.
- **Conjoint practice:** task-format examples (Examples 1–2, p. 158), efficiency/sample-size trade-offs, and the when-to-use-DR checklist.

## Page pointers

- DR definition, 2Max vs AnyMax task formats (Examples 1–2): pp. 157–159
- Benefits and efficiency numbers (25%/55% error reductions): p. 159
- Likelihood equations (Eqs. 1–8): pp. 160–161
- Stacked-data setup and redundant-task removal (Table 1): pp. 162–163
- Four estimation setups and results (Table 2): pp. 163–164
- None-ASC bias analysis (Chart 1): pp. 164–165
- ASC-coding robustness tests: pp. 165–166
- Recommendation (2Max task + AnyMax estimation) and conclusions: pp. 166–167
