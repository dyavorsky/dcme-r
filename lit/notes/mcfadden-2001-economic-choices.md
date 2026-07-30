# McFadden (2001) — Economic Choices

**Full citation:** McFadden, Daniel (2001), "Economic Choices," *The American Economic Review*, 91(3), 351–378. (Revised version of the Nobel Prize lecture delivered in Stockholm, December 8, 2000.)
**Type:** Nobel lecture / survey article
**Length:** 28 journal pages (pp. 351–378; PDF has 29 pages incl. JSTOR cover — journal p. 351 = PDF p. 2)

## One-paragraph summary

McFadden's Nobel lecture surveys the microeconometric analysis of discrete choice from its origins to circa 2000. He traces the intellectual history — Thurstone's Law of Comparative Judgment, Marschak's Random Utility Maximization (RUM) formulation, Luce's IIA axiom — to his own 1965 derivation of the conditional (multinomial) logit model and its RUM foundations, the nested MNL and GEV family, and the celebrated BART travel-demand forecasting application. He then reviews modern refinements: the standard model of the choice process, RUM-consistent families (GEV, MNP, mixed MNL), the McFadden–Train result that MMNL (or latent class models) can approximate any well-behaved RUM model, willingness-to-pay estimation, dynamics, and a long section on cognitive psychology's challenges to the standard model (anchoring and stated-WTP biases). A final section surveys statistical methods specific to choice analysis: choice-based sampling, simulation-assisted estimation (MSM, MSS, GHK, MCMC, Halton draws), and specification testing for IIA and for mixing.

## Key contributions relevant to the book

- The definitive origin story and conceptual motivation for the MNL model and its RUM interpretation — ideal framing material for the book's opening chapter.
- Compact, authoritative statements of: the MNL formula, GEV generating functions and nested MNL via inclusive values, the MNP tradeoff (flexibility vs. open-form integrals), and the MMNL approximation theorem.
- A concise history-plus-user's-guide to simulation-assisted estimation (kernel-logit smooth simulators, MSM, Method of Simulated Scores, Gibbs/Metropolis–Hastings, Halton sequences) with practical guidance on simulation error and sandwich covariance matrices.
- Easy-to-implement specification tests: Hausman–McFadden IIA test, McFadden (1987) regression-based test, and the artificial-variable LM test for unobserved mixing (precursor/companion to McFadden–Train 2000).
- Empirical exemplars for teaching: the pre/post-BART prediction-success table and Train's Montana trout-fishing MMNL model with WTP computation.

## Models & notation

