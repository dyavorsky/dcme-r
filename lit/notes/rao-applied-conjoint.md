# Rao — Applied Conjoint Analysis

**Full citation:** Rao, Vithala R. (2014). *Applied Conjoint Analysis*. Berlin/Heidelberg: Springer-Verlag. ISBN 978-3-540-87752-3 (print), 978-3-540-87753-0 (eBook). DOI 10.1007/978-3-540-87753-0.
**Type:** Book
**Length:** 401 PDF pages; book runs to ~p. 385 plus index. **Offset: PDF page = book page + 16** (Ch. 1 book p. 1 = PDF p. 17). Front matter (title, dedication, preface, TOC) occupies PDF pp. 1–16.

## Overview

A comprehensive applied treatment of conjoint analysis by one of the field's senior figures (dedicated to Paul Green, founder of conjoint methods). The book's stated aim is to make conjoint methods "understandable to students and practitioners without losing rigor." Coverage spans the full workflow — attribute selection, experimental design, data collection, estimation, and managerial use (simulators, product design, pricing, segmentation) — for both ratings-based (traditional) and choice-based (CBC) conjoint. The estimation content is practitioner-oriented: it presents the MNL model, maximum likelihood, and hierarchical Bayes at a "how it works" level (including a full WinBUGS code listing for an HB-MNL), citing Greene, Louviere et al., Allenby/Lenk, and Huber–Train rather than deriving results. Its distinctive strength relative to econometrics texts (Train, Rossi et al.) is the design side: fractional factorials, orthogonal arrays, D/A-efficiency, choice-set construction strategies, and the ratings-vs-choice tradeoff, all illustrated with real marketing applications and Sawtooth Software practice.

## Chapter-by-chapter index

### Ch 1: Problem Setting (book pp. 1–36; PDF pp. 17–52)
Motivates conjoint analysis within marketing decisions, sketches its origins (conjoint measurement, Green), defines terminology (attributes, levels, partworths, profiles), and gives a taxonomy of conjoint methods (ratings-based, choice-based, self-explicated, adaptive, hybrid). Includes a worked illustration of both a ratings study and a choice-based study, plus an appendix cataloguing non-marketing applications.
**Relevant to book chapters on:** choice framework, conjoint practice.

### Ch 2: Theory and Design of Conjoint Studies (Ratings Based Methods) (book pp. 37–78; PDF pp. 53–94)
The experimental-design chapter for ratings conjoint: attribute/level selection, partworth function types, and stimulus-set construction via full factorials, fractional factorials, orthogonal main-effects plans, incomplete block designs, and random sampling. Also covers data-collection formats (full profile, trade-off matrix, paired comparison, self-explication, adaptive, hybrid) and reliability/validity. Appendix 2 defines design-efficiency measures (D-/A-efficiency); Appendix 3 reproduces several orthogonal plans.
**Relevant to book chapters on:** experimental design, data organization, conjoint practice.

### Ch 3: Analysis and Utilization of Conjoint Data (Ratings Based Methods) (book pp. 79–126; PDF pp. 95–142)
Estimation for ratings data: additive and interaction utility models, dummy/effects coding of categorical attributes, and the individual vs. subgroup vs. pooled analysis choice. Covers market simulators, hybrid and adaptive (ACA, polyhedral) model estimation, and methods for ranked/categorical responses. Appendix 3 (book pp. 117–121; PDF pp. 133–137) is a compact primer on hierarchical Bayesian estimation for the linear conjoint model — conjugate normal/inverted chi-squared priors, full conditionals, Gibbs sampling, covariate-driven (Lenk et al. 1996) and finite-mixture variants.
**Relevant to book chapters on:** data organization (coding), Bayes-MCMC (linear-model warm-up), conjoint practice.

