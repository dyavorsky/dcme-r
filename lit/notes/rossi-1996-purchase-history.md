# Rossi, McCulloch & Allenby (1996) — The Value of Purchase History Data in Target Marketing

**Full citation:** Rossi, P. E., McCulloch, R. E., & Allenby, G. M. (1996). "The Value of Purchase History Data in Target Marketing." *Marketing Science*, 15(4), 321–340.

**Type:** Methodological + applied journal article (hierarchical Bayes MNP with demographic-driven heterogeneity; decision-theoretic valuation of information)
**Length:** 20 pages (journal pp. 321–340)

## One-paragraph summary

The showcase application of hierarchical Bayes choice modeling: how much is household-level information worth for target marketing? The authors specify a random-coefficient multinomial probit (diagonal error covariance, avoiding IIA) in which each household's coefficient vector β_h has mean Δz_h driven by demographics plus normal unobserved heterogeneity, estimate it via a 5-block Gibbs sampler (extending McCulloch & Rossi 1994), and then compute household-level posterior/predictive distributions of β_h under five nested information sets: base (population distribution only), demographics, choices-only, one observation (choice + causal), and full purchase history. A stylized target-couponing problem (choose the coupon face value maximizing expected net revenue, integrating over the posterior of β_h rather than plugging in point estimates) converts information into dollars. Findings: demographics explain only 7–33% of parameter variation (7% for price sensitivity); full-history targeting yields 2.5× the revenue gain of blanket couponing; even a single observation yields a 50% gain; and a continuous (normal) heterogeneity model dominates a finite-mixture (latent class) alternative for household-level inference (Appendix B). Uses A.C. Nielsen tuna scanner panel: 400 households, 5 brands, ~13 purchases per household.

## Key contributions relevant to the book

- A complete, appendix-level specification of a hierarchical MNP Gibbs sampler with demographics in the upper level — the model implemented in `bayesm::rhierMnpGibbs`/`rhierLinearModel`-style code (Appendix A, pp. 338–339, is essentially pseudocode).
- The definitive demonstration of household-level inference from tiny T: posterior boxplots of β_h under different information sets (Figs. 1–2) show how the hierarchical prior shrinks and how information sharpens posteriors.
- Decision theory with MCMC output: optimal coupon face value maximizes expected revenue averaged over the posterior of β_h; plug-in point estimates create "overconfident" strategies because the profit function is nonlinear (pp. 333–334; Figs. 3–4).
- Predictive distributions built by compounding Gibbs draws (Eqs. 6–8) — a clean teaching example of computing ∫p(β|θ)p(θ|Data)dθ by simulation.
- Continuous vs. finite-mixture heterogeneity comparison (Appendix B, pp. 339–340): 3-mass-point model chosen by BIC; continuous mixture improves log-likelihood by ~100% (−1170 vs −2036) and gives more reasonable household estimates (mixture posteriors confined to the simplex of mass points; Fig. 6).
- The "observable vs. unobservable heterogeneity" decomposition: ρ² = 1 − Var(ε)/Var(β) per coefficient (p. 330, Table 4) — demographics explain little, motivating unobserved heterogeneity.

## Models & notation

- Latent-utility multivariate regression (Eq. 1, p. 323): y_ht = X_ht β_h + ε_ht, ε_ht ~ N(0, Λ), m brands; X_ht = [D_m, p, d, f] (brand intercepts with first set to zero, log price, display, feature). Choice I_ht = index of max of y_ht. Censoring mechanism: I_ht | y_ht and y_ht | X_ht, β_h, Λ (Eq. 2).
- Error structure: Λ diagonal m×m with λ₁₁ = 1 for identification — an "independence probit"; simplifies choice-probability calculation while unobserved heterogeneity induces Hausman–Wise-type correlation; avoids IIA (p. 323).
- Heterogeneity (Eq. 3, p. 323): β_h = Δ z_h + v_h, v_h ~ iid N(0, V_β); z_h = intercept + d−1 demographics (income, family size, retired, unemployed, single mom); Δ is k×d. Comparing marginal variance of β_h with V_β separates observable from unobservable heterogeneity.
- Hierarchical model as conditional distributions (Eq. 4): I_ht | y_ht; y_ht | X_ht, β_h, Λ; β_h | z_h, Δ, V_β.
- Priors (p. 324 and Appendix A, p. 339):
  - Λ = diag(σ₁²,…,σ_m²), σ_i ~ independent Inverted Gamma(ν, √v_i), ν = 3, v_i = 1.0, σ₁ = 1 fixed.
  - V_β⁻¹ ~ Wishart(ν_bo, V_bo) with ν_bo = k + 4 (= 11) and V_bo = ν_bo I_k — proper but diffuse, "little shrinkage of β_h toward the common subspace Δz_h."
  - δ = vec(Δ) ~ N(d̄, V_β ⊗ A_d⁻¹) — natural conjugate for multivariate regression; d̄ = 0, A_d = 0.01 I_d.
