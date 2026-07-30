# Hess & Daly (2024) — Handbook of Choice Modelling, 2nd ed.

**Full citation:** Hess, S., & Daly, A. (Eds.) (2024). *Handbook of Choice Modelling*, 2nd edition. Cheltenham, UK: Edward Elgar Publishing. ISBN 978-1-80037-562-8 (cased); 978-1-80037-563-5 (eBook). DOI: 10.4337/9781800375635.
**Type:** Edited handbook (26 chapters, 6 parts; thoroughly peer-reviewed invited contributions)
**Length:** 787 PDF pages; book runs to p. 785 (index). Book page ≈ PDF page − 6 for most of the volume, **but the offset is not uniform**: this PDF (assembled with PDFsam) has two chapter pairs physically swapped relative to the printed order — Ch 5 appears *before* Ch 4 (PDF pp. 80 vs 110) and Ch 12 appears *before* Ch 11 (PDF pp. 312 vs 332). Use the PDF page ranges below, not book pages.

## Overview
The second edition (first ed. 2014) of the field's cross-disciplinary reference on choice modelling, spanning transport, marketing, health, and environmental economics. Six parts: (I) Foundations — economic and psychological theories of choice plus machine learning; (II) Observing Preferences — RP data capture, stated choice experimental design, best-worst scaling, hypothetical bias, VR; (III) Modelling Heterogeneity — nonparametric mixing distributions, attribute processing, alternative decision rules, latent class; (IV) Extended Frameworks — ordered choices, household decisions, multiple discrete-continuous, hybrid choice, dynamic models; (V) Specification, Estimation and Inference — frequentist numerical optimization, Bayesian estimation, endogeneity, sampling; (VI) Analysis and Use — appraisal and forecasting. For an estimation-focused course, Part V is the core payload, with Part III (heterogeneity) and Ch 15 (ordered probit/logit) close behind. Chapters are survey-style with "inner workings" depth rather than software tutorials.

## Chapter-by-chapter index

### Ch 1: Introduction to the Handbook of Choice Modelling — Hess & Daly (PDF pp. 8–11)
Editors' overview: motivates choice modelling for valuation and forecasting across disciplines, notes the growing engagement with behavioural economics and machine learning since the first edition, and walks through the volume's structure with one-paragraph previews of every chapter.
**Relevant to book chapters on:** choice framework (context/motivation only).

### Ch 2: The new science of pleasure: consumer choice behavior and the measurement of well-being — Daniel McFadden (PDF pp. 12–54)
McFadden's sweeping essay tracing utility from Bentham/Edgeworth through neoclassical duality (expenditure/indirect utility functions, Hicksian demand) to random utility models and behavioural/well-being measurement. Gives the formal consumer-theory scaffolding (U(x,z,r), taste heterogeneity via primitive characteristics r) that underlies RUM. Excellent for framing why choice models are utility-theoretic, though not an estimation chapter.
**Relevant to book chapters on:** choice framework.

### Ch 3: Psychological research and theories of preferential choice — Hotaling, Busemeyer & Rieskamp (PDF pp. 55–79)
Reviews behavioural findings (preference instability, context effects) and psychological process models, focusing on evidence-accumulation/sequential-sampling theories of choice. Useful contrast to RUM but peripheral to estimation.
**Relevant to book chapters on:** choice framework (behavioural caveats).

### Ch 4: Model building, inference and interpretation: developing discrete choice models in the age of machine learning — Rodrigues, Krueger & Pereira (PDF pp. 110–151; note: physically *after* Ch 5 in this PDF)
A practical, tutorial-style guide to when/where ML methods help in a discrete choice workflow, organized around Box's loop (design–data–model–criticism). Discusses representing MNL as a neural network and mixed logit as a probabilistic graphical model, cross-validation, and available packages. One of the more hands-on chapters.
**Relevant to book chapters on:** choice framework / MLE (model criticism, out-of-sample validation).

### Ch 5: Choice context — Goulias & Pendyala (PDF pp. 80–109; physically *before* Ch 4 in this PDF)
Defines choice context along time (life course), space, and social dimensions and discusses how to accommodate context in data collection and models. Transport/travel-behaviour oriented; low priority for estimation.
**Relevant to book chapters on:** choice framework (marginal).

