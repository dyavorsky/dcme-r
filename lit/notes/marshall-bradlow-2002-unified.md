# Marshall & Bradlow (2002) — A Unified Approach to Conjoint Analysis Models

**Full citation:** Marshall, P., & Bradlow, E. T. (2002). A Unified Approach to Conjoint Analysis Models. *Journal of the American Statistical Association*, 97(459), 674-682.
**Type:** Methodological journal article (Bayesian; Applications and Case Studies section)
**Length:** 9 journal pages (674-682; PDF has 10 pp. incl. JSTOR cover)

## One-paragraph summary

Marshall & Bradlow build a "one model fits all" Bayesian framework for conjoint data: self-explicated ratings form the *prior* on each respondent's latent partworth vector, while full-profile evaluations — whether ratings, constant-sum, rankings, or discrete choice — form the *likelihood* through format-specific link functions applied to the same underlying latent utilities. Standard models (profile-only, self-explicated-only, hybrid) drop out as special cases, and the Bayesian machinery resolves the long-standing ad hoc question of how much weight to give profile vs. self-explicated data: the posterior mean is a precision-weighted average of the two sources. Estimation is by Gibbs sampling with data augmentation (Tanner-Wong) and Metropolis-Hastings for non-conjugate outcome forms. Applied to the KGU98 automobile conjoint data (128 respondents, 6 attributes) and a simulation, the key empirical finding is that *data format matters as much as model choice*: degrading rich constant-sum data to rankings or choices loses information, and the self-explicated prior helps most when calibration and validation data formats are incongruent.

## Key contributions relevant to the book

1. **A unifying latent-utility view of conjoint outcome scales.** One latent continuous utility model (Eq. 2) plus different observation/link equations yields rating, sum-to-1, ranking (exploding logit), and binary/discrete choice (logit) models. Pedagogically ideal for showing students that "ratings conjoint," "ranking conjoint," and "CBC" differ only in the likelihood layer, not the utility layer (Sec. 3.3, pp. 676-677).
2. **Principled data fusion.** The posterior mean of partworths μ_i is a matrix-weighted average of self-explicated u_i and the regression estimate from profile data (Eq. 3, p. 676) — eliminating "ad hockery in the relative weighting of full profile and self-explicated data sources." Limiting cases: Ω⁻¹→0 gives the classical profile-only regression estimator; σ⁻²→0 gives the pure self-explicated model (p. 676).
3. **Prior information relaxes design requirements:** X_i need not be full rank; proper posteriors obtain even with few profile evaluations (p. 676) — relevant to partial-profile and sparse designs.
4. **Empirical lesson on information loss (Secs. 4-5):** transforming the same constant-sum data to ranks or first choices worsens out-of-sample fit (higher RMSE/MAD, lower correlation); the Bayesian model's gains over profile-only are largest exactly for the degraded (ranking, choice) formats, i.e., the prior compensates for lost likelihood information (Tables 1-3, p. 679; Table 5, p. 681).
5. **Congruence principle:** whether self-explicated data add value depends on the (in)congruity between calibration and validation data formats — same-format calibration/validation makes the prior nearly redundant; format mismatch makes it valuable (abstract; Sec. 4.2.4, p. 679).

## Models & notation

(Sec. 3, pp. 675-677; i indexes respondents, k = number of identified attribute-level parameters, m profiles in b blocks of p)
- Prior from self-explicated data: [μ_i | u_i, Ω] ~ N_k(u_i, Ω) (Eq. 1, p. 675); u_i = observed self-explicated partworths (desirability × importance ratings); Ω common across respondents.
- Likelihood from profile ratings: [y_i | μ_i, σ²] ~ N_m(X_i μ_i, σ² I_m) (Eq. 2, p. 675) — the traditional full-profile conjoint regression.
- Posterior (normal-normal): [μ_i | y_i, σ², Ω] ~ N(A_i⁻¹Ω⁻¹u_i + A_i⁻¹X_i′y_i/σ², A_i⁻¹), A_i⁻¹ = [Ω⁻¹ + X_i′X_i/σ²]⁻¹ (Eq. 3, p. 676).
- Hyperpriors: σ² inverse chi-squared (g₀ dof), Ω inverse Wishart (d₀, D₀) — hierarchical normal-Wishart (p. 676).
- Different scales for prior vs. likelihood: μ_i ~ N_k(Z_i α; Ω) with Z_i = (ι, u_i), α = 2-vector intercept/scale, Gaussian prior on α, conditional posterior Eq. 6 (p. 677).
- Constant-sum link: y*_ijk = y_ijk / Σ_k y_ijk within block (Eq. 7, p. 677); latent y_i unobserved, σ² = 1 for identification, positivity enforced by rejection.
- Ranking link: exploding logit of Chapman & Staelin (1982): P(y*_ijk = z) = e^{y_ijz}/Σ_{k≥z} e^{y_ijk} (Eq. 8, p. 677).
- Discrete choice link: y*_ijk = 1 if profile k most preferred in block j; logit P(y*_ijk=1) = e^{y_ijk}/Σ_k e^{y_ijk} following Allenby et al. (1995) (Eq. 9, p. 677); pairwise conjoint is the p = 2 special case.

