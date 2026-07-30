# Allenby, Brazell, Howell & Rossi (2014) — Economic Valuation of Product Features

**Full citation:** Allenby, G.M., Brazell, J.D., Howell, J.R., & Rossi, P.E. (2014). Economic valuation of product features. *Quantitative Marketing and Economics*, 12(4), 421–456. DOI 10.1007/s11129-014-9150-x
**Type:** Journal article (methodology + empirical application: conjoint-based feature valuation via equilibrium profits)
**Length:** 36 journal pages (pp. 421–456; PDF file is 37 pages incl. cover sheet — PDF page = journal page + 1)

## One-paragraph summary

The paper argues that the only economically sensible measure of a product feature's value *to the firm* is the change in equilibrium profits between a market where the focal product has the feature and one where it does not: Δπ = π(p^eq, m^eq | A*) − π(p^eq, m^eq | A) (Eq. 2.1, p. 424). This requires a valid demand system (a heterogeneous logit calibrated on choice-based conjoint data), cost information, and an equilibrium concept (static Nash pricing). The authors contrast this profit-based metric with demand-side welfare measures — a "true" WTP based on compensating variation using the log-sum formula, and the widespread "pseudo-WTP" (part-worth divided by price coefficient), which they show has no rigorous basis as a measure of value. In a digital camera application (valuing a swivel-screen feature), the equilibrium approach yields a ~$34 increase in the focal brand's equilibrium price and ~36% profit increase, while mean E[WTP] is only ~$14.63 — economically large differences. The paper also delivers a set of practical prescriptions for conjoint design and HB estimation when the goal is economic valuation: include the outside option (dual-response), include major competing brands, enter price linearly (not dummy-coded), sign-constrain the price coefficient via log-reparameterization, use somewhat informative priors, and base all inference on the posterior predictive distribution of the part-worths rather than individual-level point estimates.

## Key contributions relevant to the book

- Defines the market/profit-based paradigm for feature valuation and shows why WTP (a social-surplus/welfare measure) and pseudo-WTP (β_feature/β_price) answer different questions and can be badly misleading (Sections 2.4, 6.2).
- Careful treatment of the random utility error as a genuine source of utility: WTP must account for the expected maximum utility (log-sum), not just deterministic part-worths (pp. 430–432).
- Clear statement of scaling/identification: setting the EV scale to 1 means the absolute value of the price coefficient is the reciprocal of the error scale; part-worths have arbitrary origin and scale, so they cannot be compared across respondents in ratio terms (pp. 427–428).
- Argues price should enter utility linearly and continuously (not as K−1 dummies), because dummy-coded price makes market demand non-continuous and can destroy existence of pure-strategy price equilibria (p. 426, fn. 3).
- Strong practical case for including the outside option (via dual response) — essential for substitution in/out of the category and valid equilibrium calculations (Section 3.2, pp. 434–435).
- Definitive statement of the "hyper-parameter, not individual betas" principle: averaging respondent-level MCMC draws (Eq. 4.2) and plugging into WTP formulas is invalid; the population object of interest is defined through the random-coefficient distribution and its posterior (Section 4.1, pp. 436–437).
- Prior sensitivity analysis for the sign-constrained price coefficient: the default diffuse IW prior implies an unreasonable implied prior on β_p; recommend ν = dim(β)+15 and diagonal V element of 0.5 for the log-price parameter (Section 4.2, pp. 438–439, Fig. 1).
- Sensitivity analyses: censoring respondents with near-random marginal likelihoods (cutoff 16·ln(0.4) = −14.66; drops ~29% of sample) yields larger elasticities and more realistic equilibrium prices (Section 6.3.1, pp. 451–452); mixture-of-normals heterogeneity reveals multi-modal price sensitivity that the normal model averages over (Section 6.3.2, pp. 452–454).

## Models & notation

- Random utility: u_j = β′a_j − β_p p_j + ε_j, ε_j Type I EV (Eq. 2.2, p. 426). Linear, compensatory utility; price entered linearly; attributes a_j include the focal feature a_f.
- Logit choice probability with scale set to 1: Pr(j) = exp(β′a_j − β_p p_j) / Σ_k exp(β′a_k − β_p p_k) (Eq. 2.3, p. 427).
- Aggregate demand: q_j(p) = M ∫ Pr(j|β, A, p) δ(β|Θ) dβ (p. 428). Market share as an integral over heterogeneity (Eq. 4.3, p. 436), with δ(β|Θ) = φ(β|μ, V_β) normal (Eq. 4.4, p. 437).
- Firm profit and Nash pricing: π(p_j|p_−j) = M·E[Pr(j|p, A)](p_j − c_j) (Eq. 2.4, p. 428); FOCs (Eq. 2.6) and equilibrium as zero of the system h(p) (Eq. 2.7, p. 429). Feature value: Δπ = π(p^eq, m^eq|A*) − π(p^eq, m^eq|A) (Eq. 2.1, p. 424).
- Indirect utility / welfare: V(p, y|A) = β_p y + ln Σ_j exp(a_j′β − β_p p_j) (Eq. 2.10, p. 431); social surplus W = y + ln[Σ exp(β′a_j − β_p p_j)]/β_p (Eq. 2.11, p. 432); WTP as compensating variation between choice sets A and A*: WTP = ln[Σ exp(β′a_j* − β_p p_j)]/β_p − ln[Σ exp(β′a_j − β_p p_j)]/β_p (Eq. 2.12, p. 432). Note WTP defined via V(p, y+WTP|A) = V(p, y|A*) (Eq. 2.9, p. 431).
- "Pseudo-WTP" = feature part-worth scaled by price coefficient; invariant to which product gets the feature, ignores error-based utility; rejected as a surplus measure (p. 432).
- Assumptions for equilibrium computation (Section 2.1, p. 425): (1) heterogeneous logit linear in attributes incl. price; (2) constant marginal cost; (3) single-product firms; (4) feature exclusivity; (5) no entry/exit; (6) static Nash price competition.