### Ch 6: Self-tracing and reporting: state-of-the-art in the capture of revealed behaviour — Axhausen (PDF pp. 152–176)
Surveys revealed-preference data capture: travel diaries, GPS/smartphone tracking, mobile-phone records, and the biases of each. Data-collection oriented.
**Relevant to book chapters on:** organizing choice data (RP data provenance; marginal).

### Ch 7: Designing and conducting stated choice experiments — Bliemer & Rose (PDF pp. 177–210)
Extensive, authoritative overview of experimental design for stated choice surveys: orthogonal vs efficient (D-error) designs, attribute/level selection, pilot studies, implementation. The key reference chapter for how conjoint/CBC design decisions upstream affect the data the book's estimation chapters consume.
**Relevant to book chapters on:** conjoint practice / simulating data (design matrices) / organizing choice data.

### Ch 8: Best-worst scaling: theory and methods — Marley (PDF pp. 211–250)
Theory and models for the three BWS cases (object, profile, multi-profile), including maxdiff-type models, score properties, and links to ranking models. Directly relevant if the book touches MaxDiff; otherwise background.
**Relevant to book chapters on:** conjoint practice / building likelihoods (best-worst likelihood forms).

### Ch 9: Real choices and hypothetical choices — Harrison (PDF pp. 251–280)
Critical examination of hypothetical bias: whether unconsequential (stated) choices reveal the same preferences as consequential (real) ones, and what mitigation approaches achieve. Useful caveat material for conjoint chapters.
**Relevant to book chapters on:** conjoint practice.

### Ch 10: Virtual reality and choice modelling — van Eggermond, Mavros & Erath (PDF pp. 281–311)
Reviews use of virtual environments/VR as stimuli in stated preference studies. Peripheral.
**Relevant to book chapters on:** conjoint practice (marginal).

### Ch 11: Nonparametric approaches to describing heterogeneity — Fosgerau (PDF pp. 332–342; physically *after* Ch 12 in this PDF)
Compact but high-value chapter on estimating random-coefficient (mixed) discrete choice models when the mixing distribution F is left unspecified. Covers: (2.1) the Fosgerau–Bierlaire sieve approach — approximate the unknown density by a flexible series (polynomial) expansion around a base distribution, which nests a test of any parametric mixing distribution; (2.2) mixtures-of-distributions (finite mixture) approximations, connecting to Train (2016)-style flexible mixtures; (2.3) combining sieves with a copula for multivariate heterogeneity; and (3) regression-based nonparametric approaches for binary choice with and without covariates. Directly relevant to justifying/testing normal vs. lognormal mixing assumptions in mixed logit.
**Relevant to book chapters on:** mixed logit / drawing densities / latent class (finite-mixture connection).

### Ch 12: Attribute processing as a behavioural strategy in stated preference choice making — Hensher & Balbontin (PDF pp. 312–331; physically *before* Ch 11)
Overview of attribute non-attendance and processing heuristics as a source of apparent preference heterogeneity in SP data, and modelling approaches (often latent-class-based) to capture them.
**Relevant to book chapters on:** latent class / conjoint practice.

### Ch 13: Alternative decision rules in (travel) choice models — Chorus & van Cranenburgh (PDF pp. 343–375)
Review and critique of non-RUM decision rules (random regret minimization, elimination-by-aspects, satisficing, etc.), their econometric implementation, and pitfalls of paradigm-shopping. Background for a "the likelihood embodies a decision rule" discussion.
**Relevant to book chapters on:** building likelihoods (alternative behavioural kernels) / choice framework.

### Ch 14: Latent class structures: taste heterogeneity and beyond — Hess (PDF pp. 376–395)
Focused treatment of latent class (discrete mixture) logit as the main competitor to continuous mixed logit for random heterogeneity. Section 2 contrasts LC and continuous mixed logit methodologically (specification, estimation burden, simulated likelihood vs closed-form class-weighted likelihood, interpretation); Section 3 covers hybrid "latent-class mixed logit" (discrete–continuous mixtures); Section 4 covers confirmatory LC uses — attribute-processing strategies, decision-rule heterogeneity (mixing different model types across classes), and model averaging. Highly relevant for a latent-class chapter and for the EM-vs-gradient/label-switching discussion.
**Relevant to book chapters on:** latent class / mixed logit / building likelihoods.