## Estimation details

- **MCMC:** Gibbs sampler cycling through full conditionals [μ_i | ...] (Eq. 3), [σ² | ...] ~ IW/inverse chi-squared (Eq. 4), [Ω | ...] ~ IW(d₀+n, D₀ + Σ(μ_i−u_i)(μ_i−u_i)′) (Eq. 5) (p. 676). Diffuse priors via d₀=1, D₀=0, g₀=1, G₀=0.
- **Data augmentation** (Tanner & Wong 1987) for non-rating outcomes: draw latent y_i given observed y*_i — rejection sampling for constant-sum positivity (p. 677); sequential truncated draws (min, then next-smallest, ...) for rankings, via truncated-normal inversion (Allenby et al. 1995) (p. 677); Metropolis-Hastings for the binary/choice case where Bernoulli-product conditionals are non-conjugate (p. 678).
- **Application (Sec. 4, pp. 678-680):** KGU98 auto data — 128 students, 6 attributes (make, mpg, price, color, sound system, warranty), 64-profile orthogonal main-effects master plan, blocks of p=4, b=8 blocks per respondent seen twice (calibration/validation); self-explicated 0-10 desirabilities × 100-point constant-sum importances. 10,000 MCMC draws, first 2,500 burn-in; convergence via multiple chains (Gelman-Rubin). Three analyses treat calibration data as constant-sum, ranks, and choices; fit stats: RMSE, MAD, correlation, proportion first choice, proportion correct ranking, MAD of rank vectors; "pure error" benchmark = predicting validation with calibration responses themselves (p. 678).
- **Findings:** sum-to-1: Bayesian ≈ profile-only ≈ pure error; self-explicated-only worst (Table 1, p. 679). Rankings and choices: Bayesian beats profile-only on most metrics (Tables 2-3, p. 679). Simulation (3×3×3+1 design, Table 5, p. 681): Bayesian always ≥ profile-only and self-explicated-only, gains largest for ranking/choice data and small σ²; predictive ability degrades monotonically actual → sum-to-1 → ranking → choice.
- Notes BUGS-style software makes the whole family implementable as Bayesian hierarchical regressions (p. 681).

## Relevance to book chapters

- **Choice framework:** the cleanest published statement that rating, ranking, constant-sum, and choice conjoint share one latent-utility core and differ only in link/likelihood — a good organizing idea when the book transitions from linear models to MNL.
- **Data organization:** blocks-of-p structure, calibration vs. validation blocks, and the point that the same latent data can be expressed as ratings/ranks/choices; cautionary evidence about converting data between formats.
- **MNL:** Eq. 9 is exactly the MNL/CBC likelihood; the exploding logit (Eq. 8) is the natural extension for ranked data (rank-ordered logit).
- **HB-MNL:** a compact hierarchical normal model with inverse-Wishart hyperprior, Gibbs + data augmentation + M-H — essentially the same architecture as bayesm/ChoiceModelR HB-MNL, but with an informative, respondent-specific prior mean (u_i) instead of a common population mean. Good "where the prior comes from" discussion, incl. rescaling when prior and likelihood scales differ (Eq. 6).
- **Post-estimation / market simulation:** indirect — out-of-sample validation metrics (first-choice hit rate, share-type RMSE/MAD) are the same ones used to validate simulators.
- **Experimental design:** blocked orthogonal main-effects plan; prior information permitting rank-deficient X_i.
- **Conjoint practice:** hybrid/self-explicated methods (ACA/HB lineage), and the practical warning that outcome-format choice has first-order effects on predictive accuracy.

## Page pointers

- p. 674: abstract; intro — variety of outcome scales, block sizes, data sources; contribution statement
- p. 675: related work (hybrid models, ACA/HB, Srinivasan & Park baseline); Sec. 3.1 — Eqs. 1-2, k identified parameters example
- p. 676: posterior Eq. 3 and weighting interpretation; special cases (Ω⁻¹→0, σ⁻²→0); precision gains; rank-deficient X_i; hyperpriors; Gibbs full conditionals Eqs. 4-5
- p. 677: different scales (Eq. 6); constant-sum (Eq. 7), ranking/exploding logit (Eq. 8), discrete choice logit (Eq. 9); data-augmentation schemes
- p. 678: M-H for choice case; KGU98 data & design; self-explicated construction; three analyses
- p. 679: Tables 1-3 out-of-sample fit by data format; congruence discussion
- p. 680: Table 4 self-explicated comparisons (beats Srinivasan-Park variant); Sec. 5 simulation design
- p. 681: Table 5 simulation results; conclusions — one framework, weighting solved, information loss from transforming data; BUGS remark
- p. 682: references
