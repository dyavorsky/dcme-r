# Package: Rchoice

**Full citation / authors:** Sarrias, Mauricio (2016). "Discrete Choice Models with Random Parameters in R: The Rchoice Package." *Journal of Statistical Software*, 74(10), 1-31. doi:10.18637/jss.v074.i10. (Package version referenced: Rchoice 0.3-1.)
**Type:** R package manual/vignette (JSS article)

## What it estimates
Not multinomial choice — **binary, ordered, and count** outcomes, each with optional random parameters (individual heterogeneity), for cross-sectional and panel data. Models via the `family` argument (Table 1, p. 7):
- **Poisson** (`family = poisson`) — count.
- **Binary probit / binary logit** (`family = binomial("probit"/"logit")`).
- **Ordered probit / ordered logit** (`family = ordinal("probit"/"logit")`, thresholds kappa estimated).
Extensions on any of these:
- Random parameters beta_i ~ g(beta|theta), independent or **correlated** (`correlation = TRUE`, Cholesky L reported; Sigma = LL').
- **Observed heterogeneity in the means** (hierarchical model): beta_i = beta + PI*s_i + L*omega_i, via 2nd formula part + `mvar` list.
- **Panel / random effects**: `panel = TRUE` + `index = "id"`; classical RE model = random constant only (`ranp = c(constant = "n")`).
- Complements glm/MASS::polr/micEcon::probit (fixed-parameter versions) and mlogit/gmnl (multinomial counterparts). No latent class (planned future work); no marginal effects yet.

## Estimation approach
- Fixed-parameter models: **MLE** (Newton-Raphson etc.).
- Random-parameter models: **simulated maximum likelihood (SML)** — Monte Carlo integration of the panel/individual joint density (eqs. 4-6), R draws per individual.
- Uses **maxLik**; default optimizer **BFGS** (author reports it converges most reliably); `method = "nr"` or `"bhhh"` available; analytical gradients by default (`gradient = FALSE` switches to numerical); NR uses numerical Hessian (slow with random parameters). BHHH fast but fragile when variable scales differ — rescale variables.
- Draws: `R = 40` default (paper recommends ~500+ in real work); **Halton draws default** (`haltons = NA`, first K primes starting at 3, first 100 elements dropped); `haltons = NULL` for pseudo-random (`seed = 10` default); custom primes/burn-in via `haltons = list("prime" = c(...), "drop" = c(...))`.
- Random-parameter distributions (`ranp`, Sec. 4 — same shorthand as mlogit/gmnl): "n" normal, "ln" log-normal, "cn" truncated-at-zero normal, "u" uniform, "t" triangular, "sb" Johnson S_b; explicit transformation formulas for constructing beta_kir from primitive uniform/normal draws (pp. 10-11) — directly reusable pseudo-code for hand-coding.
- Sec. 6 computational issues: seed dependence, draw counts, starting values (`init.ran`, `start`), optimizer choice, variable scaling.

## Data format expected
- **Ordinary one-row-per-observation data.frame** (no alternatives, so no wide/long choice reshaping and no dfidx/mlogit.data needed). Dependent variable: 0/1 (binary), ordered categorical (ordered), or count (Poisson).
- **Two-part formula**: `y ~ x1 + x2 + ... | s1 + s2` — part 1 = variables with fixed and random coefficients; part 2 = individual-level variables entering the **means of the random parameters**, mapped by `mvar = list(phd = c("fem"), ment = c("fem","phd"))`.
- Panel data: long format with an individual identifier; `panel = TRUE`, `index = "id"` (string naming the id column).
- Bundled datasets: `Articles` (scientist productivity, Poisson), `Workmroz` (labor force, binary), `Health` (self-reported health, ordered), `Unions` (from pglm, panel binary).

## Key functions
- `Rchoice(formula, data, subset, weights, na.action, family, start, ranp, R = 40, haltons = NA, seed = 10, correlation = FALSE, panel = FALSE, index, mvar, print.init, init.ran = 0.1, gradient = TRUE, method, iterlim, ...)`: single fitting function for all models.
- `vcov(x, what = "coefficient"/"ranp", type = "cov"/"cor"/"sd", se = TRUE, ...)`: covariance/correlation/SDs of random parameters with delta-method SEs (msm::deltamethod wrapper).
- `effect.Rchoice(x, par, effect = "ce"/"cv", wrt)`: individual conditional means (posterior expectations) of coefficients ("ce") or **compensating variations** (ratios -beta_im/beta_il, "cv"); returns means and their SDs.
- `plot(x, par, type = "density", ind = TRUE, id = )`: kernel density of conditional means or per-individual ~95% intervals.
- S3 interoperability: `summary`, `update`, `AIC`/`BIC`, sandwich (`vcovHC` robust SEs incl. Stata-matching correction), lmtest (`waldtest`, `lrtest`), car (`linearHypothesis`, `deltaMethod`), memisc (`mtable`).

## Relevance to book chapters
- **Binary logit/probit chapter**: cleanest R validation target for hand-coded binary MLE (probit vs logit via one `family` switch); the latent-process formulation (eqs. 1-2, p. 4) matches the standard y* = x'beta + eps derivation the book will teach.
- **Ordered models** (if covered): ready-made ordered probit/logit with estimated thresholds.
- **Simulated ML mechanics**: Secs. 2.3 and 4 are arguably the best compact tutorial in these four papers on SML — simulated probability (eq. 6), asymptotics (R rising faster than sqrt(N)), Halton vs pseudo-random draws (Fig. 1), and explicit draw-transformation formulas for six mixing distributions (pp. 10-11). Directly transferable to hand-coding mixed logit even though Rchoice itself is not multinomial.
- **Random effects / panel chapter**: shows RE-as-random-constant equivalence and SML alternative to Gauss-Hermite quadrature (pglm).
- **Individual-level (posterior) estimates**: Sec. 5.5 gives the frequentist conditional-mean estimator (weights proportional to simulated likelihood per draw) — the same formula the book can contrast with HB posterior means; also compensating variation as ratio of a random and fixed coefficient.
- Ties the ecosystem together: same author as gmnl, same `ranp`/`mvar`/`haltons`/`correlation` argument conventions as mlogit/gmnl — worth one sentence in the book noting the shared interface.

## Page pointers
- p. 1-3: abstract, motivation for random parameters in binary/ordered/count models, related packages (glm, polr, pglm, lme4, mlogit, RSGHB, gmnl).
- p. 4-5: latent-process setup, PDFs for binary/ordered/Poisson (eq. 2); correlated parameters and hierarchical means beta_i = beta + PI*s_i + L*omega_i (eq. 3).
- p. 5-6: SML derivation (eqs. 4-6), consistency conditions, maxLik/BFGS/analytical gradients.
- p. 7: `Rchoice()` full argument list and Table 1 (family codes).
- p. 8-11: drawing from densities — Halton sequences, six distribution transformations, `haltons` argument.
- p. 11-16: fixed-parameter examples (Poisson/Articles, binary probit/Workmroz, ordered logit/Health); sandwich/car/lmtest interop.
- p. 16-19: random-parameter Poisson (`ranp`), distribution choice via `update`, mtable comparison; waldtest/lrtest of sd's.
- p. 19-21: correlated random parameters, Cholesky output, `vcov(what = "ranp", type = "cov"/"cor"/"sd", se = TRUE)`.
- p. 21-23: panel/RE models (`panel`, `index`; Unions binary probit with random constant + triangular lwage; ordered probit RE).
- p. 23-25: observed heterogeneity in means (2nd formula part + `mvar`), hierarchical Poisson example.
- p. 25-27: conditional means of individual parameters (Sec. 5.5), plot/effect.Rchoice, compensating variation.
- p. 27-28: computational issues (seed, R, starting values, optimizer choice, scaling); conclusions.
