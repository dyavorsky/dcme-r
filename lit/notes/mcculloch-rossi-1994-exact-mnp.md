# McCulloch & Rossi (1994) — An Exact Likelihood Analysis of the Multinomial Probit Model

**Full citation:** McCulloch, R., & Rossi, P. E. (1994). "An exact likelihood analysis of the multinomial probit model." *Journal of Econometrics*, 64(1–2), 207–240.

**Type:** Methodological journal article (the foundational Bayesian-MNP paper; basis of `bayesm::rmnpGibbs` / `rhierMnpGibbs`)
**Length:** 34 pages (journal pp. 207–240)

## One-paragraph summary

The first feasible Bayesian analysis of the multinomial probit (MNP) model with a full correlated error covariance. The MNP is attractive because it relaxes IIA, but classical MLE/MSM requires evaluating (p−1)-dimensional normal integrals over cones and relies on asymptotic approximations that the authors show are poor for covariance parameters. McCulloch & Rossi construct a Gibbs sampler that exploits the latent-variable structure via data augmentation (following Albert & Chib 1993): conditional on the latent utilities w, MNP is just a Bayesian multivariate regression, so all conditionals are standard (truncated normal, normal, Wishart) and the likelihood is never evaluated. They handle the scale-identification problem with proper-but-diffuse priors and post-hoc normalization (report β/σ₁ etc.), prove geometric ergodicity for the binomial case, run extensive simulation experiments (convergence speed, posterior non-normality, prior sensitivity, initial-condition sensitivity, CPU timing), extend the sampler to a Bayesian hierarchical random-coefficients MNP for panel data, and fit a six-brand margarine choice model to A.C. Nielsen ERIM scanner-panel data (150 households, 2,236 purchases). Variance-components and multiperiod (AR errors) probit extensions round out the paper.

## Key contributions relevant to the book

- The canonical data-augmentation Gibbs sampler for MNP — exactly the algorithm the book's MNP chapter should teach (Section 3, pp. 210–213).
- Textbook-clear explanation of the Gibbs sampler idea via the bivariate case (p. 211).
- Definitive treatment of MNP identification in a Bayesian setting: only scale-free functions (β/σ₁, σᵢⱼ/σ₁₁) are identified; improper priors make the chain a nonconvergent random walk; the fix is proper-but-diffuse priors plus reporting normalized marginals (Section 4, pp. 214–216; Fig. 1, p. 215).
- Empirical demonstration that posterior distributions of variance ratios/correlations are highly non-normal even at N = 6,000 — so asymptotics are unreliable for MNP and exact finite-sample Bayes matters (Figs. 2–3, pp. 219–221).
- The 5-block hierarchical (random-coefficient) MNP sampler (Section 8, pp. 227–229) — the direct ancestor of hierarchical Bayes choice modeling and of `bayesm`.
- Practical MCMC craft: burn-in T*, sensitivity to overdispersed starting values, Newey–West/spectral standard errors for Gibbs-based posterior-moment estimates, autocorrelation and effective-sample-size intuition ("draws ≈ 1/10th as informative as iid" for p = 6), CPU-time regression (Sections 5–7).

## Models & notation

- MNP latent-variable model (Eq. 1, p. 209): z_i = R_i β + u_i, u_i ~ N(0, V), p×1; y_ij = 1 iff z_ij ≥ max(z_i). Differenced w.r.t. alternative p: w_i = X_i β + ε_i, ε_i ~ N(0, Σ), (p−1)-dimensional; choice indicator d_i = 0 if all w_ij < 0, else d_i = argmax.
- Posterior: p(β, Σ | y) ∝ p(β, Σ) l(β, Σ) with l = Π_i Π_j Pr_ij^{y_ij} (Eq. 2, p. 209) — never evaluated directly.
- Priors (Eqs. 3a–3b, pp. 209–210): β ~ N(β̄, A⁻¹) (normal, diffuse via tiny precision A); G = Σ⁻¹ ~ Wishart(ν, V) with small ν for diffuseness (Wishart prior interpretable as an imaginary prior sample of size ν). Proper priors are essential because the likelihood is flat on a manifold (identification).
- Identification (Section 4): (cβ, c²Σ) observationally equivalent to (β, Σ); report marginals of τ = (β′/σ₁, ρᵢⱼ, σⱼ/σ₁); examine the induced prior on τ. Alternative: fix a coefficient β_s = 1 (allows improper priors but requires known sign; discussion pp. 215–216).
- Hierarchical (random-coefficient) MNP for panels (Section 8.1, pp. 227–229): w_it = X_it β_i + ε_it, ε_it ~ iid N(0, Σ); β_i ~ iid N(β̄, V_β); third stage priors β̄ ~ N(μ_β̄, V_β̄) (Eq. 13) and H = V_β⁻¹ ~ Wishart(ν₀, V₀) (Eq. 14). Also notes finite mixture-of-normals first stage with Dirichlet prior on weights as an easy Gibbs extension (Eq. 12, p. 228).
- Variance-components MNP (Eq. 17, p. 235): ε_ij = z_ij + v_ig with G groupings — Bayesian analogue of nested-logit-style correlation structure.
- Multiperiod probit with AR(p) errors (Eqs. 18–19, p. 236): w_it = x_it′β + ε_it, ε_it = Γ_p(B)ε_it + u_it, σ_u² = 1.

