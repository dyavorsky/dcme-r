# Train (2009) — Discrete Choice Methods with Simulation, 2nd ed.

**Full citation:** Train, Kenneth E. (2009). *Discrete Choice Methods with Simulation*, 2nd edition. Cambridge University Press. ISBN 978-0-521-74738-7 (pbk). Free text and companion code/data at the author's Berkeley site.
**Type:** Book (companion text for this project, cited as @train2009 / "DCMS")
**Length:** 399 PDF pages; book pages 1–370 plus bibliography/index. **PDF page offset: book page X = PDF page X + 11** (e.g., book p. 1 = PDF p. 12; book p. 184 = PDF p. 195). Front matter (TOC, preface blurb) = PDF pp. 1–11.

## Overview
DCMS is the canonical graduate-level treatment of discrete choice models estimated with simulation. Part I ("Behavioral Models," Chs. 2–7) develops the models: the general random-utility framework, logit, GEV/nested logit, probit, mixed logit, and a chapter of custom variations. Part II ("Estimation," Chs. 8–14) develops the computational machinery: numerical maximization of likelihoods, taking draws from densities, properties of simulation-based estimators (MSL/MSM/MSS), individual-level parameters, Bayesian/MCMC procedures, endogeneity (new in 2nd ed.), and EM algorithms (new in 2nd ed.). Train's explicit pedagogical stance — stated in Ch. 1 and Ch. 8 — is that researchers should be able to *program their own estimators* rather than rely on packaged models, and that coding a model is how you come to understand it. This matches the DCME-R book's approach (simulate data from a model, build the likelihood, estimate, recover parameters) almost exactly, which is why DCMS is the primary companion text.

## Chapter-by-chapter index

### Ch 1: Introduction (book pp. 1–8 / PDF pp. 12–19)
Motivates the "simulation revolution": simulation is the researcher's response to the inability of computers to perform integration. Sets up the master equation P(y|x) = ∫ I[h(x,ε)=y] f(ε) dε and identifies three cases: complete closed form (logit, nested logit), complete simulation (probit), and partial simulation / "convenient error partitioning" (mixed logit). Gives the first pseudo-code of the book (p. 5): the 4-step frequency simulator (draw ε, compute indicator, repeat R times, average). Section 1.3 outlines the two-part structure (behavioral models vs. estimation).
**Relevant to book chapters on:** choice framework / simulating data / simulation-assisted estimation

### Ch 2: Properties of Discrete Choice Models (book pp. 11–33 / PDF pp. 22–44)
The conceptual foundation for everything else. Covers: the choice set (mutually exclusive, exhaustive, finite; pp. 11–14); derivation of choice probabilities from random utility maximization, U_nj = V_nj + ε_nj, P_ni = Prob(ε_nj − ε_ni < V_ni − V_nj ∀ j≠i) as a multidimensional integral (eqs. 2.1–2.2, pp. 14–17); a preview of how logit, GEV, probit, mixed logit differ only in the assumed density f(ε_n) (pp. 17–19); identification (pp. 19–29) organized around two maxims — "only differences in utility matter" (alternative-specific constants, normalizing one to zero; sociodemographics must interact with alternatives) and "the scale of utility is arbitrary" (error-variance normalization; why coefficients are relative to error scale); aggregation via sample enumeration (p. 29); forecasting (p. 32); recalibration of constants (p. 33).
**Relevant to book chapters on:** choice framework / MLE (identification & normalization) / organizing choice data

### Ch 3: Logit (book pp. 34–75 / PDF pp. 45–86)
The workhorse chapter. Derives the logit probability P_ni = e^{V_ni}/Σ_j e^{V_nj} from iid extreme value (Gumbel) errors, density f(ε) = e^{−ε}e^{−e^{−ε}} (eqs. 3.1–3.6, pp. 34–37; full algebraic derivation deferred to §3.10, pp. 74–75). Key content: the scale parameter and normalization Var(ε) = π²/6 (p. 40); power and limitations — taste variation, IIA and proportional substitution, no correlated panel errors (pp. 42–52); consumer surplus via the log-sum formula (p. 55); derivatives and elasticities, including the IIA-driven uniform cross-elasticity E_iznj = −β_z z_nj P_nj (pp. 57–60); **estimation by MLE (§3.7, pp. 60–67)**: the log-likelihood LL(β) = Σ_n Σ_i y_ni ln P_ni (eq. 3.11), global concavity (McFadden 1974), the first-order condition Σ_n Σ_i (y_ni − P_ni) x_ni = 0 (eq. 3.13) with its interpretation (predicted shares = observed shares when ASCs are included; residuals uncorrelated with regressors — a method-of-moments view), estimation on a subset of alternatives with McFadden's uniform conditioning property (pp. 64–66), and choice-based (WESML) sampling; goodness of fit (likelihood ratio index ρ²) and hypothesis testing (pp. 67–71); BART forecasting case study (pp. 71–74). Willingness-to-pay as coefficient ratio −β₂/β₁ worked example on p. 39.
**Relevant to book chapters on:** choice framework / MLE / building likelihoods / organizing choice data

