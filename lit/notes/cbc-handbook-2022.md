# Eggers, Sattler, Teichert & Völckner (2022) — Choice-Based Conjoint Analysis

**Full citation:** Eggers, F., Sattler, H., Teichert, T., & Völckner, F. (2022). Choice-Based Conjoint Analysis. In C. Homburg, M. Klarmann, & A. Vomberg (Eds.), *Handbook of Market Research* (pp. 781-819). Springer Nature Switzerland. https://doi.org/10.1007/978-3-319-57413-4_23
**Type:** Handbook chapter / tutorial survey (state-of-the-art overview with worked R example)
**Length:** 39 pages (pp. 781-819)

## One-paragraph summary

The single best end-to-end tutorial among the four papers: it walks the full CBC workflow — attribute/level identification → experimental design (factorial + choice design) → questionnaire implementation (no-choice, dual response, best-worst, incentive alignment, holdouts) → aggregate MNL estimation via maximum likelihood → managerial transformations (attribute importance, WTP, market simulation/demand curves) → advanced estimation (latent class, hierarchical Bayes). A running "ebook reader" example (storage, screen size, color, price; 200 simulated respondents, 10 choice sets, 3 alternatives + no-choice) is carried through every step, with complete R code using the **mlogit** package in the Appendix and downloadable data (preferencelab.com/data/CBC.R, Ebook_Reader.csv). Utility theory is grounded in RUT (McFadden), and the chapter is careful about coding (dummy vs. effect coding), model comparison (LR tests, McFadden R²), and the assumptions needed to read choice shares as market shares.

## Key contributions relevant to the book

- **The CBC workflow as chapter skeleton.** Sections map one-to-one onto a course: model (utility + choice), attribute selection, design, questionnaire, estimation, transformation of estimates, heterogeneity. Fig. 3 (p. 787): product attributes → utility model → utility evaluation → choice model → observed choice.
- **Attribute/level requirements** (pp. 791-793): attributes relevant, discriminating, ≤~7, not interrelated; levels span slightly-beyond-reality range, unambiguous, few (3-4 typical), balanced number across attributes (number-of-levels effect), acceptable, mutually exclusive.
- **Design efficiency criteria** (Huber & Zwerina 1996; p. 793): balance, orthogonality, minimal overlap, utility balance; factorial design vs. choice design distinction; full vs. fractional factorial with effect-coded 2^3 example and confounding logic (Tables 1-3, pp. 784, 793-794); fold-over trick for minimal-overlap choice sets (p. 795); practical guidance: 2-5 alternatives per set, ~10-15 choice sets typical (JMR review, p. 796).
- **Questionnaire devices** (pp. 796-799): no-choice option (realism, WTP anchor), dual-response none (Brazell et al. 2006), best-worst/MaxDiff choices (β_best = −β_worst assumption), incentive alignment (Ding 2005/2007, BDM lottery), holdout sets for validation (hit rate, MAE).
- **Data layout for estimation** (Fig. 7, p. 801): long format — one row per alternative, Resp_id/Set_id/Alt_id, Selected as 0/1 dependent variable, effect-coded attribute columns, None dummy. Directly mirrors what mlogit/logitr/ChoiceModelR expect — very useful template for the book's data-organization chapter.
- **Managerial post-estimation** (pp. 804-807): relative attribute importance via part-worth ranges (Eq. 10); WTP as β ratio against linear price (Eq. 11) with signed incremental interpretation; market simulation via MNL shares for defined scenarios, demand curves by varying price (Fig. 8), absolute WTP as price where product ties the no-choice option (€130); assumptions (a)/(b) under which probabilities ≈ market shares (p. 807).
- **Model comparison in practice** (Table 6, p. 805; p. 808): partworth vs. vector vs. ideal-point vs. interaction specifications on the same data, compared via LR tests; ideal point for screen size solved as ∂v/∂x = 0 → 5.87 in.
- **Heterogeneity** (pp. 808-812): latent class (iterative EM-style loop, posterior membership, AIC/BIC/CAIC + entropy; 3-segment solution overturns the aggregate "6-in. white" conclusion — a great teaching moment) and HB (two-layer model, MNL likelihood + multivariate normal population layer, Metropolis-Hastings, ~20,000 iterations, burn-in; Fig. 9 p. 811, boxplots Fig. 10 p. 812).

## Models & notation