- MNL / conditional logit: P_C(i) = exp(V_i)/Σ_{k∈C} exp(V_k), V_k a "systematic utility" linear in attributes (eq. 1, p. 353). Naming history — "conditional logit" vs. now-standard "multinomial logit" (p. 354).
- Luce's IIA axiom: P_C(i)/P_C(j) constant across choice sets containing both; implies strict utilities; Marschak: IIA implies RUM (p. 353).
- RUM consistency of MNL iff additive disturbances are i.i.d. Extreme Value Type I (p. 354); Axiom of Revealed Stochastic Preference (ARSP) as the general necessary/sufficient condition for RUM consistency (p. 354).
- Nested MNL: separable utility trees, inclusive values carrying lower-level impacts upward; the exact "log sum" formula credited to Ben-Akiva (1972) (p. 354).
- Canonical RUM with economic content: U = V + η, V = [α·(a−c)/w − β·t]·w^θ + z(x,s)·γ — nonwage income a, alternative cost c, wage w, time t (eq. 2, p. 357); consumer heterogeneity as a continuous random field transformed to uniform variates (pp. 356–357).
- GEV family: generating function H(w_1,...,w_J) nonnegative, linear homogeneous, → +∞, alternating mixed partials; F = exp(−H(e^{−η_1},...,e^{−η_J})) is a joint EV distribution; E max u_i = log H(e^{V_1},...,e^{V_J}) + ζ (Euler's constant); choice probabilities P_C(i) = e^{V_i} H_i(·)/H(·) (eq. 3, p. 358). Recursive construction H^C = (H^A)^{1/s} + H^B with 1/s the inclusive value coefficient generating nested MNL (p. 358).
- Williams–Daly–Zachary results: EV scale-decomposition of random variables; expected max utility behaves as representative-consumer indirect utility with price derivatives proportional to choice probabilities; range restrictions on inclusive value coefficients for RUM consistency (p. 359).
- MNP: RUM with additive normal disturbances, general covariance — flexible but choice probabilities are open-form multivariate integrals; factor-analytic covariance restrictions for tractability (p. 359).
- MMNL (mixed MNL): P_C(i) = ∫ [e^{Z_i·α(ε)}/Σ_j e^{Z_j·α(ε)}] dε over uniform ε — a MNL with randomly varying coefficients; every MMNL is RUM-consistent, and any regular RUM-consistent choice probability can be approximated by MMNL (eq. 4, p. 359, citing McFadden–Train 2000). Latent class model = mixing distribution with finite support; interpretable as a single hidden-layer feedforward neural network (p. 360).
- WTP in MMNL: mean WTP = E_{α,β,γ} (1/α) log[(Σ e^{V″})/(Σ e^{V′})] — the expected log-sum formula (eq. 5, p. 360); Hicksian/Marshallian coincidence when utility is linear in income; MCMC methods for exact WTP otherwise (p. 360).
- Choice-based sampling framework: population cell probabilities P(y|z)p(z) (Table 7, p. 370); qualification factors R(z,y,s), propensity scores; conditional maximum likelihood (CML) of Manski–McFadden; for MNL, endogenous sampling shifts only alternative-specific constants by log(...) factors while slope parameters remain consistently estimated (p. 370).

## Estimation details

- **Maximum likelihood as the workhorse:** "Applied RUM analysis... has generally relied on maximum-likelihood methods," with growing use of bootstrap, GMM, and simulation methods (p. 368). MNL estimation was a "nontrivial task" in the 1960s (p. 354).
- **Choice-based sampling (pp. 368–370):** random-sample estimators are inconsistent/inefficient under endogenous stratification; solutions re-weight observations (as-if random) or re-weight the probability model; Manski–Lerman (1977) seminal treatment; CML method (Manski–McFadden 1981); enriched samples; for MNL with known qualification probabilities, only intercepts need adjustment — slopes β_y consistent without further correction (p. 370).
- **Computation and simulation (p. 371):** simple MNLs are "virtually instantaneous"; nested MNL solvable with general-purpose ML programs "although achieving and verifying convergence... remains an art"; unrestricted MNP "continues to resist conventional computation." Simulation-based estimation formalized in McFadden (1989); library expanded to include Gibbs, Metropolis–Hastings and other MCMC samplers, pseudo-random and patterned (Halton, Sobel) sequences, Method of Simulated Moments, Method of Simulated Scores, simulated EM.
- **Kernel-logit (MMNL) smooth simulator (p. 371):** parameterize α(ε, θ) with ε uniform (easy for multivariate normal, lognormal, truncated normal coefficients); draw a simulation sample of size R (random or Halton), *fix the draws for all subsequent analysis*, and treat P_C(i) = E_R exp(Z·α(ε_r,θ))/Σ_j exp(...) as exact. Gives positive, unbiased, smooth simulators of probabilities and derivatives. Rate requirement: R rising faster than √(sample size) suffices to make simulation error negligible for ML or MoM. Use the sandwich covariance formula to avoid misleading precision when R is moderate (cites McFadden–Train 2000). If the inverse transformation α(ε,θ) is intractable, use importance sampling or Metropolis–Hastings (p. 371).
- **IIA specification tests (p. 372):** Hausman–McFadden (1984) — estimate MNL on full set C and on subset A; quadratic form (β_C − β_A)'(Ω_A − Ω_C)^{-1}(β_C − β_A) asymptotically chi-square under IIA; care needed dropping components so Ω_A − Ω_C is nonsingular. McFadden (1987) regression-based test: add constructed variables z_i = log(P_A(i)) − Σ_{j∈A} P_A(j)log(P_A(j)) for subsets A; LR test of the z's ≈ score/LM test against a nested MNL alternative; 1 − coefficient of z interpretable as a preliminary inclusive-value estimate for nest A (p. 372).
- **Test for mixing (pp. 372–373):** artificial variables z_ti = (x_ti − x̄_tC)²/2 with x̄_tC = Σ_j x_tj P_C(j); re-estimate base MNL with the z's added; Wald or LR test asymptotically equivalent to LM test of no mixing against MMNL. Requires only base MNL estimation — no simulation. Generalized in McFadden–Train (2000) to testing an estimated MMNL against additional mixing.
- **Dynamics (p. 361):** panel data, state dependence, Heckman's initial-values problem and recursive structure — pointer to Heckman (1981a,b).
- **Stated preference / conjoint and data combination (p. 373):** experimental SP data, combining RP and SP via MIMC-style latent-variable models with a hidden layer mapping to discrete responses (McFadden 1986; Ben-Akiva–Morikawa); calibration of SP to RP usually needed.

## Relevance to book chapters

- **Choice framework (ch. 1):** the core reading — history of RUM, IIA, MNL derivation, the choice-process diagram, consumer-theory foundations (pp. 351–358). Section III (psychology, pp. 362–368) offers perspective on the model's behavioral limits.
- **Drawing densities (ch. 2):** inverse-CDF/uniform-transformation logic (Y = F^{-1}(v), p. 357) and the uniform-random-field representation underlying MMNL simulation.
- **MLE (ch. 4) / Optimization (ch. 5):** perspective on ML as the standard estimator; convergence "remains an art" for nested/nonlinear models (p. 371).
- **Bayes-MCMC (ch. 8):** Gibbs and Metropolis–Hastings samplers as part of the simulation toolkit; MCMC computation of exact WTP (pp. 360, 371).
- **MNP (ch. 9):** the MNP flexibility/tractability tradeoff, factor-analytic covariance restrictions, and why simulation rescued it (p. 359).
- **Nested logit / GEV (chs. 10–11):** inclusive values and log-sum (p. 354); GEV generating functions, recursion, and RUM-consistency proofs; Williams–Daly–Zachary results (pp. 358–359).
- **Simulation-assisted estimation (ch. 12):** the p. 371 discussion is a compact syllabus — MSM, MSS, GHK-adjacent simulators, Halton/Sobel sequences, fixed draws, R vs. √N rate, sandwich covariance.
- **Latent class (ch. 13):** finite-support mixing = latent class; sieve/neural-network interpretation and nonparametric approximation of RUM (p. 360).
- **Mixed logit (ch. 14):** MMNL approximation theorem (eq. 4), Train's trout-fishing application with normal/lognormal coefficient distributions (Tables 2–3, pp. 360–361), WTP formula (eq. 5), and the mixing specification test (pp. 372–373).
- **Simulating data (ch. 3):** the BART prediction-success table (Table 1, p. 355) illustrates out-of-sample validation of a fitted choice model.

## Page pointers

(journal page numbers; PDF page = journal page − 349)
- p. 351: overview; representative-agent tradition vs. microdata
- p. 353: Thurstone, Marschak RUM, Luce IIA; MNL formula (eq. 1)
- p. 354: conditional logit naming; RUM foundations (i.i.d. EV1 iff); ARSP; nested MNL, inclusive values, Ben-Akiva log-sum
- p. 355: BART forecasting application, prediction success Table 1; disaggregate RUM beats aggregate gravity models
- p. 356: Figure 2 choice-process diagram; standard model fundamentals
- p. 357: heterogeneity as continuous random field; uniform transformation; canonical indirect utility (eq. 2)
- p. 358: limits of IIA ("red bus, blue bus"); GEV generating functions and choice probabilities (eq. 3); nested MNL recursion, inclusive value coefficient
- p. 359: Williams–Daly–Zachary; MNP open-form problem; MMNL representation (eq. 4)
- p. 360: latent class / neural-net approximation; MMNL history (Boyd–Mellman, Cardell–Dunbar); WTP expected log-sum (eq. 5); Montana trout-fishing study
- p. 361: Tables 2–3 — MMNL fishing-site model, lognormal/normal coefficient distributions, elasticities; dynamics (Heckman)
- p. 362: dynamic models, endogeneity in thin markets; discrete/continuous choice (Dubin–McFadden)
- pp. 363–368: psychology of choice — cognitive illusions, anchoring experiments, stated-WTP bias (Tables 4–6)
- p. 368: Section IV statistical methods overview; choice-based sampling introduced
- p. 369: sampling framework, qualification factors, propensity scores
- p. 370: Table 7 population cell probabilities; CML; MNL intercept-shift result under endogenous sampling
- p. 371: computation & simulation — MSM, MSS, MCMC, Halton; kernel-logit smooth simulator; R vs. √N; sandwich covariance
- p. 372: IIA tests — Hausman–McFadden quadratic form; McFadden (1987) regression-based/LM test
- p. 373: mixing LM test via artificial variables; market research, SP data, conjoint analysis; conclusions begin
- pp. 374–378: references