### Ch 15: Models for ordered choices — Greene (PDF pp. 396–428)
Thorough survey of ordered probit/logit from the latent-regression viewpoint: threshold parameters, partial effects, generalized/heterogeneous-threshold models, random-parameter and panel extensions. Notes estimation via quadrature, Halton draws, and maximum simulated likelihood for the mixed variants (~83 probit mentions; simulation methods discussed). Useful if the book covers ratings-type outcomes or as a probit-family complement to MNP.
**Relevant to book chapters on:** MNP (latent-variable formulation) / MLE / simulation-assisted estimation.

### Ch 16: Activity and transportation decisions within households — de Palma, Picard & Lindsey (PDF pp. 429–454)
Models for joint decisions by multiple household members (unitary vs collective models). Transport-specific; low priority.
**Relevant to book chapters on:** choice framework (marginal).

### Ch 17: Multiple discrete-continuous choice models — Pinjari, Bhat, Saxena & Mondal (PDF pp. 455–491)
Reflective survey of MDC models (notably Bhat's MDCEV): utility-theoretic structures where consumers choose multiple alternatives and continuous quantities, vs "reduced-form" discrete+continuous equation systems. Relevant only if the book extends to volumetric/menu-choice models.
**Relevant to book chapters on:** building likelihoods (Kuhn-Tucker/MDCEV likelihoods; optional).

### Ch 18: Hybrid choice models — Abou-Zeid & Ben-Akiva (PDF pp. 492–524)
Framework integrating discrete choice with latent-variable (structural equation) models to incorporate attitudes/perceptions; discusses four classes of advantages over choice-only models.
**Relevant to book chapters on:** building likelihoods (joint likelihoods with latent variables; optional).

### Ch 19: Hybrid choice models: the identification problem — Vij & Walker (PDF pp. 525–570)
Companion chapter on identification of ICLV/hybrid models — when latent-variable augmentation is empirically distinguishable and what normalizations are needed. Longest chapter in the book; specialist material.
**Relevant to book chapters on:** building likelihoods (identification logic transfers to MNP scale/level normalization).

### Ch 20: Dynamic choice models — Bierlaire, Frejinger & Hillel (PDF pp. 571–595)
Models for sequential choices with state dependence, learning, and forward-looking behaviour (dynamic discrete choice); requires panel data. Background for panel-data discussions.
**Relevant to book chapters on:** organizing choice data (panel structure) / building likelihoods (optional).

### Ch 21: Numerical methods for optimization-based model estimation and inference — David S. Bunch (PDF pp. 596–631) — HIGH PRIORITY
The frequentist estimation-engine chapter, written to explain "how and why the methods work" — precisely the ground the book's MLE/optimization chapters cover. Structure: Sec 2 mathematical preliminaries bridging econometrics and numerical-analysis notation; Sec 3 estimators for discrete choice models — MLE as one instance of extremum/M-estimators, a generalized estimation framework, statistical properties (consistency, asymptotic normality, sandwich/robust covariance), and computational implications (Sec 3.1–3.4); Sec 4 unconstrained minimization based on Newton's method — features of Newton's method, global strategies (line search: 16 mentions; trust regions: 22 mentions), local strategies (quasi-Newton/BFGS: 9+, Gauss-Newton, BHHH: 15 mentions as the statistics-specific Hessian approximation), computer arithmetic and finite differences (Sec 4.4 — why numerical gradients fail and how step size matters), and stopping rules (Sec 4.5 — gradient-based convergence criteria). Explicitly covers simulation/quadrature-based probabilities (mixed logit, MNP) as the expensive inner loop of the iterative search, and mentions software including R packages and Apollo. This is the single best companion reading for chapters on MLE and optimization (optim/maxLik mechanics, why BHHH ≈ outer-product-of-gradients, standard errors from the Hessian).
**Relevant to book chapters on:** MLE / optimization / simulation-assisted estimation / MNP / mixed logit / software.

### Ch 22: Bayesian estimation of random utility models — Peter Lenk (PDF pp. 632–669) — HIGH PRIORITY
The Bayesian workhorse chapter, framed around conjoint data — the same marketing setting as the book. Sec 1 historical intro tying conjoint (Luce & Tukey 1964; Green & Rao 1971), RUT (McFadden 1974), and Bayesian decision theory (Savage), with the classic "broad and shallow data" argument for hierarchical Bayes over two-stage estimation (shrinkage/partial pooling; Lenk et al. 1996, Allenby & Lenk 1994/95, Allenby & Rossi 1998). Sec 2 "Basically Bayes" — priors, posteriors, loss functions. Sec 3 numerical approximations — Monte Carlo simulation, importance sampling, MCMC, Gibbs sampling, and Metropolis-Hastings including the random-walk MH algorithm spelled out step-by-step. Sec 4 hierarchical Bayes models for conjoint data — heterogeneity distributions, HB (metric) regression, HB ordinal probit, HB probit with full conditionals via data augmentation of latent utilities (Albert-Chib style), and HB logit — i.e., exactly the model ladder of a hierarchical-Bayes MNL chapter. Sec 5 Bayesian hypothesis testing and model selection (Bayes factors, marginal likelihoods). Notes commercial (Sawtooth, SAS) and free implementations (R, WinBUGS). The closest thing in the handbook to a blueprint for the book's Bayes/MCMC chapters.
**Relevant to book chapters on:** Bayes-MCMC / mixed logit (HB random coefficients) / MNP (data augmentation) / drawing densities / conjoint practice / software.

### Ch 23: Endogeneity in discrete choice models — Guevara (PDF pp. 670–694)
Authoritative treatment of endogeneity: five causes (omitted attributes, measurement error, simultaneity, etc.), consequences for consistency, and corrections (control function, BLP-style approaches, latent variables). Important econometric caveat material, secondary to estimation mechanics.
**Relevant to book chapters on:** MLE (consistency assumptions) / choice framework.

### Ch 24: Sampling and discrete choice — Bierlaire & Krueger (PDF pp. 695–720)
Covers both (a) sampling of observations — estimation under exogenous vs choice-based/endogenous sampling, with maximum likelihood, conditional maximum likelihood, and WESML (weighted exogenous sampling MLE) estimators, plus implications for prediction and elasticities; and (b) sampling of alternatives — consistent estimation of MNL (and corrections beyond MNL, via MH-type importance ideas) when the choice set is too large to enumerate. Includes numerical experiments (Biogeme). Practically relevant when organizing choice data with large choice sets or stratified samples.
**Relevant to book chapters on:** organizing choice data / MLE / building likelihoods.

### Ch 25: Appraisal — Karlström (PDF pp. 721–746)
Welfare economics with random utility models for cost-benefit analysis: logsum-based consumer surplus, rule-of-half, WTP measures, extensions to mixed logit. Useful for a "what do you do with estimates" section (WTP computation).
**Relevant to book chapters on:** choice framework (post-estimation: WTP/welfare).

### Ch 26: Forecasting choice — Daly (PDF pp. 747–~766)
Practitioner-oriented treatment of using estimated choice models for aggregate forecasting: sample enumeration, aggregation, transferability, uncertainty. Post-estimation material.
**Relevant to book chapters on:** choice framework (post-estimation: prediction/market simulation).

## Most useful chapters for this project
1. **Ch 22 (Lenk, Bayesian estimation of RUMs)** — a near-exact template for the book's Bayes/MCMC chapters: Monte Carlo → importance sampling → Gibbs → MH, then HB regression/ordinal probit/probit (data augmentation)/logit for conjoint data, plus the broad-and-shallow shrinkage argument. Cite throughout hierarchical-Bayes material.
2. **Ch 21 (Bunch, numerical methods)** — the definitive companion for the MLE and optimization chapters: extremum/M-estimator theory, Newton/quasi-Newton/BFGS/BHHH, line search vs trust region, finite-difference pitfalls, stopping rules, and why simulated probabilities (MNP, mixed logit) make the search expensive.
3. **Ch 14 (Hess, latent class)** — the best single source contrasting latent class with continuous mixed logit (closed-form vs simulated likelihood) and covering LC-mixed hybrids; anchors a latent-class chapter.
4. **Ch 11 (Fosgerau, nonparametric heterogeneity)** — short and dense; justifies and tests mixing-distribution choices in mixed logit (sieves, finite mixtures, copulas); pairs with Train (2016) already in lit/.
5. **Ch 7 (Bliemer & Rose, stated choice design)** — the upstream design reference for any simulated-conjoint or CBC data used in examples.
6. **Ch 24 (Bierlaire & Krueger, sampling)** — WESML/choice-based sampling and sampling of alternatives; directly useful for organizing-choice-data and likelihood chapters with big choice sets.
7. **Ch 15 (Greene, ordered choices)** — clean latent-variable exposition of ordered probit/logit with quadrature/Halton/MSL estimation of mixed variants; a natural bridge to the MNP chapter.
