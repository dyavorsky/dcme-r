# Package: mlogit

**Full citation / authors:** Croissant, Yves (2020). "mlogit: Random Utility Models in R." *Journal of Statistical Software*, 95(11), 1-41. doi:10.18637/jss.v095.i11. (Package version referenced: mlogit 1.1-1.)
**Type:** R package manual/vignette (JSS article — the canonical mlogit paper)

## What it estimates
- **Multinomial logit (MNL)** in the broad sense: handles "multinomial" (choice-situation-specific covariates), "conditional" (alternative-specific covariates), and mixed covariate sets in one unified formula interface. First R package (2008) for random utility models.
- **Heteroscedastic logit** (Bhat 1995): alternative-specific Gumbel scale parameters (`heterosc = TRUE`).
- **Nested logit** (McFadden 1978), via `nests` argument; unique vs. nest-specific inclusive-value elasticities via `un.nest.el`. Also supports two-step estimation (lower model + `logsum` inclusive values + upper model) vs. FIML.
- **Mixed / random-parameters logit (MIXL)** via `rpar`, with panel support, correlated normal parameters, and individual-level (conditional) parameters via `fitted(type = "parameters")`.
- Also fits (per Sec. 6, illustrated in package vignettes, not in the article): rank-ordered logit, overlapping nests, paired combinatorial logit, and **multinomial probit (MNP)** by MSL (GHK).
- Scale heterogeneity across choice situations via the 4th formula part (covariates entering the error variance).

## Estimation approach
- MLE with analytic gradients; Newton-Raphson with analytic Hessian is default for the basic MNL (globally concave; converges in a handful of iterations). `method = "bhhh"` or "bfgs" available (optimization via maxLik-style interface).
- Heteroscedastic logit: one-dimensional integral computed by Gauss-Laguerre quadrature.
- Mixed logit: **maximum simulated likelihood**; `R` draws, `halton` argument (NA = default Halton draws, NULL = pseudo-random). Panel likelihood via `panel = TRUE`.
- Random-parameter distributions in `rpar`: "n" (normal), "ln" (log-normal), "cn" (zero-censored normal), "u" (uniform), "t" (triangular), plus zero-bounded one-parameter variants "zbt" and "zbu" (useful for sign-restricted price coefficients).
- `correlation = TRUE` (or a character vector for a subset) estimates the Cholesky factor of the covariance of normal-related random parameters.
- Testing: Wald (`waldtest`), LR (`lrtest`), and a dedicated Lagrange-multiplier `scoretest`; convenient one-argument forms for heteroscedasticity/nesting/correlation hypotheses.
- Optimization troubleshooting (Sec. 5.3): switch BFGS→BHHH, supply `start`, fix parameters with `constPar`, or change the mixing distribution.

## Data format expected
This is the reference package for choice-data formatting; gmnl and others reuse it.
- Data are indexed by three indexes: alternative (`alt`), choice situation (`chid`), and individual (`id`) — id vs. chid matters only with repeated choices (panel).
- Two shapes: **wide** (one row per choice situation; alternative-specific variables in columns like `price_A`, `price_B`) and **long** (one row per alternative per choice situation).
- Key function: **`dfidx()`** from the dfidx package (successor to the older `mlogit.data()`). Arguments:
  - `shape = "wide"` (mandatory for wide data; default "long"), `choice` (response variable), `varying` (column positions of alternative-specific variables, passed to `stats::reshape`), `sep` (separator in wide names, default "."),
  - `idx` — index specification, e.g. `idx = c("case", "alt")` or nested `idx = list(c("choiceid", "id"))` for panels, or `idx = list("firm", c("region", "country"))` for grouped (nest) structures; `idnames` renames indexes,
  - `alt.levels` (names of alternatives when data are balanced and index columns absent), `opposite` (negate covariates so expected coefficients are positive — handy for sign-restricted random parameters), `subset`, `drop.index`, `pkg = "mlogit"`.
- Returns a 'dfidx' object: long-format data.frame with an `idx` attribute; specific `model.frame`/`model.matrix` methods build the RUM design matrix (J-1 columns for situation-specific vars, 1 column for generic, J columns for alternative-specific coefficients).
- `mlogit()` also accepts a plain data.frame plus dfidx arguments (`idx =`, etc.) directly.