### Ch 4: GEV (book pp. 76–96 / PDF pp. 87–107)
Generalized extreme value models: closed-form probabilities with correlated errors. Nested logit (§4.2, pp. 77–86): alternatives partitioned into nests B_k; GEV cumulative distribution exp(−Σ_k (Σ_{j∈B_k} e^{−ε_nj/λ_k})^{λ_k}) (eq. 4.1); choice probability eq. 4.2 (p. 80) with λ_k as the independence ("log-sum" / inclusive-value) coefficient — 1−λ_k indexes within-nest correlation, λ_k = 1 collapses to logit; IIA holds within but not across nests (worked substitution example, Table 4.1, p. 78); decomposition into marginal (nest-choice) × conditional (within-nest) logits with the inclusive value linking them, and the warning against sequential estimation vs. FIML (pp. 80–86). Also: three-level nested logit (p. 86); overlapping nests — paired combinatorial logit (PCL) and generalized nested logit (GNL) (pp. 89–92); heteroskedastic logit (p. 92); the general GEV family and McFadden's generating function G with its four properties for constructing new models (pp. 93–96).
**Relevant to book chapters on:** nested-GEV / building likelihoods / MLE

### Ch 5: Probit (book pp. 97–133 / PDF pp. 108–144)
Probit handles all three logit limitations (taste variation, flexible substitution, correlated panel errors) at the cost of requiring normality. Choice probabilities as J-dimensional integrals over ε_n ~ N(0, Ω), or (J−1)-dimensional integrals over error differences using the differencing matrix M_i, with Ω̃_i = M_i Ω M_i′ worked out explicitly (pp. 97–100). Identification of the covariance matrix — which elements of Ω are estimable after level/scale normalization (pp. 100–106). Random taste variation (p. 106), substitution/failure of IIA (p. 108), panel data (p. 110). **§5.6 Simulation of the probabilities (pp. 114–133)** is the heart: quadrature and the Clark approximation dismissed (pp. 114–115); **accept–reject (AR) simulator** with explicit 5-step algorithm (pp. 115–117) and its flaws (not smooth, can be zero); **logit-smoothed AR simulator** (McFadden 1989) (§5.6.2, ~pp. 120–124); **GHK simulator** (§5.6.3, pp. 126–133) explained three ways — as truncated-normal recursion with full step-by-step pseudo-code using Choleski elements and Φ (pp. 128–129), in general terms, and as importance sampling (pp. 131–133); practical notes on using GHK inside MLE (p. 129).
**Relevant to book chapters on:** MNP / drawing densities / simulation-assisted estimation / building likelihoods

### Ch 6: Mixed Logit (book pp. 134–150 / PDF pp. 145–161)
Defines mixed logit by its probability form P_ni = ∫ L_ni(β) f(β) dβ, a mixture of logits over mixing distribution f(β) (eq. 6.1, p. 135). Discrete f(β) gives the **latent class model** (p. 135–136); continuous f(β) (normal, lognormal, uniform, triangular, Rayleigh, truncated normal) gives random-coefficients logit. Carefully distinguishes β (random coefficients, integrated out) from θ (parameters of f, estimated) (p. 136). Derivations: random coefficients U_nj = β_n′x_nj + ε_nj (p. 137); error components U_nj = α′x_nj + μ_n′z_nj + ε_nj creating correlation/substitution patterns (p. 139); the McFadden–Train theorem that mixed logit approximates any RUM (§6.5, pp. 141–144). **§6.6 Simulation (p. 144)**: 3-step simulated probability P̌_ni = (1/R)Σ_r L_ni(β^r) — unbiased, strictly positive, smooth — inserted into the simulated log-likelihood SLL = Σ_n Σ_j d_nj ln P̌_nj for MSL estimation. Panel data via product-of-logits inside the integral (eqs. 6.2–6.3, pp. 145–147); anglers' fishing-site case study (p. 147).
**Relevant to book chapters on:** mixed logit / latent class / simulating data / MLE / simulation-assisted estimation / building likelihoods

