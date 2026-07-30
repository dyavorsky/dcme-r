# Train (2001) — A Comparison of Hierarchical Bayes and Maximum Simulated Likelihood for Mixed Logit

**Full citation:** Train, K. (2001). "A Comparison of Hierarchical Bayes and Maximum Simulated Likelihood for Mixed Logit." Working paper, Department of Economics, University of California, Berkeley (dated June 18, 2001). (Material later incorporated into Ch. 12 of Train, *Discrete Choice Methods with Simulation*.)

**Type:** Methodological working paper; head-to-head comparison of estimation strategies
**Length:** 13 pages

## One-paragraph summary

Train specifies a panel mixed logit and estimates it two ways — classical maximum simulated likelihood (MSL) and Bayesian MCMC (hierarchical Bayes, HB) — then systematically varies the specification (independent normals, full-covariance normals, some fixed coefficients, lognormals, triangulars) to show how each method's programming effort and run time respond. Both methods give essentially the same answers on the RTI/EPRI energy-supplier stated-choice data (361 customers, up to 12 choice situations, 4 alternatives, 6 attributes). The paper's theoretical core is the Bernstein–von Mises argument: the simulated posterior mean is a classical estimator asymptotically equivalent to MLE, and its consistency/asymptotic-normality conditions are *weaker* than MSL's (which needs simulation draws to rise faster than √N). Practically: HB wins for full-covariance normals (run time ~55 vs 139 min) and for lognormals (where MSL often fails to converge); MSL wins for fixed coefficients (HB needs an extra M-H layer, doubling run time) and decisively for bounded-support (triangular) distributions, where the HB chain converges "exceedingly slowly" (4× run time).

## Key contributions relevant to the book

- The clearest published statement of the HB-mixed-logit Gibbs/M-H sampler with all conditionals spelled out (Section 2.2, pp. 3–5) — the algorithm behind Sawtooth CBC/HB, `bayesm::rhierMnlRwMixture`, and Train's own GAUSS/Matlab code.
- Bernstein–von Mises "posterior mean as classical estimator" (Section 2.3, p. 5): three statements — (1) posterior converges to N(mean, B⁻¹/N); (2) posterior mean converges to the MLE; (3) √N(posterior mean − θ*) →d N(0, B⁻¹), so posterior standard deviations are valid classical standard errors. Justifies teaching HB even to frequentist students.
- Simulation-noise comparison (p. 5): simulated posterior mean with R independent draws has variance (1 + 1/R) times the exact posterior mean's and is consistent for fixed R rising with N at any rate; MSLE is inconsistent for fixed R and needs R rising faster than √N for asymptotic normality — a condition hard to verify, making HB "attractive relative to MSLE."
- Specification-by-specification convenience scoreboard (Table 2, p. 13) — great for a lecture on choosing an estimation strategy:
  - All normal, no correlation: MSL 48 min, HB 53 (tie)
  - All normal, full covariance: MSL 139, HB 55 (HB wins; Bayesian cost of correlation ≈ 0)
  - 1 fixed + rest normal: MSL 42, HB 112 (MSL wins)
  - 3 lognormal + 3 normal: MSL 69 (when it converges at all), HB 54 (HB wins)
  - All triangular: MSL 56, HB 206 (MSL wins)
- Practical wisdom on lognormals under MSL (p. 9): flat/singular Hessians, sensitivity to starting values, local-vs-global ambiguity — HB sidesteps all of it because it never searches for a maximum.

## Models & notation

