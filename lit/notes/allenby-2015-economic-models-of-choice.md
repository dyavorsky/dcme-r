# Allenby, Kim & Rossi (2015) — Economic Models of Choice

**Full citation:** Allenby, G.M., Kim, J., & Rossi, P.E. (2015). Economic Models of Choice. Chapter 18 in *Handbook of Marketing Decision Models* (working-paper/SSRN version dated August 25, 2015; SSRN abstract 2650572). Published version: Springer, pp. 199–222 (2017).
**Type:** Handbook/review chapter on direct utility choice models
**Length:** 36 PDF pages (title + abstract + 34 numbered manuscript pages incl. appendix and references)

## One-paragraph summary

This chapter derives choice models from the primitive of *direct utility maximization subject to constraints*, arguing that the ubiquity of zeros in disaggregate marketing data is evidence of goal-directed, resource-constrained behavior. It starts with the standard discrete choice (logit) model as a linear direct-utility problem with a budget allotment E and an outside good, showing that with linear utility the budget cancels out of the choice probability — which is precisely why the workhorse MNL ignores budgets. It then develops the general "volumetric" model: log utility for inside goods with satiation parameter γ, linear (or nonlinear) outside good, Kuhn–Tucker first-order conditions mapping observed corner/interior demand to inequality/equality restrictions on the error terms, and a closed-form likelihood (products of EV densities for purchased goods and CDFs for non-purchased goods, times a Jacobian). Extensions cover nonlinear outside goods (which make E identified), multiple constraints (money and space/quantity), non-linear budget sets from quantity discounts (kinked budget sets, region-wise FOCs), correlated errors for similarity effects, indivisible (integer) demand, and a critique of indirect-utility (translog) approaches as unsuitable for marketing data with corner solutions and mass points. It is the theory backbone linking constrained optimization to the likelihoods estimated in choice modeling.

## Key contributions relevant to the book

- Cleanest available derivation of the standard MNL from a direct utility function with a budget constraint: u(x,z) = Σ_k ψ_k x_k + ψ_z z, choice among corner solutions, giving Pr(j) = exp[ψ_j − ψ_z p_j] / (1 + Σ_k exp[ψ_k − ψ_z p_k]) (Eq. 1, manuscript pp. 3–4). Makes explicit that (i) the price coefficient is the marginal utility of money ψ_z, common across alternatives; (ii) with linear utility the budget E cancels and only screens out options with p_k > E (p. 4–5).
- Motivates the whole "direct utility" agenda: utility (what is gained) separated from constraints (what is given up); zeros in data as corner solutions, not noise (Introduction, pp. 1–2; Conclusion, pp. 27–28).
- General volumetric model with satiation: Max u(x,z) = Σ_k (ψ_k/γ) ln(γx_k + 1) + z s.t. p′x + z ≤ E (Eq. 2, p. 7); marginal utility u_k = ψ_k/(γx_k + 1); closed-form demand x_k = (ψ_k − p_k)/(γ p_k) if ψ_k > p_k else 0 (p. 9) — the "bang equals buck" KT logic.
- Statistical specification: ψ_kt = exp[a_kt′β + ε_kt] guarantees positive marginal utility and links part-worths β to attributes (Section 3.1, p. 11); KT conditions become ε_kt = g_kt if x_kt > 0, ε_kt < g_kt if x_kt = 0 with g_kt = −a_kt′β + ln(γx_kt + 1) + ln(p_kt) (Eqs. 3–4, p. 11).
- Closed-form likelihood under iid EV(0,σ): product of R "logit-like" density terms for purchased goods times CDF terms for zeros, times Jacobian |J_R| = Π γ/(γx_it + 1) (p. 12); general form Pr(x_t) = |J_R| {Π f(g_it)} {Π F(g_jt)} (p. 13). Notes the standard discrete choice model is the special case with Jacobian 1 and price coefficient = 1/σ (p. 12).
- Non-linear outside good (u_z = ln z ⇒ marginal utility 1/z): budget E no longer cancels; g_kt = −a_kt′β + ln(γx_kt +1) + ln(p_kt/(E − p_t′x_t)) with full non-diagonal Jacobian; E is statistically identified from the equality KT conditions (Section 3.2, pp. 13–14). Predicted demand has no closed form; can be computed by constrained optimization, e.g., R's `constrOptim` (p. 14).
- Multiple constraints (money E and quantity/space Q): two Lagrange multipliers; g_kt = −a_kt′β + ln(γx_kt+1) + ln(p_kt/(E − p′x) + q_k/(Q − q′x)); goods that exhaust either budget are less likely to be chosen; multipliers are shadow values of relaxing each constraint (Section 4.1, pp. 16–17).
- Non-linear budget sets (quantity discounts / multi-part pricing): kinked budget constraints create mass points in demand at kink points τ_k; solution partitions demand space into regions (P1–P4), applies FOCs within linear segments, likelihood combines density, mass, and interval terms (Section 4.2, pp. 17–20).
- Error specification: iid additive errors imply no dominated alternatives and demand insufficiently price-sensitive; correlated errors with Σ built from perceptual distance σ_kj = exp[−d_kj/θ], d_kj = |ψ_k − ψ_j| relax IIA (Section 5.1, pp. 21–23); indivisible (integer) demand handled by data augmentation over utility-consistent error regions (Lee and Allenby 2014; Section 5.2, pp. 23–24).
- Critique of indirect utility (translog etc.): closed-form indirect utility depends on interior-solution equality conditions; corner solutions, kinks, and packaging grids break Roy's identity and closed forms; direct utility plus constraints is the right primitive for marketing data (Section 6, pp. 24–27).
- Appendix: full Lagrangian derivation of optimal demand x*_k = (1/γ)(ψ_k/(λp_k) − 1) with λ = 1/(γE + Σ p_k), and the implied indirect utility V (pp. 29–30).