### Ch 7: Variations on a Theme (book pp. 151–183 / PDF pp. 162–194)
A tour of custom models built from the primary ones, organized by data type; the theme is that slight specification changes make packaged software unusable, so the researcher should adapt her own code. Covers: combining stated-preference and revealed-preference data with scale differences (p. 152); ranked data via exploded logit and mixed/probit versions (p. 156); ordered responses (ordered logit/probit with cutpoints; multiresponse via GHK) (p. 159); contingent valuation (p. 164); mixed models like mixed probit estimated with GHK-inside-mixing draws (p. 166); dynamic optimization / forward-looking behavior (p. 169).
**Relevant to book chapters on:** organizing choice data / building likelihoods / simulation-assisted estimation

### Ch 8: Numerical Maximization (book pp. 185–204 / PDF pp. 196–215)
The optimization chapter. Notation: average log-likelihood LL(β) = Σ_n ln P_n(β)/N; gradient g_t; Hessian H_t; score s_n(θ) = ∂ln P_n/∂θ (pp. 185–186). Algorithms (§8.3, pp. 187–198), each with intuition and update formula β_{t+1} = β_t + λ(−H_t)^{−1}g_t or a Hessian substitute: **Newton–Raphson** (pp. 187–191, incl. one-step convergence on quadratics, step-size halving/doubling rule for λ, concavity guarantees); **BHHH** using the outer product of scores B_t (pp. ~192–194, with the information identity motivation); **BHHH-2** (p. ~195); **steepest ascent** (p. ~196); **DFP/BFGS** quasi-Newton updates (pp. ~197–198, noted as the usual default). Convergence criterion based on the statistic m_t = g_t′(−H_t)^{−1}g_t (p. 198); local vs. global maxima (p. 199); variance of estimates from −H^{-1} or robust sandwich (p. 200); the information identity (p. 202). Directly transferable to R's `optim`/`maxLik` workflow.
**Relevant to book chapters on:** optimization / MLE

### Ch 9: Drawing from Densities (book pp. 205–236 / PDF pp. 216–247)
The chapter the DCME-R "drawing from densities" material maps onto. **§9.2 Random draws (pp. 205–214)** in progressive sequence: standard uniform/normal from library RNGs (notation: η = std normal draw, μ = std uniform draw); transformations (normal b + sη; lognormal e^{b+sη} with moment formulas) (p. 206); **inverse-CDF method** ε = F^{−1}(μ) for univariate densities, with the extreme value example ε = −ln(−ln μ) (pp. 206–207, Fig. 9.1); truncated univariate densities via μ̄ = (1−μ)F(a) + μF(b) (p. 207); **Choleski transformation** ε = b + Lη for multivariate normals, LL′ = Ω, with 3-dimensional worked example (pp. 208–209); accept–reject for truncated multivariate densities (p. 209); importance sampling (p. 210); Gibbs sampling for joint densities via conditionals (p. ~212); **Metropolis–Hastings algorithm** with explicit 6-step pseudo-code and the key point that the normalizing constant cancels (pp. 212–214). **§9.3 Variance reduction (pp. 214–236)**: coverage and (negative) covariance as the two design criteria; antithetic draws (§9.3.1, p. ~217); systematic sampling (§9.3.2, p. ~219); **Halton sequences** (§9.3.3, pp. ~221–230) including evidence that 100 Halton draws beat 1000 pseudo-random draws for mixed logit; randomized Halton (§9.3.4, p. ~233) and scrambled Halton for high dimensions (§9.3.5, p. ~236).
**Relevant to book chapters on:** drawing densities / simulating data / Bayes-MCMC / mixed logit

### Ch 10: Simulation-Assisted Estimation (book pp. 237–258 / PDF pp. 248–269)
Theory of estimators when simulated probabilities replace exact ones. Defines and compares three estimators (pp. 237–245): **MSL** (maximize SLL(θ) = Σ_n ln P̌_n(θ)); **MSM** (McFadden 1989; simulated residuals d_nj − P̌_nj orthogonal to instruments z_nj, eq. 10.1); **MSS** (simulated scores, Hajivassiliou–McFadden). Headline results (p. 239): MSL is biased for fixed R because ln P̌ is a nonlinear transform of an unbiased simulator — inconsistent with fixed R, consistent if R rises with N, and asymptotically equivalent to ML if R rises faster than √N; MSM with unbiased simulated probabilities is consistent for fixed R; MSS can attain both consistency and efficiency under weaker conditions but is harder to implement. Develops the chunky asymptotics via the central limit theorem (p. 245), traditional estimator properties (p. 247), and the simulation-noise decomposition (bias, variance) of simulation-based estimators (pp. 250–257).
**Relevant to book chapters on:** simulation-assisted estimation / MLE / mixed logit / MNP