- Mixed logit (Eqs. 1–3, p. 2): U_njt = β_n′x_njt + ε_njt, ε iid extreme value; β_n ~ N(b, Ω) (Ω diagonal in Section 2, full in Section 3). Conditional choice-sequence probability L(y_n | β_n) = Π_t [exp(β_n′x_n,y_nt,t) / Σ_j exp(β_n′x_njt)] (Eq. 2); unconditional P_n(y_n | b, Ω) = ∫L(y_n | β)g(β | b, Ω)dβ (Eq. 3).
- Classical: SLL(b, Ω) = Σ_n ln P̂_n with P̂ an average of L over draws from g (Eqs. 4–5, p. 3). MSLE consistent if R rises with N; asymptotically normal/efficient (≡ MLE) if R rises faster than √N (Hajivassiliou & Ruud 1994; McFadden & Train 2000). Individual-level β_n via Revelt & Train (2000) conditioning.
- Bayesian priors (Section 2.2, p. 3): flat prior on b (improper uniform, or effectively-flat proper normal); each diagonal element of Ω ~ inverted gamma with 1 df and scale 1 (notation IG(Ω | 1, ℓ), ℓ a K-vector of ones). Joint posterior Λ(β_n ∀n, b, Ω | Y) ∝ Π_n L(y_n | β_n) g(β_n | b, Ω) · IG(Ω | 1, ℓ) (Eq. 6). Full-covariance case: Ω ~ inverted Wishart IW(K, KI) with posterior IW(K + N, KI + N·V̄) (Section 3, p. 7).
- Fixed + random coefficients (Eqs. 7–8, p. 8): U_njt = α′z_njt + β_n′x_njt + ε_njt with α fixed across people.
- Lognormals (Eqs. 9–10, p. 9): U_njt = (e^{β_n})′x_njt + ε_njt; draw normals, exponentiate in utility — HB machinery otherwise unchanged.
- Triangular distribution draw (p. 9): β_n = b + s(√(2μ) − 1) if μ < .5, else b + s(1 − √(2(1−μ))), μ ~ U(0,1).

## Estimation details

**HB Gibbs sampler with data augmentation on β_n (pp. 3–5).** Three blocks, iterated:

1. **b | {β_n}, Ω ~ N(β̄, Ω/N)** where β̄ = (1/N)Σβ_n (flat prior ⇒ standard normal Bayesian update; Zellner 1971). Drawn cheaply: b_k = β̄_k + (σ_k/√N)η, η ~ N(0,1).
2. **Ω | b, {β_n}**: diagonal case — each element inverted gamma IG(1 + N, (ℓ + N·V̄_k)/(1+N)) with V̄ = (1/N)Σ(β_n − b)², drawn via 1 + N standard-normal deviates: σ̃_k² = (1 + N·V̄_k)/Σ_r η_r². Full-covariance case — inverted Wishart IW(K + N, KI + N·V̄); draw by K + N K-dimensional normal deviates, Choleski factor of (KI + N·V̄)⁻¹, S = Σ(Mη_r)(Mη_r)′, Ω = S⁻¹ (p. 7).
3. **β_n | b, Ω for each n**: conditional posterior ∝ L(y_n | β_n) g(β_n | b, Ω) — nonconjugate (logit likelihood), so one **Metropolis–Hastings step per person per iteration**: (i) d = ρLη with L = Choleski of Ω, η ~ N(0, I), ρ a tuning scalar; (ii) trial β̃_n¹ = β_n⁰ + d; (iii) R = [L(y_n | β̃_n¹)g(β̃_n¹ | b, Ω)] / [L(y_n | β_n⁰)g(β_n⁰ | b, Ω)]; (iv) draw μ ~ U(0,1); (v) accept if μ < R else keep β_n⁰. One M-H draw per person per Gibbs iteration suffices — convergence of the M-H chains and the overall Gibbs chain "is attained simultaneously" (p. 4).
   - **Adaptive tuning of ρ** (pp. 4–5): target acceptance rate ≈ 0.4 for K = 1 falling to ≈ 0.23 in high dimensions (Gelman et al. 1995); following Sawtooth (1999), lower ρ when acceptance < 0.3, raise when > 0.3, each iteration.

**Fixed coefficients under HB (p. 8):** α cannot ride along in each person's M-H step (different people would accept different values of a "fixed" parameter). Extra Gibbs layer: (i) β_n | α, b, Ω ∀n by M-H with α′z in the logit; (ii) b | {β_n}, Ω normal; (iii) Ω | {β_n}, b IW; (iv) α | {β_n} ∝ Π_n L(y_n | α, β_n) by **M-H on pooled data**. Layer (iv) costs as much as layer (i) ⇒ run time roughly doubles (confirmed: 112 vs ~54 min).