## Models & notation

- Linear model: u(x,z) = Σ ψ_k x_k + ψ_z z; utilities of corners u(x_j=1, z=E−p_j) = ψ_j + ψ_z(E−p_j) + ε_j; outside good u(x=0, z=E) = ψ_z E + ε_z (p. 3). Logit form Eq. (1), p. 4. Likelihood Π_t Π_j Pr(j)^{y_jt} with error scale σ=1 for identification (p. 5).
- Volumetric: Eq. (2) p. 7 (log inside goods, linear outside good); KT conditions p. 10; statistical KT Eqs. (3)–(4) p. 11; likelihood and Jacobian p. 12–13; nonlinear outside good Eq. (5) p. 13.
- Multiple constraints: utility Σ (ψ_k/γ)ln(γx_k+1) + ln z + ln w s.t. p′x + z ≤ E, q′x + w ≤ Q (p. 16).
- Kinked budget sets: FOC regimes ε < g_ℓ (zero), ε = g_ℓ (below kink), g_ℓ < ε < g_h (at kink mass point), ε = g_h (above kink); likelihood with density/mass/interval contributions and Jacobian J_ij (pp. 19–20).
- Correlated errors: Σ with σ_kj = exp[−d_kj/θ], d_kj = |ψ_k − ψ_j| (pp. 22–23).
- Translog indirect utility ln V = α_0 + Σ α_k ln(p_k/E) + ½ ΣΣ β_kj ln(p_k/E) ln(p_j/E) (p. 26) — discussed and rejected for disaggregate work.

## Estimation details

- Likelihoods are given in closed form for iid EV errors (volumetric KT model); Bayesian estimation with prior π(ψ) discussed generically; MLE and Bayes both mentioned (p. 5). References Rossi, Allenby, McCulloch (2005) for hierarchical priors.
- Correlated-error probit-style model estimated as hierarchical Bayes with custom software (Dotson et al. 2015; p. 23).
- Indivisible demand: Bayesian data augmentation (Tanner–Wong) over error regions consistent with utility-maximizing integer demand (Eq. 6, pp. 23–24).
- Demand prediction for nonlinear-outside-good model via constrained optimization (`constrOptim` in R, p. 14).
- No empirical application; this is a theory/synthesis chapter.

## Relevance to book chapters

- **Choice framework:** the book's economic-foundations chapter can follow this chapter's arc: budget allotment E, inside vs. outside goods, corner solutions, why zeros dominate marketing data. The derivation of MNL from direct utility (pp. 2–5) is the ideal bridge from consumer theory to the logit likelihood.
- **Utility specification:** authoritative source on linear vs. nonlinear utility, satiation (γ), linear vs. log outside good (and hence whether E is identified), and why the price coefficient in standard MNL is the marginal utility of money / reciprocal error scale.
- **WTP and post-estimation:** indirect utility appendix and Lagrange-multiplier interpretation (shadow value of constraints, pp. 17, 29–30) underpin welfare computations.
- **HB-MNL:** ψ_k = exp(a′β + ε) parameterization and hierarchical treatment; links to bayesm ecosystem.
- **Conjoint practice:** the KT preference-data condition (if k preferred then ψ_k/p_k > ψ_j/p_j, p. 10) shows how stated-preference tasks map into the same framework; volumetric conjoint foreshadows Allenby, Hardt & Rossi (2019).

## Page pointers

(Manuscript page numbers printed at page bottom; PDF page = manuscript page + 2.)
- pp. 1–2: motivation, zeros as constrained behavior
- pp. 2–5: simple discrete choice from direct utility; Eq. (1); likelihood; identification (σ=1)
- pp. 5–6: applications/extensions of logit (McFadden, Guadagni–Little, BLP, heterogeneity)
- pp. 7–10: general volumetric model Eq. (2); marginal utility; Lagrangian; demand; KT conditions
- pp. 11–13: statistical specification; Eqs. (3)–(5); likelihood; Jacobians; nonlinear outside good
- pp. 14–15: constrOptim demand computation; applications (Hanemann, MDCEV, complements)
- pp. 16–17: multiple constraints; shadow values
- pp. 17–20: nonlinear/kinked budget sets; regions P1–P4; mass-point likelihood
- pp. 21–24: error specification — correlated errors, similarity, indivisible demand
- pp. 24–27: indirect utility models (translog) and why to avoid them here
- pp. 27–28: conclusion
- pp. 29–30: appendix — demand and indirect utility derivation