- RUT: U_ci = V_ci + e_ci; choice probability p_i = p(V_i − V_j > e_j − e_i) (Eq. 1, p. 787). Only utility differences matter; constants must be alternative-specific (p. 788).
- V_i = Ψ[f_1(v_1i), ..., f_N(v_Ni)] (Eq. 2, p. 788); evaluation functions: vector v_in = β_n·X_inm (Eq. 3), ideal point with squared term (Eq. 4), partworth with M−1 dummy/effect codes (Eq. 5) (pp. 788-789; Fig. 4).
- Additive combination V_i = Σ v_in (Eq. 6) plus interaction terms (Eq. 7) (p. 790).
- MNL: p(i|S) = exp(V_i)/Σ_{j∈S} exp(V_j) (Eq. 8, p. 791); iid Gumbel errors; probit noted as alternative but rarely used in CBC (p. 791).
- Likelihood L = Π_c Π_t p(i_tc|S_tc) (Eq. 9, p. 802); attribute importance w_n (Eq. 10, p. 804); WTP_nm = β_nm/β_p (Eq. 11, p. 804).

## Estimation details

- Aggregate ML estimation of MNL (pp. 799-803): pooled across respondents; null benchmark LL = T·C·log(1/S) (= −2772.6 in the example); fitted LL = −2277.8; LR test χ² = 989.6, df 10; McFadden R² = 0.178 with 0.2-0.4 rule of thumb, low fit attributed to unmodeled heterogeneity (p. 803).
- Coding (pp. 800-801): dummy vs. effect coding; reference-level partworth recovered as negative sum of estimated ones; standard error of reference level needs off-diagonal vcov elements — the Appendix R code shows sqrt(sum(covMatrix[i:j, i:j])) explicitly (p. 814).
- Latent class (pp. 809-810): fix #segments, iterate segment-specific ML + Bayes-rule posterior membership; choose #segments by AIC/BIC/CAIC + entropy (0.948 in example); individual estimates from LC lie in convex hull of segment utilities — HB preferred for individual level.
- HB (p. 811): MNL first layer, multivariate normal second layer (Arora et al. 1998; Lindley & Smith 1972), Metropolis-Hastings, burn-in, inference from retained draws.
- **Appendix R code (pp. 813-816):** mlogit.data(..., choice="Selected", shape="long", alt.var="Alt_id", id.var="Resp_id"); models ml1-ml5 (partworth, vector, vector-for-screen-size, ideal point, interactions); lrtest() comparisons; WTP as coefficient ratios.

## Relevance to book chapters

- **Choice framework:** RUT setup, Eq. 1-8, scale/identification remarks (differences only; alternative-specific constants) — clean minimal treatment to cite.
- **Experimental design:** the most complete practical treatment of the four papers — factorial vs. choice design, efficiency criteria, fractional factorial confounding example, decision parameters (alternatives per set, number of sets).
- **Data organization:** Fig. 7 long-format dataset + coding section is a ready-made template for the book's data chapter and matches mlogit conventions.
- **MNL:** worked ML estimation with null LL, LR test, McFadden R², effect-coding recovery of reference levels — directly reproducible in R from the appendix.
- **HB-MNL:** conceptual two-layer HB description and boxplot presentation of individual partworths; hands off to a dedicated chapter for depth.
- **Post-estimation / market simulation:** Eqs. 10-11, scenario-based share simulation, demand curve, absolute vs. incremental WTP, share-interpretation assumptions.
- **Conjoint practice:** attribute/level rules, no-choice & dual response, incentive alignment, holdout validation, number-of-levels effect.

## Page pointers

- p. 781: TOC of the chapter; abstract
- pp. 782-786: intro, ebook example, evolution of conjoint (static/adaptive/interactive, Fig. 2), extended example attributes (Table 2)
- pp. 787-791: utility model (RUT, Eqs. 1-7, Fig. 4 functional forms), MNL choice model (Eq. 8, Fig. 5)
- pp. 791-793: attribute & level selection requirements
- pp. 793-796: factorial design, fractional factorial & confounding (Table 3), choice design, minimal overlap/utility balance, alternatives & sets counts
- pp. 796-799: stimuli presentation, no-choice & dual response, best-worst, incentive alignment (Ding), holdouts
- pp. 799-803: estimation — coding (Table 4), long-format data (Fig. 7), ML, null model, LR test, McFadden R², aggregate estimates (Table 5)
- pp. 804-807: attribute importance (Eq. 10), WTP (Eq. 11), market simulation, demand function (Fig. 8), probabilities-as-shares assumptions
- pp. 805, 808: alternative specifications compared (Table 6), ideal point solution
- pp. 809-812: latent class (Table 7), HB (Fig. 9), individual-level boxplots (Fig. 10)
- p. 813: outlook; start of Appendix R code
- pp. 813-816: full mlogit R code; data URL (preferencelab.com)
- pp. 816-819: references
