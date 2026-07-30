# Brazell, Diener, Karniouchina, Moore, Séverin & Uldry (2006) — The No-Choice Option and Dual Response Choice Designs

**Full citation:** Brazell, J. D., Diener, C. G., Karniouchina, E., Moore, W. L., Séverin, V., & Uldry, P.-F. (2006). "The no-choice option and dual response choice designs." *Marketing Letters*, 17(4), 255–268. DOI: 10.1007/s11002-006-7943-8.
**Type:** Empirical journal article (simulation + two between-subjects conjoint experiments)
**Length:** 14 pages (255–268)

## One-paragraph summary

The foundational published paper on dual-response conjoint. Including a no-choice option in CBC is desirable (realism, design efficiency, market-size modeling) but costly: every no-choice response throws away information about the relative attractiveness of the available alternatives. The dual-response remedy asks a forced choice among the available alternatives first, then a free choice that adds the no-choice option. A simulation shows dual response cuts RMSE of individual-level HB coefficients by up to ~50% as the no-choice share rises (Fig. 1). Two experiments (MP3 players, n=180; laptops, n=392) then test whether adding/deleting the no-choice option violates IIA or biases parameters: using Swait–Louviere scale-adjusted coefficient-equality tests, equality up to rescaling is never rejected in eight tests, and choice-proportion shifts are at chance levels (contradicting Dhar & Simonson 2003, attributed to the richer multi-attribute products lacking obvious "compromise" alternatives). Further analysis shows no-choice selection is driven by the (un)attractiveness of the alternatives (max utility, rejected attribute levels), not decision difficulty. Conclusion: dual response delivers estimation power without systematically biasing part-worths, and yields more realistic (higher) no-choice incidence needing less post-hoc calibration.

## Key contributions relevant to the book

- Motivates *why* no-choice matters for estimation: no-choice responses starve the likelihood of information on inside-good part-worths and can degrade the information matrix when concentrated in particular choice sets (pp. 256).
- The simulation efficiency argument (pp. 257–258): dual response vs traditional single-stage free choice, RMSE of individual HB coefficients as a function of % no-choice; gains grow with no-choice incidence and preference heterogeneity.
- Empirical validation that forced-choice and free-choice data can be pooled: coefficients equal up to a scale factor (Swait–Louviere 1993 test), a nice teaching example of the role of the logit scale parameter (Tables 1A/1B, 3A/3B).
- Evidence on the behavioral driver of no-choice: max utility of the choice set (attractiveness), not utility variance (difficulty) — supports treating no-choice as a utility-maximizing alternative in a RUM, i.e., modeling it with an ASC (pp. 261–262, 264–265; Tables 2A/2B).
- Validation: HB individual-level estimates from dual response predict holdouts at least as well as traditional format; predicted no-choice share from dual response is closer to what practitioners need for market calibration (pp. 265–267, Table 4).

## Models & notation

- Aggregate logit models with effects-coded attributes; brand-specific constants; memory and price mean-centered (Study 1, pp. 258–259).
- **No-choice enters as a zero/one alternative-specific constant** (dummy ASC, following Haaijer, Kamakura & Wedel 2001) — inside goods carry attributes, the no-choice alternative carries only its ASC (p. 259; Study 2 same coding, p. 262).
- Dual-response task: stage 1 forced choice among 3 alternatives; stage 2 free choice adding the no-choice option (p. 256, p. 259).
- In pooled/constrained models comparing single-stage vs dual-response data, attribute coefficients are constrained equal up to a rescaling constant while **two separate no-choice ASCs** are allowed (the dual-response format produces much higher no-choice incidence, so its ASC differs; Table 1B, p. 261; Table 3B, p. 264).
- Scale test: Swait–Louviere (1993) likelihood-ratio test of coefficient equality up to a multiplicative scale constant; e.g., χ²(9)=11.4 n.s., rescaling constant 1.62 for less-attractive MP3 sets (p. 259).

## Estimation details

- Aggregate comparisons use standard MNL logit MLE; constrained models estimate one common coefficient vector plus a scaling constant, with log-likelihoods and 2×(LL difference) reported in Tables 1A/1B (pp. 260–261) and 3A/3B (pp. 263–264).
- Individual-level estimates for validation obtained by **hierarchical Bayes** for both traditional and dual-response models (p. 265); holdout hit rates from max-utility rule, shares from averaged individual choice probabilities; validations run both with and without no-choice holdout tasks (Table 4, p. 265).
- No-choice incidence: MP3 study 13.9% (single-stage) vs 57.7% (dual response) for less attractive sets; 9.2% vs 46.6% for more attractive sets (p. 261). Laptop study: 15.0% vs 8.4% (relabeled) and 19.6% vs 21.6% (relabeled+swapped) (p. 264).
- Regressions of no-choice proportion on max utility and utility variance (Table 2A, p. 262) and of individual no-choice counts on number of rejected attribute levels (Table 2B, p. 262; discussion pp. 264–265): attractiveness dominates.
- Practical calibration note: practitioners must usually adjust predicted no-purchase upward; dual response's higher no-choice rate needs much smaller adjustment (p. 267).

## Relevance to book chapters

- **Choice framework:** no-choice as a RUM alternative chosen when its utility exceeds all inside goods; evidence for that interpretation vs behavioral "difficulty" accounts.
- **Data organization:** dual-response data yield two responses per task — motivates the stacked two-task data layout formalized in Diener et al. (2006).
- **Likelihood construction:** shows why deleting no-choice observations wastes information and how scale (variance) differences between task formats must be handled when pooling (Swait–Louviere).
- **MNL:** clean applied example of effects coding, ASCs, and LR testing across data conditions.
- **HB-MNL:** simulation and validation are all about individual-level HB estimates; dual response is essentially an information-augmentation device for HB.
- **Conjoint practice:** the canonical citation practitioners use to justify dual-response designs; guidance on when dual response pays off (high expected no-choice, heterogeneous preferences, durables with "keep current product" constant alternative; p. 267).

## Page pointers

- Motivation, no-choice information loss: pp. 255–256
- Simulation, RMSE gains (Fig. 1): pp. 257–258
- Study 1 design & no-choice ASC coding: pp. 258–259
- Forced vs free choice coefficient equality (Table 1A): pp. 259–260
- Single-stage vs dual response, two no-choice ASCs (Table 1B): pp. 260–261
- Attractiveness vs difficulty regressions (Tables 2A/2B): pp. 261–262, 264–265
- Study 2 (laptops, Tables 3A/3B): pp. 262–264
- HB choice validations (Table 4): pp. 265–266
- Summary and practical recommendations: pp. 266–267