### Ch 4: Choice Based Conjoint Studies: Design and Analysis (book pp. 127–184; PDF pp. 143–200)
The core chapter for this project. (1) Grounds CBC in random utility theory (reproduces McFadden's 1986 choice-process diagram) and notes the key design complication: unlike linear models, the information matrix in choice models depends on the unknown betas. (2) Design of choice sets: binary vs. multinomial choice experiments, no-choice option, labeled (branded) vs. generic designs, a taxonomy of choice-set designs, and design strategies based on linear models, nonlinear models with assumed betas, and Bayesian designs with a prior on betas; D-efficiency illustrations in appendices. (3) Estimation: full development of the MNL — Type-I extreme value errors, scale parameter, choice probability derivation (Eq. 4.6), marginal effects and elasticities, the long-format data structure (individual × choice set × alternative with y and X columns), MLE of the likelihood, fit statistics (U², chi-square, AIC, BIC), and IIA with the red-bus/blue-bus example. Worked MNL examples (Louviere fast-food, jeans, smart-phone data). (4) Section 4.10 surveys alternatives: multinomial probit, heteroscedastic extreme value, random-coefficients (mixed) logit, nested logit — with a side-by-side MNL/MNP/HEV estimate table. (5) Section 4.11 covers HB estimation for CBC, including full WinBUGS code for a random-coefficients HB-MNL (multivariate normal heterogeneity, Wishart prior) and a summary of Huber–Train (2001) comparing HB with maximum simulated likelihood (near-identical means and holdout hit rates). Closes with a ratings-vs-choice comparison table and a software survey (Sawtooth CBC, LIMDEP, GAUSS/MATLAB).
**Relevant to book chapters on:** choice framework, experimental design, data organization, MLE, Bayes-MCMC, mixed logit, conjoint practice.

### Ch 5: Methods for a Large Number of Attributes (book pp. 185–224; PDF pp. 201–240)
Surveys strategies when attribute counts overwhelm respondents: partial-profile methods, attribute simplification, self-explicated methods (including adaptive self-explication), combined/hybrid approaches, upgrading methods, and support-vector-machine estimation. The opening pages give a clean statement of the parameter-count problem (parameters = sum of levels minus attributes) that motivates HB and other information-pooling approaches.
**Relevant to book chapters on:** experimental design, conjoint practice.

### Ch 6: Applications for Product and Service Design and Product Line Decisions (book pp. 225–274; PDF pp. 241–290)
Managerial-use chapter: a unified product design framework, the role of choice simulators, and eight case applications (trucks, cameras, hotels, e-toll systems, pharma) plus product-line optimization (SIMOPT, genetic algorithms) in appendices.
**Relevant to book chapters on:** conjoint practice (downstream use of estimated partworths).

### Ch 7: Applications for Product Positioning and Market Segmentation (book pp. 275–290; PDF pp. 291–306)
Short chapter on segmenting with conjoint output. Notably contrasts two-step segmentation (cluster individual-level partworths) with one-step latent-class estimation of segment-specific choice models chosen via AIC — a useful applied framing for finite-mixture MNL.
**Relevant to book chapters on:** conjoint practice; tangentially mixed logit (latent-class heterogeneity).

### Ch 8: Applications for Pricing Decisions (book pp. 291–316; PDF pp. 307–332)
Conjoint for pricing: brand/price trade-off designs, self- and cross-price elasticities from logit estimates, competitor-reaction elasticities, reservation-price methods, and applications (contract bidding, digital content, multipart pricing). Shows how price enters ratings- vs choice-based studies.
**Relevant to book chapters on:** conjoint practice; interpretation of price coefficients (WTP-adjacent).

### Ch 9: Applications to a Miscellany of Marketing Problems (book pp. 317–344; PDF pp. 333–360)
Applications grab-bag: competitive strategy (attributes + cost structures), store location, sales quotas, channel choice, web design, legal/damages uses (patent infringement, class actions), resource allocation (market value of attribute improvement), brand equity, and satisfaction.
**Relevant to book chapters on:** conjoint practice.

### Ch 10: Recent Developments and Future Outlook (book pp. 345–362; PDF pp. 361–378)
Newer elicitation formats: mixture/mixture-amount designs, incentive-aligned barter conjoint (detailed protocol), conjoint poker, best-worst scaling (MaxDiff), peer-influence measurement, non-compensatory choice processes, combining preference and choice data, self-designed products, and bundle choice models.
**Relevant to book chapters on:** conjoint practice, choice framework (non-compensatory extensions).

### Ch 11: Beyond Conjoint Analysis: Advances in Preference Measurement (book pp. 363–381; PDF pp. 379–397)
Reproduction of the multi-author 2008 Choice Symposium paper (Marketing Letters, 2008) as a supplement — a research agenda covering optimal design beyond A-/D-efficiency (M-efficiency, managerially weighted designs), adaptive questionnaires, large attribute spaces, combining data sources, flexible utility functions, social interactions, behavioral effects, dynamics, and "recent tools for estimation."
**Relevant to book chapters on:** experimental design (efficiency criteria), mixed logit / flexible heterogeneity (pointers to literature).

## Most useful chapters for this project

1. **Ch 4** (PDF pp. 143–200) — the single most relevant chapter: an applied, self-contained treatment of CBC design + MNL derivation, MLE, fit statistics, IIA, MNP/HEV/mixed-logit alternatives, and HB-MNL with actual WinBUGS code. Excellent source for the data-structure exposition (long-format choice data table, book p. 158) and for motivating why Bayesian designs are needed when the information matrix depends on beta.
2. **Ch 3 Appendix 3** (PDF pp. 133–137) — concise HB/Gibbs primer for the linear conjoint model; a natural stepping-stone before HB-MNL, parallel to how an estimation book might sequence Bayesian linear regression before Bayesian logit.
3. **Ch 2** (PDF pp. 53–94) — fractional factorial and orthogonal-array design fundamentals plus D-/A-efficiency; complements econometrics texts that assume the design is given.
4. **Ch 1** (PDF pp. 17–52) — accessible framing, terminology, and taxonomy useful for an introductory chapter situating conjoint/stated-preference data as the input to discrete choice estimation.
5. **Ch 11** (PDF pp. 379–397) — quick literature map for "where the field is going" boxes (M-efficiency, adaptive design, flexible heterogeneity).

Caveats for an estimation-focused text: Rao presents estimators descriptively (no likelihood asymptotics, no MCMC diagnostics), uses WinBUGS rather than R, and Chs. 5–9 are application case studies with little estimation content. Use it for design, data layout, applied context, and the ratings-vs-choice comparison — not as the primary source for estimation theory (pair with Train, Rossi/Allenby/McCulloch).
