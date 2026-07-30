# Allenby, Hardt & Rossi (2019) — Economic Foundations of Conjoint Analysis

**Full citation:** Allenby, G.M., Hardt, N., & Rossi, P.E. (2019). Economic foundations of conjoint analysis. Chapter 3 in *Handbook of the Economics of Marketing*, Vol. 1, pp. 151–192. Elsevier. DOI 10.1016/bs.hem.2019.04.002
**Type:** Handbook chapter (economic theory of conjoint + study design + validation study)
**Length:** 42 pages (journal pp. 151–192; ~40 substantive pages plus references)

## One-paragraph summary

This chapter is the modern statement of conjoint analysis as applied economics: conjoint is a demand *experiment*, and its data should be analyzed with valid economic models derived from direct utility maximization under a budget constraint. Two workhorse models are developed side by side: (i) the discrete-choice model from linear utility u(x,z) = Σψ_k x_k + ψ_z z with budget Σp_k x_k + z = E, giving the standard logit where ψ_z is the price coefficient / marginal utility of money and E drops out; and (ii) the volumetric demand model from u(x,z) = Σ(ψ_k/γ)ln(γx_k+1) + ln(z), whose Kuhn–Tucker conditions give a closed-form likelihood in which the error scale σ is identified and the budget E enters. Marginal utilities are parameterized as ψ_j = a_j′β (discrete) or ψ_j = exp(a_j′β + ε_j) (volumetric), with normal (or mixture/regression) heterogeneity estimated by Bayesian MCMC. The chapter then defines three coherent measures of economic value — WTP (compensating variation via the indirect utility / log-sum), WTB (change in expected demand or share), and EPP (economic price premium from Nash equilibrium pricing) — and stresses that all market-level inference must integrate over the posterior of the hyper-parameters, never over individual-level point estimates. Long practical sections cover survey design (screening, representativeness of internet panels, glossaries, dual-response no-choice, timing data, sample size) and enumerate practices that destroy statistical validity (unproven estimators, ad hoc tying/zeroing of constrained part-worths) or economic validity (dummy-coded price, self-explicated conjoint, comparing raw part-worths across respondents, mixing MaxDiff with conjoint). A closing validation study on frozen pizza shows conjoint and transaction-based panel estimates of part-worths agree closely (r ≈ 0.9–0.93), demand changes and WTP agree once brand intercepts are aligned, and pseudo-WTP grossly overstates value (e.g., $0.78–$3.31 pseudo-WTP vs. ~$0.03 true WTP for a "for two" attribute).

## Key contributions relevant to the book

- Positions conjoint as an experimentally designed demand system with no price endogeneity — all variation is usable — vs. observational data requiring instruments (pp. 152–153); also stresses conjoint alone cannot deliver equilibrium outcomes without supply-side assumptions ("market simulators" ≠ market equilibria, p. 153).
- Twin utility specifications (discrete + volumetric) with complete likelihood derivations, including the volumetric KT likelihood with Jacobian (Eqs. 1–13, pp. 154–158). Notes error scale σ is identified in the volumetric model because price enters without a separate price coefficient (p. 157).
- Expected demand framework D(θ_h, ε_ht | A_t, p_t) (Eq. 14) and its integration over errors, individual parameters, and hyper-parameters (Eqs. 15, 19, 21) — the template for all post-estimation computation (pp. 158–161).
- Heterogeneity: θ_h ~ N(θ̄, Σ), mixtures Σφ_k N(θ̄_k, Σ_k), and covariate-driven means N(Γz_h, Σ) (Eqs. 16–18, p. 159); insistence that only hyper-parameters are consistently estimated (fixed T, growing N) and inference must be based on them (p. 160, 176–177).
- Three value measures: WTP via V(p, E+WTP|A) = V(p, E|A*) with log-sum expression for logit (Eqs. 22–25, pp. 162–163) and numerical solution for volumetric (Eq. 26); WTB as change in expected share/sales (Eqs. 27–29, p. 164); EPP via Nash equilibrium pricing (Eqs. 30–33, pp. 164–165). Explicit critique of Ofek–Srinivasan MVAI (p. 163).
- Practices that compromise validity (Section 5, pp. 175–179): estimators without consistency proofs; imposing sign/order constraints by post-hoc tying or zeroing draws (incoherent, violates Bayes theorem) — instead reparameterize, e.g., ψ_z = −exp(β_p), or use constrained priors (bayesm supports both, p. 177); dummy-coded price violates monotone indirect utility (p. 177–178); self-explicated conjoint and MaxDiff "importances" are not utilities (pp. 178–179); raw part-worths are not comparable across respondents — monetize via WTP/WTB/EPP first (pp. 178–179).
- Survey design guidance: screen for category prospects; internet panels are convenience samples — establish representativeness with behavioral correlates, not just click-balancing demographics (pp. 166–170); glossaries must describe attributes factually, not sell benefits (p. 170); dual-response no-choice improves realism (p. 172, Fig. 3); collect timing data (p. 173); sample sizes for equilibrium computations exceed the usual 500–1000 rule of thumb (p. 175).
- Validation study (Section 6, pp. 179–188): frozen pizza volumetric conjoint (181 households, 12 tasks, 6 alternatives + no-choice) vs. 2-year transaction panel of the same panelists; part-worth means agree (r = 0.93 volumetric, Fig. 6; r = 0.9 discrete, Fig. 7); discrepancies concentrated in β_0 (no-choice/brand intercept), γ (satiation), E (budget), σ — conjoint shows lesser satiation and larger budgets (pp. 183–184, Table 2); demand curves parallel; WTP for a "for-two" attribute ≈ $0.03 (logit) from either data source, vs. pseudo-WTP $0.78 (conjoint) or $3.31 (transactions) (Table 4, p. 187).
- Technical appendix: efficient exact algorithm for computing volumetric expected demand (ordering breakpoints ρ_i = p_i/ψ_i, iterating to find optimal outside good z, then x) — the basis for the authors' `echoice` R package (pp. 189–190; software mentioned p. 178 fn. 5, p. 152).

