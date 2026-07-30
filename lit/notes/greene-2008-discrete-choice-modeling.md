# Greene (2008) — Discrete Choice Modeling

**Full citation:** Greene, William H. (2008), "Discrete Choice Modeling," in T. Mills and K. Patterson (eds.), *The Handbook of Econometrics: Vol. 2, Applied Econometrics*, Part 4.2, Palgrave, London.
**Type:** Handbook survey chapter (practitioner-oriented)
**Length:** 78 pages (PDF); body runs printed pp. 1–70 plus references. Note: PDF page = printed page + 1 (title/TOC page is unnumbered). Page refs below use printed page numbers.

## One-paragraph summary

A comprehensive practitioner's survey of econometric models for discrete *choice* (as opposed to arbitrary discrete dependent variables), built on the random utility maximization (RUM) platform. Greene develops the binary choice model in full detail as the template for estimation and inference — MLE, covariance estimators, hypothesis and specification tests, marginal effects, a Bayesian (Gibbs/data-augmentation) estimator, semiparametric alternatives, endogeneity, and panel-data treatments (fixed effects, incidental parameters, random effects via quadrature and simulation, random parameters, latent class) — then extends to bivariate/multivariate probit, ordered choice, count models, and multinomial unordered choice (MNL, MNP, nested logit, mixed logit / error components). Every model class is illustrated with live data: the GSOEP German health care panel (7,293 families; binary, ordered, count models) and the Hensher–Greene Sydney–Melbourne mode choice data (210 travelers; multinomial models).

## Key contributions relevant to the book

- The single most complete "one-stop" reference mapping nearly every chapter of the book: MLE mechanics, optimization behavior (global concavity of logit/probit), Bayes-MCMC for probit, MNP with GHK, nested logit, mixed logit, latent class, and simulation-based estimation, all in consistent notation with worked applications.
- Careful treatment of identification/normalization in RUM models (location and scale of utility) that first-year students need before writing any likelihood (p. 6).
- Explicit likelihoods and gradients (not just model statements), with the three standard asymptotic covariance estimators (BHHH, Hessian, expected Hessian) and a pointed caveat about "robust" covariance matrices in binary choice (Freedman 2006 discussion, p. 10).
- Side-by-side classical vs. Bayesian estimation of the same probit model, including practical timing (Gibbs ~5 minutes vs. Newton MLE ~5 seconds on the same data, p. 32).
- Clear statement of the incidental parameters problem with Monte Carlo evidence (Table 1, p. 23) — essential background for panel/hierarchical models.
- Empirical demonstration of IIA's cross-elasticity restriction and how MNP, nested logit, HEV, and random-parameters logit relax it (Tables 10–12, pp. 69–70).

## Models & notation

