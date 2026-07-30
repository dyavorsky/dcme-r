# Package: gmnl

**Full citation / authors:** Sarrias, Mauricio and Ricardo A. Daziano (2017). "Multinomial Logit Models with Continuous and Discrete Individual Heterogeneity in R: The gmnl Package." *Journal of Statistical Software*, 79(2), 1-46. doi:10.18637/jss.v079.i02.
**Type:** R package manual/vignette (JSS article)

## What it estimates
One function, six models selected by the `model` argument (Table 2, p. 13):
- `"mnl"`: standard MNL/conditional logit.
- `"mixl"`: mixed logit (MIXL) — continuous random parameters, optionally correlated, optionally with observed heterogeneity in the means (beta_i = beta + PI*z_i + L*eta_i).
- `"smnl"`: scale heterogeneity MNL (S-MNL, Fiebig et al. 2010) — individual-specific error scale sigma_i = exp(sigma_bar + delta's_i + tau*v_i); covariates can enter the scale.
- `"gmnl"`: generalized multinomial logit (G-MNL, Fiebig et al. 2010) — beta_i = sigma_i*beta + [gamma + sigma_i(1-gamma)]*L*eta_i; nests MNL, MIXL, S-MNL, G-MNL-I (gamma=1), G-MNL-II (gamma=0). Only R package that fits G-MNL.
- `"lc"`: latent class MNL (LC-MNL), Q classes, class-membership probabilities optionally driven by socio-economic covariates (semiparametric MNL form for w_iq).
- `"mm"`: mixed-mixed MNL (MM-MNL) — discrete mixture of multivariate normals; nests both MIXL (Q=1) and LC (Sigma_q -> 0). Only frequentist/MSLE implementation (bayesm does it Bayesian).
Also supports **WTP-space models** (Sec. 3.7) by re-using the S-MNL/G-MNL machinery with fixed price coefficient and gamma.

## Estimation approach
- MNL and LC-MNL: exact **MLE** with analytical gradients (analytical Hessian for MNL); no simulation needed for LC.
- All others: **maximum simulated likelihood (MSLE)** with analytical gradients, via `maxLik` (default `method = "bfgs"`; BHHH and NR available).
- Draws: `R` = number of draws; `haltons = NA` (default) uses first-K-primes Halton draws, `NULL` uses pseudo-random, or a list `list(prime = c(...), drop = ...)` for custom primes/burn-in.
- Random-parameter distributions (`ranp`, Table 3, p. 18): "n" normal, "ln" log-normal, "cn" truncated-at-zero normal, "t" triangular, "u" uniform, "sb" Johnson S_b. With `correlation = TRUE` only normal-related distributions allowed.
- G-MNL details: tau (sd of scale), gamma estimated directly (Keane & Wasi 2013) or via logistic transform (`hgamma = "indirect"`); `typeR` chooses truncated-normal vs. Greene-Hensher (2010) capped draws for the scale; `notscale` flags variables (typically ASCs) excluded from scaling; `fixed` pins parameters (e.g., gamma = 0); `init.gamma`, `print.init`, `start` for starting values (G-MNL not globally concave — the paper recommends warm-starting from simpler models).
- Individual-level **conditional (posterior) estimates** of beta_i and WTP_i via Bayes' theorem (Sec. 3.8, eqs. 6-7), with approximate 95% intervals; caveats about conditional variance noted.
- Model comparison via lmtest's `waldtest`/`lrtest`, `AIC`/`BIC`.
- Sec. 4: computational issues — seed sensitivity of pseudo-random draws, number of draws ("increase until estimates stabilize"), starting values, weak identification (check Hessian eigenvalues).

## Data format expected
- Uses the **mlogit data format**: data must be prepared with `mlogit.data()` (long or wide input; `choice`, `shape`, `alt.levels`, `id.var` for panels, `varying` + `sep` for wide, `opposite` to negate covariates). gmnl errors if data are not of this class.
- Panel data: set `id.var` in `mlogit.data()` and `panel = TRUE` in `gmnl()`.
- **Five-part formula** (Formula package): `choice ~ asv | isv.altcoef | isv.for.random.means-part? | mvar-vars | scale-or-class-vars`
  1. alternative-specific variables with generic coefficients,
  2. individual-specific variables with alternative-specific coefficients (use `1` for ASCs, `0`/`-1` to drop),
  3. alternative-specific variables with alternative-specific coefficients,
  4. variables entering the **mean of random parameters** (deterministic taste variation; pair with `mvar = list(travel = c("income","size"))`),
  5. variables entering the **scale parameter** (S-MNL/G-MNL het.) or the **class-membership probabilities** (LC/MM-MNL; at minimum `| 1`).

## Key functions
- `gmnl(formula, data, model, ranp, R, haltons, panel, correlation, mvar, Q, notscale, typeR, hgamma, fixed, start, init.gamma, subset, weights, method, iterlim, print.init)`: single entry point for all six models.
- `mlogit.data()` (imported from mlogit): data preparation.
- `wtp.gmnl(model, wrt = "price_var")`: WTP point estimates + delta-method SEs from a preference-space model.
- `effect.gmnl(model, par, effect = "ce"/"wtp", wrt)`: individual conditional means (and SDs) of parameters or WTP.
- `plot(x, par, effect = "ce", type = "density", ind = TRUE, id = ...)`: kernel density or per-individual CI plots of conditional means.
- `vcov(x, what = "ranp", type = "cov"/"sd"/"cor", se = TRUE, Q = )`: covariance/correlation/SDs of random parameters with delta-method SEs (uses msm::deltamethod); Q selects class in MM-MNL.
- S3 methods: `summary`, `AIC`, `BIC`, `update`; works with lmtest (`waldtest`, `lrtest`).

## Relevance to book chapters
- **Mixed logit / MSLE chapter**: the most complete frequentist-MSLE reference implementation — validate hand-coded simulated likelihoods, Halton draws, correlated random parameters (Cholesky L), and observed heterogeneity in means (the `mvar` hierarchical mean beta_i = beta + PI*z_i + L*eta_i maps directly to the HB upper-level regression).
- **Latent class chapter**: LC-MNL and MM-MNL by direct MLE/MSLE — a frequentist counterpart to Bayesian finite-mixture MNL (bayesm); the MM-MNL nesting result (MIXL and LC as special cases) is good exposition material.
- **Scale heterogeneity / WTP-space**: only R package with G-MNL/S-MNL; Sec. 3.7 gives a clean derivation of WTP-space vs. preference-space and why WTP ratios of normals misbehave (Daly-Hess-Train) — directly relevant if the book covers WTP.
- **Individual-level estimates chapter**: Sec. 3.8's Bayes-theorem conditional means (with simulators for continuous/discrete/mixture cases) are the frequentist analogue of HB individual draws — good for comparing hand-coded HB posteriors with `effect.gmnl` output.
- Table 1 (p. 5) is a handy survey of R packages by model (MNL/MNP/MIXL/G-MNL/S-MNL/LC/MM-MNL) and estimation procedure — citable in the book's software overview.
- Uses the same `Electricity` and `TravelMode` datasets as mlogit — convenient for cross-package validation exercises.

## Page pointers
- p. 1-4: abstract, intro, model landscape, package survey.
- p. 5: Table 1 — R packages by model and estimator.
- p. 6-8: MIXL and LC theory; MM-MNL (Sec. 2.2).
- p. 8-9: G-MNL theory, sub-models, identification/normalization of scale, MSLE + maxLik.
- p. 9-11: data format via `mlogit.data`, TravelMode example, long-to-wide reshaping.
- p. 11-13: five-part formula interface; Table 2 model codes.
- p. 12-17: S-MNL examples (notscale, scale covariates, typeR), Wald/LR tests, AIC/BIC.
- p. 17-21: MIXL with `mvar` hierarchical means, `haltons` customization; correlated random parameters on Electricity panel; `vcov(what = "ranp")`.
- p. 22-25: G-MNL estimation, hgamma, fixed/init.gamma, starting-value strategy.
- p. 25-31: LC (`model="lc"`, `Q`) and MM-MNL (`model="mm"`, correlated) examples.
- p. 31-37: WTP-space (wtp.gmnl; S-MNL and G-MNL WTP-space with fixed price and gamma; correlated WTP).
- p. 37-40: individual conditional estimates (eqs. 6-7), plot/effect.gmnl.
- p. 40+: computational issues (draws, seeds, starting values, weak identification).