## Key functions
- `mlogit(formula, data, ...)`: main fitting function. Multi-part Formula: `choice ~ alt.specific.generic | situation.specific | alt.specific.altcoef | scedasticity.covariates`. Key args: `reflevel`, `alt.subset`, `heterosc`, `nests` (+ `un.nest.el`), `rpar`, `R`, `halton`, `panel`, `correlation`, `weights`, `method`, `constPar`, `start`, `subset`.
- `dfidx()` / (legacy `mlogit.data()`): reshape/index choice data (see above).
- `fitted(x, type = "outcome"/"probabilities"/"parameters")`: chosen-alternative probabilities, full probability matrix, or individual-level posterior parameters (Train's conditional means).
- `predict(x, newdata)`: probabilities for counterfactual data.
- `effects(x, covariate, type = "aa"/"ar"/"ra"/"rr")`: marginal effects/elasticities.
- `logsum(coef, data, formula, type = "group"/"global", output)`: inclusive values / log-sum for consumer surplus and two-step nested logit.
- `rpar(x, par, norm =)` + `mean`, `med`, `stdev` methods: extract/summarize random-parameter distributions, incl. WTP-space normalization by a price coefficient.
- `vcov(x, what = "rpar", type = "cov"/"cor")` + summary method (delta-method SEs of the covariance/correlation elements).
- `scoretest`, plus mlogit methods for `lrtest`/`waldtest` (lmtest) and compatibility with `linearHypothesis` (car), `texreg`.

## Relevance to book chapters
- **The data chapter**: `dfidx`/`mlogit.data` is the de facto standard for wide-vs-long choice data in R; the alt/chid/id index taxonomy is exactly the notation a hand-coded estimator needs. Also the source of classic teaching datasets used throughout the literature: `Train`, `Electricity`, `ModeCanada`, `NOx`, `RiskyTransport`, `JapaneseFDI`, `TravelMode` (via AER).
- **MNL chapter**: primary validation target for a hand-coded MNL MLE (NR with analytic gradient/Hessian; McFadden R2; IIA discussion; marginal effects, MRS/WTP, log-sum consumer surplus formulas in Sec. 3.4 are all directly reusable).
- **Nested logit chapter**: both two-step (inclusive value) and FIML estimation shown side by side — good pedagogy for validating each stage of hand-coded nested logit.
- **Mixed logit chapter**: validate hand-coded MSLE (Halton draws, correlated normals via Cholesky, panel likelihood, individual-level conditional parameters via `fitted(type="parameters")`).
- **MNP chapter**: mlogit fits MNP by MSL (vignette, not the article) — a frequentist cross-check for a hand-coded/Bayesian MNP.
- The paper's theory sections track Train (2009) closely, so notation aligns with the book's likely main reference.

## Page pointers
- p. 1-2: abstract, model taxonomy, related packages (mnlogit, gmnl, bayesm, MNP, RSGHB).
- p. 3-7: data management — indexes, wide vs long, `dfidx` usage (Train and ModeCanada examples).
- p. 7-10: model description, 4-part formula, model.matrix construction.
- p. 10: testing (waldtest/lrtest/scoretest).
- p. 11-13: RUM theory, MNL derivation, IIA, marginal effects, MRS, log-sum consumer surplus.
- p. 14-18: `mlogit()` application, fitted/predict/effects/logsum, value-of-time computation.
- p. 20-23: heteroscedastic logit (Gauss-Laguerre; Bhat 1995 replication) + tests.
- p. 21-27: nested logit theory, two-step vs FIML, JapaneseFDI example, nest tests.
- p. 28-30: mixed logit derivation, individual parameters, panel data; rpar distributions.
- p. 30-35: Train data mixed logit, correlation/Cholesky, rpar/vcov extraction, WTP via `norm`.
- p. 35-38: RiskyTransport example (VSL), individual parameters, optimization tips.
- p. 38-39: conclusions — rank-ordered logit, overlapping nests, paired combinatorial logit, MNP in vignettes.