## Estimation details

**Basic MNP Gibbs sampler (Section 3, pp. 210–213).** Data augmentation: add latent w to the parameter set; conditional on w, MNP = Bayesian linear model. Cycle through three blocks (Eq. 4, p. 212):

1. **w_ij | w_i,−j, β, G, d_i** for i = 1..N, j = 1..p−1: each latent utility component is univariate truncated normal. Mean/variance from partitioning G (Eq. 5, p. 212): m_ij = x_ij′β + F′(w_i,−j − X_i,−j β), τ_ij² = E⁻¹ with E = σ_jj − σ_j(−j)Σ⁻¹σ_(−j)j. Truncation: if d_i = j then w_ij > max(w_i,−j, 0); else w_ij < max(w_i,−j, 0). Gibbsing through components avoids drawing directly from a truncated MVN over a cone. Truncated-normal draws via spliced rejection methods: exponential rejection (Devroye), half-normal, and direct rejection (Geweke 1991) depending on truncation region (pp. 212–213).
2. **β | w, G**: premultiply by Cholesky root C of G (G = CC′) to whiten errors (Eq. 6), then standard conjugate normal posterior β | w, G ~ N(β̂, Σ_β), Σ_β = (X*′X* + A)⁻¹, β̂ = Σ_β(X*′w* + Aβ̄) (Eq. 7, p. 213).
3. **G | β, w**: conjugate Wishart posterior G ~ W(ν + N, V + Σᵢ εᵢεᵢ′), εᵢ = wᵢ − Xᵢβ (Eq. 8, p. 213). Wishart draws via Bartlett decomposition: chi-square square roots on the diagonal, N(0,1) off-diagonal, premultiplied by lower-triangular factor (p. 213).

Start from prior modes of β and G with w = 0 (p. 212).

**Hierarchical MNP sampler (Section 8.1, p. 229, Eq. 15).** Five conditional blocks: (1) w_itj | w_it,−j, {β_i}, G, β̄, H, d; (2) β_i | w, G, β̄, H; (3) G | w, {β_i}, β̄, H; (4) β̄ | {β_i}, G, H — multivariate normal; (5) H | {β_i}, β̄ — Wishart(ν₀ + N, (V₀ + Σ(β_i − β̄)(β_i − β̄)′)). Individual-household posteriors p(β_i | data) come "free" by saving β_i draws (Eq. 16, p. 229) — no plug-in of hyperparameter MLEs needed.

**Theoretical convergence (Section 5.1, pp. 216–217; Appendix pp. 236–238).** Strictly positive transition kernel ⇒ irreducible, aperiodic, unique invariant distribution = posterior; ergodicity gives LLN/CLT for posterior-moment estimates. Appendix proves geometric ergodicity of the binomial-probit sampler via a drift/minorization argument (g(x) = w₁², bounded β, G bounded away from zero) — Albert & Chib noted fast convergence but did not prove it.

**Practical convergence and inference (Sections 5.2–7, pp. 217–227).**
- Burn-in: discard first T* draws; assess by running many short chains (5,000 draws) from widely dispersed starts and comparing marginals of the last few thousand draws; MNP sampler converges "within only a few hundred draws" (p. 217). Gelman–Rubin overdispersed-start diagnostics impractical here because initial conditions include the latent w (p. 218).
- Then one long run of T** draws, keep T = T** − T*; Gibbs output is a stationary ergodic time series with complicated autocorrelation and conditional heteroskedasticity; use spectral/Newey–West (Bartlett-weight) standard errors for moment estimates (p. 218). For p = 6, lag-200 Newey–West; draws roughly 1/10 as informative as iid (p. 223).
- Simulation findings (Section 6): posterior of σ₂₂/σ₁₁ highly skewed even with 500–1,000 obs/parameter; normality only near N = 6,000 (Fig. 2, p. 220). Sampling distribution of the Börsch-Supan/Hajivassiliou simulated MLE of the same ratio is nearly identical — skewness is a feature of the parameter, but Bayes avoids delta-method asymptotics entirely (Fig. 3, p. 221). Regression coefficients are fine asymptotically; bounded functions (variance ratios, correlations, choice probabilities) are not (pp. 221–222).
- Prior sensitivity (Fig. 4, pp. 223–224): halving/doubling prior precision on β and tightening ν from 6 to 12 leaves posteriors virtually unchanged (ν ≥ p needed for a proper Wishart).
- Initial-condition sensitivity (Figs. 5–6, pp. 223–226): nine-point two-factor orthogonal design of (β_i, Σ_j) starts; last 4,000 of 5,000 draws give essentially identical marginals.
- Timing (Section 7, p. 227): Secs/100 draws = 0.63 + 0.0081N(p−1) + 0.00024N(p−1)² + 0.000074N(p−1)k² + 0.0059k³ (on a Sparc 2); e.g., N=1000, p=6, k=5 → 9.5 min per 1,000 draws.