- Choice indicators: d_itj = 1 if individual i makes choice j at time t; P_itj = Prob(d_itj = 1 | X_it, z_it, ...); attributes of alternatives x_itj vs. characteristics of individuals z_it; sum of d and P over j equals 1 (eq. 0.4, p. 3).
- General parametric model P_itj = F(j, X_it, z_it, β, γ, u_it) with log likelihood ln L = Σ_i Σ_t Σ_j d_itj ln F(·) (p. 4); Bayesian posterior p(β,γ|D,X,Z) ∝ L × g(β,γ) (p. 4).
- Binary choice via RUM: U_i1 = x_i1'β + z_i'γ + ε_i1 vs. U_i0; identification discussion — only attribute differences matter, individual characteristics need choice-varying coefficients, mean and scale normalizations (eq. 0.15 and surrounding text, p. 6). Standard latent-index form d* = α + x'β + z'γ + ε, d = 1(d* > 0) (eq. 0.1, p. 7).
- Logit F(c) = Λ(c) = e^c/(1+e^c); probit F(c) = Φ(c) (p. 9). Compact notation q_i = 2d_i − 1, w_i = (x_i, z_i), so g_i = q_i f_i w_i (p. 9).
- Heteroscedastic binary choice (Harvey model): Var[ε_i] = [exp(v_i'τ)]² (p. 14).
- Bivariate probit: Prob(d1=1, d2=1) = Φ2[w1'θ1, w2'θ2, ρ] (p. 34); recursive simultaneous bivariate probit (p. 35); bivariate probit with sample selection (p. 36); M-variate probit / panel probit with ln L = Σ ln Φ_M[c_i, D_i] (p. 37).
- Ordered choice: y_i = j if μ_{j−1} < U_i* ≤ μ_j, thresholds μ estimated, μ_0 = 0 normalization; ordered probit/logit (p. 38); heterogeneous thresholds μ_ij = exp(μ_j + v_i'π) (Greene/Harris–Zhao form, p. 40).
- Counts: Poisson λ_i = exp(x_i'β) (p. 46); NB2 from log-gamma heterogeneity, NB1, NegBin P family with Var = λ(1 + αλ^{P−1}) (pp. 48–49); hurdle and zero-inflation two-part models (pp. 50–51); FE/RE panel count models incl. HHG FENB (pp. 53–55).
- Multinomial unordered choice (Section 0.7, p. 61): U_ij = x_ij'β + z_i'γ_j + ε_ij; MNL choice probabilities Prob(d_ij=1|X_i,z_i) = exp(x_ij'β + z_i'γ_j)/Σ_m exp(x_im'β + z_i'γ_m), γ_J = 0 normalization (pp. 61–62); IIA restriction ∂lnP(j)/∂x_m identical across j≠m (p. 62).
- MNP: ε_i ~ N_J[0, Σ], identification via differencing — last row of Σ normalized, one more diagonal fixed, Cholesky Σ = CC' (pp. 62–63).
- Nested logit: three-level tree (trunk/limb/branch/twig), P(j,b,l,r) = P(j|b,l,r)·P(b|l,r)·P(l|r)·P(r); inclusive values IV_b = log Σ exp(x'β), alternative normalizations (RU1/RU2-style scaling at branch vs. twig level), IV parameters between 0 and 1 for RUM consistency; marginal effects decomposition (pp. 63–65).
- Mixed logit / random parameters: β_ki = β_k + z_i'δ_k + σ_k v_ki (normal or lognormal); full vector β_i = β + Δz_i + Γv_i; error-components form generalizing nested logit with E_i,Private / E_i,Public factors (pp. 65–66).

## Estimation details

- **Binary MLE:** ln L = Σ ln F[(2d_i−1)(x_i'β + z_i'γ)]; gradient g = Σ q_i f_i w_i (p. 9). Both logit and probit log likelihoods are globally concave (second-derivative results, p. 10), so Newton or scoring "will always converge to the unique maximum" — a key optimization fact for the book.
- **Covariance estimators:** V_BHHH (outer product), V_H (Hessian), V_EH (expected Hessian) (p. 10); skepticism about robust-sandwich covariance for MLE in binary choice (p. 10, citing Freedman 2006).
- **Inference:** LR, Wald, LM tests with explicit formulas; LM test for "all slopes zero" has closed form in data moments (pp. 13–14); Vuong statistic for logit vs. probit (p. 15); pseudo-R² caveats and prediction-rule fit measures (Cramer's λ_C) (pp. 15–16).
- **Marginal effects:** δ_i = f(w_i'θ)θ; discrete-change effects for dummies; delta method and Krinsky–Robb simulation for standard errors; average partial effects (pp. 11–12).
- **Bayesian probit (Gibbs + data augmentation, Albert–Chib):** treat latent d_i* as parameters; p(θ|d*,d,W) is normal N[q*, (W'W)^{-1}]; p(d_i*|θ,d_i) is truncated normal; explicit 4-step Gibbs algorithm including inverse-cdf truncated-normal draws d*_ir = w'θ + Φ^{-1}[...] (pp. 16–18). Notes the similarity to EM. Application: 500 replications, burn-in 100; posterior means nearly identical to MLE; MLE preferred on practical grounds (pp. 31–32).
- **Semiparametric:** Klein–Spady single-index estimator with kernel-estimated G; Manski maximum score (pp. 18–19). Trade-off: robustness vs. inability to compute partial effects/probabilities.
- **Endogenous regressor:** GMM moment based on residual [d − Φ(x'β + γz)] and FIML control-function likelihood (eq. 0.5) with Olsen transformation (pp. 20–22).
- **Panel binary choice:** unconditional FE MLE inconsistent (incidental parameters; logit T=2 estimator converges to 2β; Monte Carlo Table 1, p. 23); Chamberlain/Rasch conditional logit conditioning on Σ_t d_it (p. 24); Mundlak device (p. 25); RE probit likelihood requires one-dimensional integral (eq. 0.6, p. 27) evaluated by Butler–Moffitt Gauss–Hermite quadrature (typically H = 20, 32, 64 nodes) **or** maximum simulated likelihood: ln L_S = Σ_i ln (1/R) Σ_r Π_t Φ(q_it(x_it'β + z_i'γ + σ_u u_ir)), with the requirement √n/R → 0; Halton sequences noted as more efficient than pseudo-random draws (p. 27). Practical guidance: several hundred to 1,000 draws (fn. 17, p. 27).
- **Dynamic panel:** state dependence, initial conditions, Wooldridge (2005) treatment (eq. 0.7–0.8, pp. 27–28).
- **Random parameters / mixed models for panels:** θ_i = θ_0 + Δz_i + Γu_i, estimated by quadrature or MSL with simulated log likelihood (p. 29).
- **Multivariate probit / panel probit:** M-dimensional normal cdf evaluated by GHK simulator (Geweke–Hajivassiliou–Keane) (p. 37).
- **Ordered choice estimation:** standard MLE; application finds Butler–Moffitt quadrature converged to a wrong/implausible point while MSL was slower but reliable — a nice cautionary optimization anecdote (p. 44).
- **Count models:** Poisson MLE with closed-form gradient/Hessian (p. 46); NB via gamma mixture integrated in closed form (p. 48); selection and bivariate models needing Hermite quadrature or simulation of the log likelihood (log L_S formula, p. 52); FE Poisson has no incidental parameters problem (conditional = unconditional MLE, p. 53).
- **MNP estimation:** simulated probabilities/derivatives via GHK; Gibbs sampler with noninformative priors (Allenby–Rossi 1999, Rossi–Allenby 2003) as alternative; "even with the GHK simulator... computation of the probabilities by simulation is time consuming" (p. 63).
- **Mixed logit estimation:** unconditional probabilities P_j = E_v,E[P(j|ε_i,E_i)] are open-form integrals approximated by simulation; parameters estimated by maximum simulated likelihood (pp. 66–67).
- **Choice-based sampling:** Manski–Lerman WESML weighted log likelihood ln L(WESML) = ΣΣ (π_j/p_j) d_ij ln Π_ij with sandwich covariance H^{-1}(G'G)H^{-1} (p. 67) — the Sydney–Melbourne sample is choice based.
- **Empirical multinomial comparison:** MNL, MNP, three nested logit trees, HEV (heteroscedastic extreme value with variance function σ_j²·exp(θ·PartySize)), and random-parameters logit on the same data (Table 10, p. 69); predicted-vs-actual cross-tabs (Table 11); GC elasticities exposing IIA — MNL cross-elasticities identical across alternatives (0.0435 etc.), none of the other models share this (Table 12, p. 70).

## Relevance to book chapters

- **Choice framework (ch. 1):** Sections 0.1–0.2 and the opening of 0.3 — RUM platform, choice indicators, identification/normalization (pp. 1–7, 61).
- **MLE (ch. 4):** Section 0.3.2 is a model treatment — likelihood, gradient, covariance estimators, LR/Wald/LM, fit (pp. 9–16).
- **Optimization (ch. 5):** global concavity of logit/probit log likelihoods (p. 10); quadrature-vs-MSL convergence failure anecdote (p. 44); Gibbs vs. Newton timing (p. 32).
- **Estimation practice / programming (chs. 6–7):** worked applications with real data, prediction tables, marginal effects and delta-method/Krinsky–Robb standard errors (pp. 11–12, 31–33, 67–70).
- **Bayes-MCMC (ch. 8):** Albert–Chib Gibbs sampler for binary probit spelled out step by step (pp. 16–18, 31–32); Gibbs for MNP referenced (p. 63).
- **MNP (ch. 9):** identification of Σ, Cholesky parameterization, GHK (pp. 62–63); multivariate/panel probit (pp. 36–37).
- **Nested logit / GEV (chs. 10–11):** Section 0.7.2 — trees, inclusive values, normalizations, RUM restrictions on IV parameters, marginal-effect decomposition (pp. 63–65); HEV as another GEV-adjacent relaxation (p. 68).
- **Simulation-assisted estimation (ch. 12):** MSL for RE probit (p. 27), GHK (pp. 37, 63), simulated log likelihoods for selection/count models (p. 52), Halton sequences (p. 27).
- **Latent class (ch. 13):** introduced as the discrete-heterogeneity counterpart of random parameters (p. 29); zero-inflation models described as "a type of latent class model" (p. 50).
- **Mixed logit (ch. 14):** Section 0.7.3 — random parameters, lognormal variant, error-components generalization of nested logit, MSL estimation (pp. 65–67); RPL results in Table 10.
- **Drawing densities / simulating data (chs. 2–3):** inverse-cdf truncated normal draws in the Gibbs algorithm (p. 18); uniform-to-target-transformation logic throughout the simulation discussions.

## Page pointers

(printed page numbers; add 1 for PDF page)
- p. 1: scope — models of discrete *choice*, RUM platform; roadmap of sections
- p. 3: notation d_itj, P_itj; attributes vs. characteristics
- p. 4: general log likelihood; Bayesian posterior; partial effects defined
- p. 5: two application datasets (GSOEP health care; Sydney–Melbourne mode choice)
- p. 6: binary RUM; identification — differences, normalizations of mean and scale
- p. 9: logit and probit cdfs; log likelihood and gradient
- p. 10: BHHH / Hessian / expected Hessian covariance estimators; global concavity; robust-covariance caveat
- p. 11: generalized residuals; logit fitted-share property; marginal effects
- p. 12: delta method and Krinsky–Robb standard errors for partial effects
- p. 13–14: LR, Wald, LM tests; heteroscedasticity (Harvey model)
- p. 15: Vuong test logit vs. probit; pseudo-R² critique
- p. 16–18: Bayesian probit — Albert–Chib data augmentation, 4-step Gibbs sampler
- p. 18–19: semiparametric estimators (Klein–Spady; Manski maximum score)
- p. 20–22: endogenous RHS variable — GMM and FIML control function (eq. 0.5)
- p. 23: incidental parameters problem; Monte Carlo Table 1
- p. 24: Chamberlain/Rasch conditional fixed-effects logit
- p. 25: Mundlak device; random effects probit setup
- p. 27: RE probit likelihood (eq. 0.6); Butler–Moffitt quadrature; MSL; Halton draws
- p. 27–28: dynamic panel models, initial conditions (eqs. 0.7–0.8)
- p. 29: random parameters and latent class models for panel data
- p. 31–32: GSOEP application; LR/Wald/LM computed; Gibbs vs. MLE practicality
- p. 33: Table 3 — panel binary estimates (pooled, RE, FE, Bayesian, MSL)
- p. 34–37: bivariate, recursive, selection, multivariate probit; GHK; panel probit
- p. 38–40: ordered probit/logit; thresholds; heterogeneous thresholds
- p. 43–44: ordered choice panel; MSL vs. quadrature failure
- p. 46–55: count models — Poisson, NB1/NB2/NBP, hurdle, ZIP, selection, panel counts
- p. 61–62: MNL — choice probabilities, log likelihood, IIA restriction
- p. 62–63: MNP — identification, Cholesky, GHK, Gibbs (Allenby–Rossi)
- p. 63–65: nested logit — tree structure, inclusive values, normalizations, marginal effects
- p. 65–66: mixed logit and error-components models
- p. 67: WESML choice-based sampling correction; utility specifications for application
- p. 68–70: Tables 9–12 — estimates across MNL/MNP/NL/HEV/RPL; predictions; elasticities showing IIA
- p. 70: summary and conclusions