## Estimation details

- Hierarchical MNL: y_i | A_i, β_i ~ MNL; β_i ~ N(μ, V_β); (μ, V_β) ~ Normal–Inverted-Wishart conditionally conjugate prior (Eq. 4.1, p. 436). Estimated with bayesm routine `rhierMnlMixture`, 50,000 draws, 10,000 burn-in (p. 443).
- Sign constraint on price: reparameterize [β, β_p = ln(−β_p*)]′ ~ N(μ, V_β) (Eq. 4.7, p. 438) — implemented trivially inside the likelihood evaluation of the RW-Metropolis step. With this, tighten the prior: diagonal V element 0.5 for the log-price element and ν = dim(β) + 15 rather than the barely proper default ν = dim(β) + 5 (pp. 438–439, Fig. 1 shows implied priors).
- Posterior predictive distribution of part-worths: p(β|data) = ∫ φ(β|μ, V_β) p(μ, V_β|data) dμ dV_β (Eq. 6.1, p. 443) — symmetric but fatter-tailed than normal.
- Equilibrium computation: expectations approximated by simulation (>50,000 draws from the heterogeneity distribution); equilibrium found both by iterative best-response and by quasi-Newton root-finding on the FOC system, cross-checked (pp. 429–430). Posterior distribution of equilibrium prices/profits built by solving the equilibrium for each draw of the hyper-parameters (Eq. 4.6, p. 437).
- Empirical study: digital point-and-shoot cameras; 7 attributes (brand: Canon/Sony/Nikon/Panasonic; pixels; zoom; video; swivel screen; WiFi; price $79–279); 16 choice sets × 4 profiles; dual-response outside option; 501 completes → 469 analyzed (Section 6, p. 442).
- Key results: adding swivel screen to Sony raises its equilibrium price by $34.42 while competitors cut prices; share changes small; profit change +35.8% with competitive reaction vs. +92.9% naively assuming no reaction (Tables 2–3, Fig. 5, pp. 446–448); mean E[WTP] $14.63 (Eq. 6.3, Fig. 6, pp. 449–450), well below the equilibrium price change because ~50% of the market chooses the outside good.
- Censored-sample and mixture-of-normals sensitivity: Tables 4–7, pp. 451–454. Mixture model shows tri-modal price part-worth distribution; small mass of price-insensitive respondents drives equilibrium prices to implausible levels unless censored.

## Relevance to book chapters

- **Choice framework:** exemplary discussion of the role of the random utility error (utility source vs. measurement error), location/scale invariance, and interpretation of part-worths (pp. 426–428).
- **Utility specification:** linear-in-price argument vs. dummy-coded price; outside good needed for category expansion/contraction; connects directly to the budget-constraint issues in Allenby et al. (2015) and Pachali et al. (2022).
- **WTP and post-estimation:** the central reference for distinguishing pseudo-WTP (β/β_p), true WTP (compensating variation via log-sum), and equilibrium profit metrics; how to compute posterior distributions of any nonlinear function of parameters (elasticities Eq. 6.2, equilibrium prices, WTP).
- **HB-MNL:** concrete hierarchical spec with NIW prior, bayesm `rhierMnlMixture`, sign constraints via log-reparameterization, prior-tightening guidance, mixture-of-normals heterogeneity, marginal-likelihood-based respondent screening — all directly implementable in R.
- **Conjoint practice:** design prescriptions — include competing brands, outside option via dual response, wide realistic price variation, larger samples for equilibrium work; discussion of straight-liner removal and sample censoring.

## Page pointers

(Journal page numbers; add 1 for PDF page.)
- p. 424: Eq. 2.1 profit-based valuation definition
- pp. 425–426: assumptions; Eq. 2.2 utility; fn. 3 on why not to dummy-code price
- pp. 427–428: scaling/identification, part-worth interpretation; Eq. 2.3 logit; aggregate demand
- pp. 428–430: firm problem, Nash FOCs, computation of equilibria
- pp. 430–432: WTP theory; Eqs. 2.8–2.12; pseudo-WTP critique
- pp. 432–435: conjoint design for economic valuation; outside option / dual response debate
- pp. 435–439: HB model (Eq. 4.1); individual vs. market quantities (Eq. 4.2–4.6); price sign constraint (Eq. 4.7) and prior settings; Fig. 1
- pp. 442–450: camera application; bayesm estimation; Tables 1–3; Figs. 3–6; WTP computation (Eq. 6.3)
- pp. 451–454: sample censoring and mixture-of-normals sensitivity (Tables 4–7, Fig. 7)
- p. 455: conclusions