- Information sets (Section 4, Table 1, pp. 325–328): Base (predictive distribution integrating over empirical distribution of z_h and posterior of Δ, V_β; Eqs. 6–7); Demographic (condition on z_h′; Eq. 8); Choices-only (no causal variables — requires mapping the reduced model's intercepts μ to full parameters via γ + Rδ ≡ μ and conditional MVN theory, Eqs. 9–16, pp. 326–327); One observation; Full.
- Target couponing (Section 7, pp. 333–334): coupon = temporary price cut of face value F; expected net revenue π_F = Pr(i | β_h, Λ, price − F, X)(M − F), margin M = $0.35; choose F (multiples of 5¢, possibly 0) to maximize E[π_F] over the posterior of β_h (Eqs. 17–18); aggregate net revenue Π averages π over households (Eq. 19, p. 337).

## Estimation details

**Gibbs sampler (Section 3, p. 324, Eq. 5; exact conditionals in Appendix A, p. 339).** Five blocks, extending McCulloch & Rossi (1994):

1. **y_ht | I_ht, β_h, Λ, X_ht** (data augmentation): truncated m-dimensional multivariate normal, y ~ trunc-N(Xβ, Λ) with y_I > y_k for all k ≠ I. Drawn by "Gibbsing through" the m components as truncated univariate normals: for k = I draw y_k ~ TN(μ_k, σ_k; y_k > max(y_−k)), else y_k ~ TN(μ_k, σ_k; y_k < max(y_−k)) — pseudocode loop given verbatim in Appendix A (p. 339). Households and observations conditionally independent, so drawn one at a time.
2. **β_h | y_h, Λ, Δ, V_β**: standard Bayesian linear regression with known covariance and normal prior; premultiply by Λ^(−1/2) to standardize, then β_h ~ N(b̄_h, (X_h′X_h + V_β⁻¹)⁻¹) with b̄_h = (X_h′X_h + V_β⁻¹)⁻¹[X_h′X_h β̂_h + V_β⁻¹ β̄_h], β̄_h = Δz_h, β̂_h = (X_h′X_h)⁻¹X_h′y_h (Appendix A, II).
3. **Λ | y, {β_h}**: σ_i ~ Inverted Gamma(ν + n, sqrt((νv_i + ns_i²)/(ν + n))) where ns_i² = residual sum of squares from stacked e_h = y_h − X_h β_h (Appendix A, III). (σ₁ fixed at 1.)
4. **Δ | {β_h}, V_β**: δ = vec(Δ) ~ N(d̂, V_β ⊗ (Z′Z + A_d)⁻¹), with D̂ = (Z′Z + A_d)⁻¹(Z′ZD̃ + A_d D̄), D̃ = (Z′Z)⁻¹Z′B, B = H×k matrix of β_h′ rows, Z = H×d matrix of z_h′ rows (Appendix A, IV) — multivariate regression of {β_h} on demographics.
5. **V_β | {β_h}, Δ**: V_β⁻¹ ~ W(ν_bo + H, V_bo + S), S = Σ_h(β_h − β̄_h)(β_h − β̄_h)′, β̄_h = Δz_h (Appendix A, V).

**Why Bayes rather than simulated-likelihood classical methods** (p. 324): (1) targeting needs the household-level {β_h} directly, not just common parameters; (2) inference from a handful of observations per household demands exact finite-sample uncertainty, free of asymptotics (cf. Börsch-Supan & Hajivassiliou, Keane).

**Predictive computation** (pp. 325–327): all predictive distributions are simulated by compounding: draw (Δ, V_β) from Gibbs output, draw z_h′ from the empirical demographic distribution, then β_h′ ~ N(Δz_h′, V_β). Choices-only inference maps the reduced-model μ_h posterior into (γ_h, δ_h) via a conditional-normal step (Eq. 16) inside the draw loop (algorithm steps i–vi, p. 327).

**Diagnostics/notes:** the paper defers technical MCMC issues to McCulloch & Rossi (1994) and Gelman & Rubin (1992) (p. 324). Household posteriors displayed as 10th–90th percentile boxplots (Figs. 1–2). Figure 3 shows highly non-normal posteriors of choice probabilities — large-sample approximations inappropriate (p. 334). Plug-in E[R(β̄)] ≠ E[R(β)|F] due to nonlinearity (Fig. 4, pp. 334–335).

**Results (Section 8, Table 5, p. 337):** net revenue per household: Full 0.1570, Choices-only 0.1529, One-obs 0.1500, Demos-only 0.1467, Blanket 0.1459, No coupon 0.1380. Gains relative to blanket: Full 2.55×, Choices-only 1.93×, One-obs 1.56×, Demos-only 1.12×.

## Relevance to book chapters

- **HB-MNL / hierarchical models:** the canonical example of adding covariates to the upper level (β_h = Δz_h + v_h) — direct template for the Δ-matrix ("Z matrix") argument in `bayesm` hierarchical functions; the observable-vs-unobservable heterogeneity ρ² decomposition is a nice exercise.
- **MNP:** an applied hierarchical (independence) probit; Appendix A's Gibbs conditionals are the most code-ready statement of the sampler in this literature — ideal for translating into R alongside `rhierMnpGibbs`.
- **Bayes-MCMC intro:** predictive distributions by compounding draws (Eqs. 6–8) and the plug-in-vs-full-posterior decision theory (Figs. 3–4) illustrate why we keep draws rather than point estimates.
- **Latent class:** Appendix B is a citable head-to-head of finite mixture vs. continuous normal heterogeneity — continuous wins on fit and on household-level plausibility (mixture estimates confined to the convex hull of mass points).
- **Applications:** target couponing as a decision-theoretic use of posteriors; valuation of data/information sets is a memorable framing for why heterogeneity modeling matters commercially.

## Page pointers

- p. 321: abstract — information sets, 2.5× gain, 50% gain from one observation
- p. 322: motivation (Catalina checkout coupons, frequent-shopper data); need for finite-sample inference from as little as one observation
- p. 323: model — latent utilities (Eq. 1), censoring (Eq. 2), diagonal Λ with λ₁₁ = 1, heterogeneity regression (Eq. 3), hierarchical form (Eq. 4); continuous vs. finite-mixture heterogeneity discussion
- p. 324: priors (conjugate Δ | V_β normal, V_β inverted Wishart, Λ inverted gamma); reasons for Bayes over classical simulation estimators; Gibbs blocks (Eq. 5a–e)
- p. 325: base information set; predictive distribution via integration over z and (Δ, V_β) (Eqs. 6–7)
- p. 326: demographic set (Eq. 8); choices-only set setup (Eqs. 9–10)
- p. 327: mapping reduced-form μ to (γ, δ) (Eqs. 11–16); algorithm steps (i)–(vi); full information set
- p. 328: Table 1 information sets; data — Nielsen tuna panel, 400 households, 5 brands, avg 13 purchases (Table 2)
- p. 329: demographics (Table 3); posterior of Δ (Table 4) with posterior sign probabilities and unobserved-heterogeneity column
- p. 330: ρ² decomposition — demographics explain 7–33% of parameter variance; 7% for price
- pp. 331–332: Figs. 1–2 — household-level posteriors of C-O-S oil intercept and price coefficient across information sets
- pp. 333–334: target couponing model (Eqs. 17–18); plug-in overconfidence; Fig. 3 non-normal choice-probability posteriors
- p. 335: Fig. 4 posterior of expected revenue by face value; decision-theoretic choice
- p. 336: Fig. 5 optimal face-value distributions by information set
- p. 337: aggregate net revenue (Eq. 19); Table 5 value of information sets; conclusions
- pp. 338–339: Appendix A — priors and all five Gibbs conditionals (including truncated-normal loop pseudocode)
- pp. 339–340: Appendix B — finite mixture (BIC selects 3 mass points) vs. continuous mixture; Fig. 6 comparison; ~100% log-likelihood improvement