### Ch 11: Individual-Level Parameters (book pp. 259–281 / PDF pp. 270–292)
The classical (non-Bayesian) route to individual-level coefficients in random-coefficient models. Central distinction: population distribution g(β|θ) vs. the conditional distribution of tastes among people who made choices y facing attributes x, h(β|y,x,θ) ∝ P(y|x,β)g(β|θ) (derived pp. 262–264). Conditional means simulated as weighted averages of draws with logit-likelihood weights. Monte Carlo illustration (p. 267), the average conditional distribution (p. 269), and an energy-supplier case study (pp. 270–280). Mirrors (classically) what HB delivers via draws of β_n in Ch. 12; also the conceptual basis for individual partworth estimation in conjoint/maxdiff practice.
**Relevant to book chapters on:** mixed logit / Bayes-MCMC (classical analog) / simulation-assisted estimation

### Ch 12: Bayesian Procedures (book pp. 282–314 / PDF pp. 293–325)
The MCMC/hierarchical Bayes chapter. Motivations (pp. 282–284): no maximization needed; consistent for fixed simulation draws; and — key framing — Bayesian procedures are an *estimation method*, not a behavioral model, and the posterior mean can be interpreted classically (Bernstein–von Mises: asymptotically equivalent to MLE). Bayesian concepts: prior k(θ), likelihood L(Y|θ) = Π_n P(y_n|θ), posterior K(θ|Y) ∝ L(Y|θ)k(θ) (pp. 284–291); simulation of the posterior mean (p. 291); drawing from the posterior (p. 293); conjugate results for the normal distribution — posterior of mean given variance (result A) and inverted Wishart posterior of variance given mean (result B) (§12.5, pp. 294–299). **§12.6 Hierarchical Bayes for mixed logit (pp. 299–305)**: the model U_njt = β_n′x_njt + ε_njt, β_n ~ N(b, W) with diffuse normal prior on b and IW(K, I) prior on W; full three-layer **Gibbs sampler with pseudo-code** — (1) draw b | W, β_n from N(β̄, W/N); (2) draw W | b, β_n from IW(K+N, (KI + NS̄)/(K+N)); (3) draw each β_n by one Metropolis–Hastings step with normal proposal ρLη, acceptance ratio F = [L(y_n|β̃)φ(β̃|b,W)]/[L(y_n|β⁰)φ(β⁰|b,W)] — including burn-in, thinning (keep every 10th draw), and adaptive tuning of ρ to target ~0.23–0.44 acceptance (pp. 301–303). Succinct restatement of the model/priors/conditional posteriors in publication form (§12.6.1, p. 304). Case study comparing Bayesian and classical estimates on energy-supplier data (p. 305); Bayesian probit via Albert–Chib/McCulloch–Rossi data augmentation (p. 313).
**Relevant to book chapters on:** Bayes-MCMC / mixed logit / drawing densities / MNP

### Ch 13: Endogeneity (book pp. 315–346 / PDF pp. 326–357)
New to the 2nd edition. When explanatory variables (especially price) are correlated with unobserved factors — unobserved attributes reflected in price, marketing co-movement with price, interrelated choices (mode + residential location) — standard estimation is inconsistent, with sign-predictable bias (pp. 315–317). Methods: the **BLP approach** with alternative-specific constants absorbed and the contraction mapping/instrumental variables at the market level (p. 318); supply side (p. 328); **control functions** (p. 334); full-information maximum likelihood (p. 340); new-vehicle choice case study (p. 342). Peripheral to the DCME-R estimation core, but the natural pointer for demand-modeling extensions.
**Relevant to book chapters on:** choice framework (exogeneity assumption) / MLE (advanced)