## Models & notation

- Discrete choice: u(x,z) = Σ_k ψ_k x_k + ψ_z z (Eq. 1, p. 154), budget Σ p_k x_k + z = E (Eq. 2, p. 155); chosen-good utility ψ_j + ψ_z(E−p_j) + ε_j (Eq. 3); no-choice ψ_z E + ε_z (Eq. 4); logit Pr(j) = exp[ψ_j − ψ_z p_j]/(1 + Σ_k exp[ψ_k − ψ_z p_k]) (Eq. 5, p. 155). E drops out but screens alternatives with p_k > E (p. 156, citing Pachali et al. 2017). Attribute link ψ_j = a_j′β (Eq. 6, p. 156).
- Volumetric: u(x,z) = Σ(ψ_k/γ) ln(γx_k+1) + ln(z) (Eq. 7, p. 156); marginal utilities Eq. 8; KT conditions Eq. 9–11 with g_j = −a_j′β + ln(γx_j+1) + ln(p_j/(E−p′x)) (Eq. 12, p. 157); likelihood ℓ(θ) ∝ |J_R| Π_{chosen} f(g_j) Π_{not} F(g_i), EV(0,σ) errors, Jacobian given explicitly (Eq. 13, pp. 157–158). Discrete model is the R=1, σ=1, Jacobian=1 special case with g_j = −a_j′β − ψ_z p_j (p. 158).
- Heterogeneity: Eqs. 16–18 (p. 159); market-level quantities Eq. 19 (p. 160); indirect utility Eqs. 20–21 (pp. 160–161).
- Value measures: WTP discrete closed form Eqs. 24–25 (welfare W = E + ln[Σ exp(β′a_j − β_p p_j)]/β_p, pp. 162–163); WTP volumetric Eq. 26 (numerical); WTB Eqs. 27–29 (p. 164); EPP/Nash Eqs. 30–33 (pp. 164–165).

## Estimation details

- Bayesian MCMC per Rossi, Allenby & McCulloch (2005); normal random-coefficients as default with diffuse priors; mixtures and covariate-shifted means as extensions (p. 159).
- Sign constraints via reparameterization ψ_z = −exp(β_p) inside the likelihood, or via constrained priors (Allenby et al. 1995); automated in **bayesm**; tying/zeroing draws condemned (p. 177).
- Volumetric expected demand has no closed form: simulate ε draws, solve constrained optimization per draw (constrOptim or the appendix algorithm), average (pp. 158–159, 189–190). R package **echoice** for economically valid volumetric conjoint (p. 178, fn. 5).
- Pizza study estimation: dummy coding with reference levels; β_0 inside-good intercept vs. outside good; ln γ, ln E, ln σ log-transformed for positivity; MVN heterogeneity, diffuse priors; EV Type 1 errors (Table 2 notes, p. 182). Discrete-choice version estimated on "exploded" volumetric data with re-parameterized negative price coefficient (p. 184, Table 3).
- Consistency discussion: Bayes procedures consistent and admissible; large-N fixed-T asymptotics; individual-level estimates neither consistent nor appropriate for inference; using them understates posterior uncertainty (pp. 176–177).

## Relevance to book chapters

- **Choice framework:** Section 2 is arguably the best compact source for the book's "from utility theory to logit" development, including the outside good and budget allotment interpretation.
- **Utility specification:** linear vs. volumetric (satiating) utility; when E is identified; dummy vs. effects coding of attributes (p. 156); why price must enter as a continuous monotone term, not dummies (pp. 177–178).
- **WTP and post-estimation:** definitive taxonomy WTP / WTB / EPP with formulas; pseudo-WTP warning backed by empirical magnitudes (Table 4); all market-level quantities as posterior functionals of hyper-parameters (Eqs. 19, 21).
- **HB-MNL:** Eqs. 16–18 heterogeneity menu; hyper- vs. individual-parameter inference; constraint handling in bayesm; sample size discussion for demanding posterior functionals.
- **Conjoint practice:** Sections 4–5 provide the book's practice guidance: screening, representativeness, glossary construction, dual response, timing data, and the list of invalid practices (self-explicated, MaxDiff mixing, raw part-worth comparisons).
- **Validation/credibility:** Section 6's conjoint-vs-transaction comparison is the key empirical evidence that well-designed conjoint recovers marketplace preferences.

## Page pointers

(Journal page numbers = PDF page + 150.)
- pp. 152–154: introduction; conjoint as experiment; endogeneity discussion; "market simulator" caveat
- pp. 154–156: discrete choice model, Eqs. 1–6
- pp. 156–158: volumetric model, KT conditions, likelihood, Eqs. 7–13
- pp. 158–161: expected demand, heterogeneity, market-level predictions, indirect utility, Eqs. 14–21
- pp. 161–165: measures of value — WTP (Eqs. 22–26), WTB (Eqs. 27–29), EPP (Eqs. 30–33)
- pp. 165–175: study design — screening, representativeness, glossary, choice tasks (Figs. 1–4), dual response, timing, sample size
- pp. 175–179: threats to statistical validity (consistency, constraints) and economic validity (dummy price, self-explicated, raw part-worth comparison, MaxDiff); bayesm and echoice mentions
- pp. 179–188: frozen pizza validation study; Tables 1–4; Figs. 5–9; WTP vs. pseudo-WTP
- pp. 189–190: technical appendix — algorithm for volumetric expected demand
