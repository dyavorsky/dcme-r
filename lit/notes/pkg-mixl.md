# Package: mixl

**Full citation / authors:** Molloy, Joseph, Felix Becker, Basil Schmid, and Kay W. Axhausen (2021). "mixl: An open-source R package for estimating complex choice models on large datasets." *Journal of Choice Modelling*, 39, 100284. doi:10.1016/j.jocm.2021.100284. (IVT, ETH Zurich; code at github.com/joemolloy/fast-mixed-mnl.)
**Type:** R package paper (Journal of Choice Modelling article; user guide ships with the package)

## What it estimates
- **MNL** with arbitrary user-written utility functions.
- **Mixed MNL (MMNL)**: random coefficients with any distribution the user can write as a transformation of draws (normal by default; any draw matrix — Sobol, MLHS, etc. — can be supplied). Panel/repeated-choice structure built in. Inter-individual heterogeneity only (deliberately no intra-respondent mixing).
- **Hybrid choice models (HCM)** / integrated choice and latent variable (ICLV) models: latent variables with continuous (linear-regression) measurement equations, structural equations with covariates, latent variable entering utilities (Sec. 5.1); measurement indicators declared via `P_indic_` variables.
- Design scope is deliberately narrow: MNL, MMNL, HCM with a **logit kernel only** (no probit kernel, no nested logit, no latent class). Positioned against Apollo/Biogeme for speed and memory on very large datasets.

## Estimation approach
- **MLE / maximum simulated likelihood.** Wraps `maxLik` (Henningsen & Toomet 2011); default optimizer **BFGS** (per Train's recommendation); all maxLik options pass through (optimizer choice, Hessian, iteration limits, fixing parameters). Robust (sandwich) SEs via the sandwich package.
- Numerical gradients (unlike gmnl/Apollo/Biogeme's analytical ones) — the speed comes from architecture instead:
  - A **pre-compiler** (`specify_model`) converts a plain-text utility specification into a C++ log-likelihood, compiled once per specification (Rcpp); validates variables against the dataset and auto-detects random/hybrid components.
  - **OpenMP data-parallelism** over observations: near-linear speedups to 24 cores (19x with 10k draws); log-likelihood keeps a running N x R logsum instead of an N x T x R array, so memory stays flat in draws (contrast: Apollo replicating draws per choice task hit ~900 GB where mixl used ~25 GB).
- Draws: `nDraws` in `estimate()` generates Halton draws by default; alternatively pass any user-supplied draw matrix (Sobol, MLHS, ...).
- Benchmarks (Secs. 6-7): with many cores, mixl ~= pandasBiogeme and up to ~3.5x faster than Apollo 0.2.0; gmnl did not finish a 16,000-respondent / 1000-draw problem in 72 hours. Scales to 128,000 choice observations, 10,000 draws.

## Data format expected
- A plain **long-ish data.frame with one row per choice observation** (choice task), not per alternative — alternative attributes sit in columns referenced by `$varname` in the utility script (e.g., `$price_PT`, `$time_Car`). Effectively "wide on alternatives, long on choice tasks."
- Required columns: `ID` (decision maker, values continuous from 1) and `CHOICE` (chosen alternative as integer matching the `U_x` numbering).
- **Availabilities**: a separate n x a matrix (rows = observations, columns = utility functions), 1 = available; `mixl::generate_default_availabilities(data, n_alts)` builds the all-available default.
- Hybrid choice additionally needs a `count` column (number of observations per individual).
- No wide/long reshaping helper — mixl consumes mlogit's example datasets (Electricity, Travel) directly after minor recoding of ID/CHOICE.
- Utility-specification syntax (its distinctive feature): `$var` = data column, `@par` = parameter to estimate, `draw_k` = the k-th random draw, statements end with `;`, utilities named `U_1 ... U_J` (or `U_pt` etc.), intermediate variables allowed, `_RND` suffix marks random coefficients whose individual posteriors should be computed, `P_indic_` prefix declares hybrid-choice measurement indicators.

## Key functions
- `specify_model(utility_script, data)`: pre-compiles the text specification to a C++ log-likelihood; validates the spec against the data; detects mixed/hybrid components.
- `estimate(model_spec, start_values, data, availabilities, nDraws = , ...)`: runs MSLE; start values as a named numeric vector (`stats::setNames`); passes maxLik controls through.
- `generate_default_availabilities(data, n_alternatives)`: all-ones availability matrix.
- `summary(model)`: convergence diagnostics, LL(null/init/final), rho-2, AIC/AICc/BIC, estimates with classical and robust SEs, t-ratios vs 0 and vs 1.
- `posteriors(model)`: individual-level posterior means of `_RND` random parameters.
- `probabilities(model)`: per-observation/alternative choice probabilities — for elasticities and scenario/market-share simulation on modified data.
- `summary_tex(model)`: LaTeX output (texreg-based).

## Relevance to book chapters
- **Mixed logit chapter**: an alternative validation target for hand-coded MSLE, and the best reference on *computational architecture* — the running-logsum trick (sum log-probabilities per individual inside the draw loop, N x R storage) is exactly the implementation insight a hand-coding book should teach; Sec. 2-3 give the cleanest published derivation of the simulated panel log-likelihood (eqs. 1-6) with the 2k+1 numerical-gradient cost accounting.
- **Performance/Rcpp discussion**: if the book has a section on speeding up hand-coded R estimators (vectorization vs. Rcpp vs. parallelism), Secs. 2.3-3 and 6-7 are the citable evidence, including the memory-vs-vectorization tradeoff that bites Apollo.
- **Hybrid choice**: only if the book touches ICLV models; Sec. 5.1 shows the likelihood construction (product of choice probability and indicator densities).
- Table 1 (p. 3): software comparison grid (Apollo, gmnl, RSGHB, mlogit, mnlogit, Biogeme, ALOGIT, NLOGIT, Stata, Gauss, MATLAB) by open-source/R/mixed/HCM/large-problem support — useful in the software-overview section.
- Uses mlogit's Electricity and Travel datasets, so results can be triangulated across mlogit/gmnl/mixl in the book's validation exercises.
- Caveat for the book: numerical (not analytical) gradients and logit kernel only; not a source for nested logit, probit, or latent-class validation.

## Page pointers
- p. 1-2: abstract, motivation, MNL/MMNL likelihood setup (eqs. 1-6).
- p. 3: MLE/MSLE background, BFGS vs NR, numerical vs analytical gradients; Table 1 software comparison.
- p. 4: software architecture — running logsum, memory design, pre-compilation to C++, OpenMP.
- p. 5-6: utility-script syntax rules; Listing 1-2 (MNL on Electricity); estimate/maxLik/sandwich details.
- p. 7-8: output format; mixed MNL specification (Listings 3-4), Halton draws, texreg table.
- p. 8-10: hybrid choice model (eqs. 15-21, Listings 5-6); limitations (no intra-respondent heterogeneity, logit kernel only).
- p. 11: post-processing — posteriors, probabilities, summary_tex; multicore scaling.
- p. 12-15: benchmarks vs Apollo/Biogeme/gmnl (Tables 3-7, Figs. 1-4), memory comparison, conclusions.
