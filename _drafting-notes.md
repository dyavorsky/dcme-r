# Drafting conventions (not committed; underscore prefix keeps Quarto away)

Working notes for drafting the full text. Update the progress log as chapters complete.

## Notation (fixed for the whole book)

- Decision-makers `n = 1, ..., N`; choice situations `t = 1, ..., T`; alternatives `j = 1, ..., J`; simulation draws `r = 1, ..., R`; parameters `k = 1, ..., K`.
- Utility: $U_{ntj} = V_{ntj} + \varepsilon_{ntj}$ with representative utility $V_{ntj} = \x_{ntj}'\bfbeta$.
- Macros from latex-header.tex: `\x`, `\y`, `\bfbeta`, `\bftheta`, `\beps`, `\iid`, `\var`, `\cov`.
- Choice probabilities: $P_{ntj}$ for MNL-family; $p(y|x)$ in the generic ch 1 framework.
- Log-likelihood $\ell(\bfbeta)$; estimates $\hat{\bfbeta}$; standard errors from $-H^{-1}$.
- Heterogeneity: $\bfbeta_n \sim N(\bar{\bfbeta}, \Sigma)$. Hyperpriors: $\bar{\bfbeta} \sim N(\mathbf{a}_0, A_0)$, $\Sigma \sim IW(\nu_0, V_0)$.
- MNP errors: $\beps \sim N(\mathbf{0}, \Omega)$.

## The running example: laptop choice study

Fictional CBC study of laptop purchases. Introduced in ch 1, grown through the book.

- **Brands:** Apple, Dell, Acer (Acer = reference level). OS follows brand: Apple = macOS, Dell/Acer = Windows -> the nests in ch 10.
- **Attributes:** `price` in $1,000s (range 0.8-2.4, continuous); `ram` 8 (ref) / 16 / 32 GB -> dummies `ram16`, `ram32`; `screen` 13" (ref) / 15" -> dummy `screen15`; brand dummies `apple`, `dell`.
- **True parameters (homogeneous-preference chapters):**
  `apple = 1.0, dell = 0.5, ram16 = 0.6, ram32 = 0.9, screen15 = 0.3, price = -1.2`
- **Binary chapters (1-6):** buy/no-buy one configured laptop. `x = (1, price, ram16)`, `beta_true = c(1.0, -1.2, 0.6)`. Worked number in ch 1: price $1,500, 16GB -> V = 1.0 - 1.2(1.5) + 0.6 = -0.2, P(buy) ~= 0.450.
- **MNL data sizes (ch 7+):** N = 500 respondents, T = 8 tasks, J = 3 alternatives.
- **Mixed/HB (ch 13, 17):** beta_n MVN around the values above; sds circa (0.8, 0.5, 0.4, 0.5, 0.3, 0.5); correlations introduced when needed; lognormal price coefficient in ch 17 practical notes.
- Chapter 22: none option added (dual response); budget constraint (Pachali-style, laptops are the natural category); flexible mixing on selected coefficients.

## Code conventions

- snake_case functions; the canonical family: `sim_binary_data()`, `sim_mnl_data()`, `loglik_binary()`, `loglik_mnl()`, `build_choice_data()`.
- Canonical long-format data.frame `laptops`: columns `id, task, alt, choice` then attributes. One row per alternative per task per person.
- Estimation-ready structure (decided in ch 4 after discussing alternatives): stacked X matrix ((N*T*J) x K) + integer group index `task_id` + 0/1 vector `choice`; grouped ops via `rowsum()`. Chosen for reuse: the same structure feeds MLE (ch 8), MSL (ch 12-13), and MCMC (ch 15-17).
- Plots: ggplot2 only; each chapter's setup chunk runs `library(ggplot2); theme_set(theme_minimal())`. Keep every plot a few transparent lines.
- Seeds: `set.seed()` in every stochastic chunk; vary across chapters (use chapter number pattern, e.g. 1010, 1020 for ch 10).
- Validation targets: mlogit (ch 8, 10), gmnl (ch 11, 13), bayesm (ch 17, 19, 20); mixl referenced in ch 9/13 prose.
- Chapter template: latex-header include block; `# Title {#sec-id}`; setup chunk; ends with `## Key Learnings`.
- Cross-reference with `@sec-...`, `@eq-...`, `@fig-...` liberally (callbacks are a book goal).

## Per-chapter render check

`quarto render chapters/XX_name.qmd` renders the single chapter within the book project. Full render at part boundaries.

## Progress log

- ch 01-22 + appendix: fully drafted with executed R code; all render individually to HTML.
- Saved data artifacts flow between chapters: `data/laptop_study.rds` (ch 7), `data/mixed_study.rds` (ch 13), `data/mnp_study.rds` (ch 18), `data/hb_mnl_fit.rds` (ch 17).
- Validations run inside chapters: mlogit (ch 8, 10, 13), EM-vs-BFGS (ch 11), mvtnorm/pmvnorm (ch 19), bayesm rhierMnlRwMixture (ch 17), bayesm rmnpGibbs base=3 (ch 19).
- Known content quirks (deliberate): gmnl LC decayed (documented in ch 11 footnote); IW variance floor shown as pedagogy (ch 17, 20); ch 22 LML fixes non-price coefficients (disclosed shortcut).
- Consistency pass (2026-07-05): 5 parallel reviewers audited all chapters against the notation policy + derivation-completeness standard (~85 findings); all fixes applied. Highlights: `time_ms()` lazy-evaluation bug in ch 9 fixed (substitute/eval); ch 10 IIA-boundary claim corrected (third-NEST alternatives still cancel); alternative-summation index renamed j' (ch 7/8/10); β* adopted for true values from ch 1; representative utility V defined at first use; full derivations added for binary-logit closed form, binary/MNL scores, Gumbel max-stability, cross-elasticity, nested log-prob identity + cross-nest odds, EM Q-function, Jensen bias rate, MSL gradient chain rule, conditional-mean importance-sampling, normal-normal complete-the-square, M-vs-H ratio, detailed balance, HB-MNL block conditionals, GHK factorization, bivariate conditionals, delta method, log-sum CV (Small-Rosen cite); Ω/Ω̃/W mapping made explicit in ch 18/19/20 + appendix glossary rows; ch 12 Halton segment scheme aligned with ch 13; ch 14 conditional mean renamed β̂_n; τ standardized for MCMC step scale; latex-header \rm → \mathrm (fixed PDF build).
- Notation policy that reviewers enforced is recorded in the appendix glossary (@tbl-notation) — keep it authoritative when editing.
- Final render verified 2026-07-06: HTML site clean (0 crossref warnings), PDF builds at 260 pages. PDF-specific gotchas fixed along the way: `\rm` -> `\mathrm` in latex-header.tex; literal Unicode `≈` replaced with `$\approx$`; `\hat\bftheta` must be written `\hat{\bftheta}` (pdflatex rejects unbraced \hat over a \boldsymbol macro; MathJax tolerates it — always brace).
- Remaining: Dan's read-through; NOT committed (per instruction).