**Bounded-support distributions under HB (p. 10):** with flat priors on triangular (b, s): (i) β_n | b, s ∝ L·h(β_n | b, s) by M-H per person; (ii) (b, s) | {β_n} ∝ Π h(β_n | b, s) by M-H. Bounded support cripples mixing: β_n draws outside (b − s, b + s) are auto-rejected in (ii), and (b, s) draws whose range fails to cover all current β_n are auto-rejected, so the range can barely move between iterations — run time ×4 for "a semblance of convergence."

**Classical side:** full covariance triples MSL run time (27 vs 12 parameters, more gradient work, more iterations; p. 6–7); fixing coefficients speeds MSL; lognormals inflate MSL time ~50% *when* a maximum is found; triangulars are trivial (only the draw line changes).

**Empirical comparison (Section 2.4, p. 6; Table 1, p. 13):** MSL and HB posterior means/SDs nearly identical; HB scale slightly larger (posterior skewed, mean > mode); rescaling MSL to match the price-coefficient mean makes the two sets "remarkably close" in both point estimates and standard errors.

## Relevance to book chapters

- **Mixed logit:** the core reference for estimating mixed logit both ways; Section 2's model + both procedures is essentially the book's mixed-logit chapter outline (MSL via `mixl`/`mlogit`/`gmnl`, HB via `bayesm`/RSGHB).
- **HB-MNL:** the 3-block sampler (normal b / IW Ω / per-person random-walk M-H with adaptive ρ) is exactly `rhierMnlRwMixture`'s architecture; the fixed-coefficient extension explains why "fixed" parameters are awkward in HB code.
- **Bayes-MCMC intro / Bayes-vs-classical:** Section 2.3's Bernstein–von Mises discussion is the cleanest bridge for econometrics students — posterior means as classical estimators with weaker simulation requirements than MSLE.
- **MNP:** notes the parallel classical (GHK) vs Bayesian (Albert–Chib; McCulloch–Rossi) split for probit, with Bolduc et al. finding Bayes ~2× faster (p. 1).
- **Practical estimation chapter:** Table 2's run-time scoreboard and the lognormal-convergence war stories are ideal for a "which tool when" discussion; WTP-distribution and fixed-price-coefficient rationale (p. 7) previews WTP-space debates.

## Page pointers

- p. 1: framing — asymptotic equivalence, Huber & Train (2001) similarity result; probit analogues (GHK vs Albert–Chib/McCulloch–Rossi); which comparisons carry over to probit
- p. 2: theoretical advantages of Bayes from both perspectives; mixed logit model (Eqs. 1–3)
- p. 3: MSL (Eqs. 4–5) and consistency conditions; Bayesian priors (flat b, IG variances) and joint posterior (Eq. 6)
- p. 4: conditional posteriors for b (normal) and Ω (IG); per-person M-H algorithm in 5 numbered steps; ratio R; simultaneous convergence remark; optimal acceptance rates (.4 → .23)
- p. 5: adaptive ρ rule (Sawtooth, threshold .3); Bernstein–von Mises statements 1–3; simulation variance (1 + 1/R); MSLE draw-growth requirements
- p. 6: energy-supplier data (361 customers, ≤12 situations, 4 suppliers, 6 attributes); Table 1 discussion — skewed posterior, scale difference, scaled-MSL closeness; Section 3 full covariance, Choleski parameterization for MSL
- p. 7: inverted Wishart prior/posterior and draw algorithm; run-time tripling for MSL vs unchanged HB; reasons to fix coefficients (Ruud identification caution, ASC mixture unidentifiability, substitution-pattern focus, WTP)
- p. 8: fixed coefficients — easy classically; HB needs extra M-H layer (conditionals i–iv); run-time doubling
- p. 9: lognormals (Eqs. 9–10) — MSL convergence failures vs untroubled HB; triangular density and draw formula
- p. 10: bounded-support HB conditionals and the slow-convergence mechanism; conclusions — normals/lognormals favor HB, fixed and bounded-support coefficients favor MSL
- p. 13: Table 1 (MSL vs HB vs scaled-MSL estimates, SEs); Table 2 (run times in minutes across five specifications)