**Empirical application (Section 8.2, pp. 230–234).** ERIM margarine panel: 150 households, 2,236 purchases, 6 brands; regressors = 5 brand intercepts + log price. Priors: Σ⁻¹ ~ W(p+4, (p+4)I_p), β̄ ~ N(0, 100I_k), V_β⁻¹ ~ W(k+4, (k+4)I_k). 15,000 draws, last 11,000 kept; numerical SEs < 0.001. Mean normalized price coefficient −5.2 with across-household SD 3.1 (Table 3, p. 232); household-level price-coefficient posteriors from saved β_i draws (Fig. 7, p. 233); several error correlations well away from zero, rejecting independence probit (Fig. 8, p. 234).

## Relevance to book chapters

- **MNP chapter:** this is *the* source. The 3-block Gibbs sampler (truncated normal w / normal β / Wishart G), the identification discussion, and the normalization-by-σ₁₁ reporting convention map directly onto `bayesm::rmnpGibbs`.
- **Bayes-MCMC intro:** the bivariate Gibbs explanation (p. 211), data augmentation as "conditional on w it's just regression," conjugate normal/Wishart updates, burn-in, and time-series standard errors for MCMC output are all core teaching material.
- **HB-MNL / hierarchical models:** Section 8's 5-block hierarchical sampler is the generic HB architecture (unit-level draws + multivariate-regression hyperparameter draws) reused in HB-MNL; Eq. 16's "individual posteriors for free" is the key selling point.
- **Mixed logit / latent class:** Eq. 12's finite mixture-of-normals heterogeneity with Dirichlet prior and latent indicators anticipates the latent-class/mixture chapters.
- **Bayes vs. classical:** Sections 5.2–6 give concrete evidence on when asymptotics fail (bounded parameters) and show Bayesian and classical sampling distributions nearly coincide for this model — nuanced material for the comparison discussion.

## Page pointers

- p. 207: abstract — Gibbs variant, exact posterior, avoids choice-probability evaluation
- p. 208: why MNP is hard for MLE/MSM (cone integrals, asymptotics, bootstrap impractical); first feasible Bayesian MNP claim
- p. 209: latent-variable MNP (Eq. 1); differencing to w; identification problem introduced; priors (Eq. 3a)
- p. 210: Wishart prior (Eq. 3b); how to make priors diffuse but proper
- p. 211: Gibbs sampler intuition (bivariate case); data augmentation; Albert & Chib (1993) credit; strategy = marginal of (β, G) from (w, β, G) chain
- p. 212: three conditional blocks (Eq. 4); partitioned-G conditional moments (Eq. 5); truncation logic
- p. 213: truncated-normal rejection methods; β draw (Eqs. 6–7); Wishart draw (Eq. 8) with Bartlett construction
- pp. 214–216: identification; random-walk behavior under improper priors (Fig. 1); proper-diffuse-prior solution; β_s = 1 alternative; Bernoulli-prior-on-sign discussion
- pp. 216–218: theoretical convergence (irreducibility, ergodicity); burn-in T*; multiple-start diagnostics; multimodality discussion; time-series inference for Gibbs output
- pp. 219–222: posterior non-normality experiments (Figs. 2–3); when asymptotics fail
- pp. 222–226: six-choice equicorrelated example (Eq. 9, Table 1); prior sensitivity (Fig. 4); initial-condition sensitivity (Figs. 5–6, Table 2)
- p. 227: CPU-timing regression
- pp. 227–229: hierarchical random-coefficient MNP; priors (Eqs. 13–14); 5-block sampler (Eq. 15); household-level posteriors (Eq. 16)
- pp. 230–234: ERIM margarine panel application (Table 3, Figs. 7–8); priors used; 15,000-draw run
- pp. 234–236: variance components (Eq. 17); multiperiod AR(p) probit (Eqs. 18–19); hybrid Gibbs/Metropolis note for ARMA (fn. 5)
- pp. 236–238: Appendix — geometric ergodicity proof (drift condition) for binomial case