### Ch 14: EM Algorithms (book pp. 347–370 / PDF pp. 358–381)
New to the 2nd edition. EM as maximization when gradient methods struggle (many parameters, non-quadratic LL): treat unobserved quantities (e.g., each person's β_n or class membership) as missing data z with density f(z|θ); iterate E-step (expected complete-data log-likelihood, with weights h(z|y,θ^t) ∝ P(y|z,θ)f(z|θ)) and M-step (pp. 347–355). Worked examples (§14.3, pp. 355–365) include discrete mixing distributions (latent class logit — each M-step reduces to weighted logit estimation) and **nonparametric estimation of random-coefficient distributions**; case study on demand for hydrogen cars (p. 365). Useful for the latent-class chapter as the classical estimation counterpart to gradient-based MLE.
**Relevant to book chapters on:** latent class / mixed logit / optimization / MLE

## Notation conventions
(The Quarto book follows these.)
- **Decision maker:** n = 1,…,N; **alternatives:** i, j = 1,…,J; **time/choice situation:** t = 1,…,T. Researcher is "she," decision maker is "he."
- **Utility:** U_nj = V_nj + ε_nj; V_nj = representative (observed) utility, usually linear-in-parameters V_nj = β′x_nj; ε_nj = unobserved portion, density f(ε_n).
- **Data:** x_nj = observed attributes of alternative j faced by n; s_n = characteristics of the decision maker; y_n (or y_ni / d_nj = 0/1 chosen-alternative indicators) = observed choice(s).
- **Probabilities:** P_ni = choice probability; L_ni(β) = logit formula evaluated at β (used inside mixed logit); P̌ = a *simulated* probability (check accent); simulated draws indexed r = 1,…,R with superscripts (ε^r, β^r).
- **Mixed logit / HB:** β_n = individual coefficients with mixing density f(β|θ); θ = parameters of the mixing distribution; in HB notation β_n ~ N(b, W) with population mean b and covariance W; g(β|θ) population vs. h(β|y,x,θ) conditional (individual-level) distribution.
- **Probit:** ε_n ~ N(0, Ω); error differences ε̃_nji with covariance Ω̃_i = M_iΩM_i′; L = Choleski factor (LL′ = Ω).
- **Estimation:** LL(β) = log-likelihood (divided by N in Ch. 8); SLL = simulated log-likelihood; g_t = gradient, H_t = Hessian, s_n = score; λ = step size.
- **Draws:** η = standard normal draw; μ = standard uniform draw; Φ = standard normal CDF.
- **GEV:** λ_k = nest independence parameter (log-sum coefficient); nests B_k.
- **Bayes:** prior k(θ); posterior K(θ|Y); likelihood (not logged) L(Y|θ); IW = inverted Wishart.

## Key algorithms & pseudo-code locations
(Book pages; add 11 for PDF pages.)
- 4-step frequency (indicator) simulator of any choice probability — p. 5
- Logit log-likelihood, first-order conditions, proof of Σ(y−P)x = 0 — pp. 61–63
- Estimation on a subset of alternatives (uniform conditioning) — pp. 64–66
- Logit probability derivation from extreme value errors (full algebra) — pp. 74–75
- Nested logit probability (eq. 4.2) and inclusive-value decomposition — pp. 80–86
- Accept–reject (AR) probit simulator, 5 steps — pp. 115–117
- Logit-smoothed AR simulator — ~pp. 120–124
- GHK simulator: step-by-step recursion with truncated-normal draws — pp. 126–129 (numbered steps pp. 128–129); GHK as importance sampling — pp. 131–133
- Mixed logit simulated probability (3 steps) and SLL — pp. 144–145
- Newton–Raphson with step-size adjustment (halving/doubling λ) — pp. 187–191
- BHHH / BHHH-2 / steepest ascent / DFP–BFGS updates — pp. ~192–198
- Convergence statistic m_t = g′(−H)^{−1}g — p. 198
- Inverse-CDF draws, ε = −ln(−ln μ) for extreme value — pp. 206–207
- Truncated univariate draws via μ̄ = (1−μ)F(a)+μF(b) — pp. 207–208
- Choleski draw ε = b + Lη from N(b, Ω), worked 3-D example — pp. 208–209
- Importance sampling weights f/g — pp. 210–211
- Metropolis–Hastings algorithm, 6 steps (normalizing constant cancels) — pp. 213–214
- Antithetics / systematic sampling / Halton / randomized & scrambled Halton — pp. ~217–236
- MSL, MSM, MSS definitions and R-vs-N consistency results — pp. 238–245 (headline results p. 239)
- Conditional (individual-level) taste distribution h(β|y,x,θ) and simulated conditional means — pp. 262–267
- Posterior for normal mean (result A) and variance / inverted Wishart (result B) — pp. 294–299
- **Gibbs sampler for HB mixed logit (3 layers, incl. MH step for β_n, burn-in, thinning, adaptive ρ)** — pp. 299–304; succinct restatement p. 304
- Bayesian probit via data augmentation — p. 313
- BLP contraction / control function estimation — pp. 318–342
- General EM iteration and latent-class/nonparametric examples — pp. 348–365
