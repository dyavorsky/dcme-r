# Allenby & Rossi (2006) — Hierarchical Bayes Model (A Practitioner's Guide)

**Full citation:** Allenby, G. M., & Rossi, P. E. (2006). "Hierarchical Bayes Model." Chapter 20 in R. Grover & M. Vriens (Eds.), *The Handbook of Marketing Research: Uses, Misuses, and Future Advances* (pp. 418–440). Thousand Oaks, CA: Sage.

**Type:** Non-technical handbook chapter / practitioner tutorial
**Length:** 23 pages (book pp. 418–440; PDF pp. 1–23), of which ~9 pages are an annotated bibliography

## One-paragraph summary

A gentle, practitioner-oriented introduction to hierarchical Bayes (HB) models in marketing. The chapter motivates HB by the fundamental data problem of marketing: individual-level data are scarce (15–20 conjoint responses, <20 purchases per household), discrete, and noncontinuous, yet analysts want respondent-level parameters. It builds intuition from a censored-regression example, explains Bayes theorem via a diagnostic-testing example (posterior odds = likelihood ratio × prior odds), sketches how MCMC replaces analytic posterior derivation with iterative conditional draws, and then walks through a full HB multinomial logit conjoint case study (946 bank credit-card customers, 14,799 paired comparisons) showing convergence assessment, posterior means of hyperparameters, the covariance matrix of heterogeneity, individual-level part-worth distributions, and a "focusing on extremes" targeting analysis. Closes with challenges of using HB in practice (software, convergence mindset, distributions rather than point estimates) and a long annotated bibliography of Bayesian applications in marketing.

## Key contributions relevant to the book

- The clearest low-math statement of *why* HB: pooling via a random-effects distribution solves the limited-individual-data problem while retaining respondent-level inference (pp. 418–420).
- Conditional independence as the organizing principle of hierarchical models: the latent variable z_t is sufficient for the parameters; all information flows through it (p. 420) — this is exactly the logic that makes Gibbs steps simple.
- Plain-English description of MCMC as "draw each block given the others, repeat," with two worked Markov-chain sketches (p. 423).
- A complete applied HB-MNL conjoint example with real output (trace plots, posterior means of Γ and V_β, individual vs. aggregate heterogeneity densities) — an excellent template for what students' R output should look like.
- Frank discussion of practitioner pain points: convergence vs. "closed-form" mindset, burn-in, working with draws instead of point estimates, and available software (WinBUGS, Sawtooth, and the R code accompanying Rossi, Allenby & McCulloch 2006 — i.e., `bayesm`) (pp. 431–432).
- Annotated bibliography (pp. 432–440) is a ready-made further-reading list for the book.

## Models & notation

- Motivating censored/latent-variable model: y_t = 1 if z_t > 0, 0 otherwise; z_t = β0 + β1·price_t + ε_t, ε ~ N(0, σ²) (Eqs. 2–4, pp. 419–420). Introduces data augmentation intuition without naming it.
- Bayes theorem: posterior ∝ likelihood × prior (Eqs. 5–8, pp. 421–422); normal prior on regression coefficient (Eq. 10) times normal likelihood (Eq. 11) gives posterior (Eq. 12).
- HB random-effects logit (the case-study model, p. 424):
  - Likelihood: Pr(i)_h = exp(x_i'β_h) / Σ_j exp(x_j'β_h) (Eq. 13) — MNL per respondent h.
  - Heterogeneity: β_h = Γ z_h + ξ_h, ξ_h ~ MVN(0, V_β) (Eq. 14) — mean of the random-effects distribution is a regression on respondent covariates z_h (age, income, gender).
  - Hierarchical form (Eqs. 15–18): y | x, β; β | z, Γ, V_β; Γ | a, A; V_β | w, W — the last two are priors on hyperparameters with analyst-supplied hyperprior constants (a, A) and (w, W). (Specific conjugate families — normal on Γ, inverted Wishart on V_β — are implied but not spelled out.)

## Estimation details

- Generic MCMC recipe for regression (p. 423): (1) draw β | data, σ²; (2) draw σ² | data, β; repeat. For the latent-variable model: (1) draw z_t | data, params (data augmentation step); (2) draw β0 | z; (3) draw β1 | z; ...; repeat.
- HB-MNL Gibbs structure (p. 424): (1) draw β_h one respondent at a time given {y, x} and hyperparameters (in practice an M-H step, since the MNL likelihood is nonconjugate — the chapter does not belabor this); (2) draw Γ given {β_h} and V_β; (3) draw V_β given {β_h} and Γ; repeat. Key point: by conditional independence, steps 2–3 depend on the data only through {β_h}, so they are standard multivariate-regression conditionals (p. 424).
- Scale: models with thousands of parameters (hundreds of respondents × part-worth vectors of dimension in the tens) are routine (p. 425).
- Convergence/diagnostics (pp. 426, 431): chain run 20,000 iterations, every 20th draw plotted; convergence judged by trace plots leveling off ("same mean value and variability over iterations"), here after ~6,000 iterations; "burn-in" of several thousand iterations; posterior means/SDs computed as sample averages over draws 10,000–20,000 (p. 428).
- Using the draws (pp. 428–431): individual-level part-worths {β_h} are imprecisely estimated — use the full set of draws, not point estimates, for market simulation; distributions of net utility (sums of part-worth draws) across respondents identify high-preference "extreme" targets; comparing tail mass (4.5% vs 7.5% above a threshold) rather than means changes the managerial conclusion.
- Practitioner cautions (pp. 431–432): no off-the-shelf software for complex HB beyond WinBUGS/Sawtooth at the time; HB doesn't "converge" to a point like MLE — draws keep varying after burn-in; each respondent gets a distribution, not a number.

## Relevance to book chapters

- **Bayes-MCMC intro:** the diagnostic-test Bayes-theorem example, posterior ∝ likelihood × prior derivation, and the "draw each block conditionally" MCMC description are ideal first-lecture material.
- **HB-MNL:** Eqs. 13–18 + the 3-step Gibbs sketch is precisely the model estimated by `bayesm::rhierMnlRwMixture` / the book's HB-MNL chapter; the credit-card case study is a citable applied example with covariates in the upper-level mean (Γ z_h).
- **Mixed logit:** the random-coefficients logit here *is* Bayesian mixed logit with a normal mixing distribution — useful for connecting HB and mixed-logit terminology.
- **Applications:** targeting on extremes of the heterogeneity distribution; the annotated bibliography maps applications by topic.
- **Diagnostics chapter:** Figure 20.1 trace-plot discussion and the burn-in guidance are quotable for teaching convergence assessment.

## Page pointers

(Page numbers below are the printed book pages 418–440; PDF page = book page − 417.)
- p. 418: motivation — limited individual-level data; history of HB in conjoint
- p. 419: censored demand model (Eqs. 1–2); discreteness of marketing data
- p. 420: hierarchical/latent-variable form (Eqs. 3–4); conditional independence; within-unit vs. cross-sectional heterogeneity
- pp. 421–422: Bayes theorem, diagnostic-test example, posterior odds (Eqs. 5–8); prior × likelihood for regression (Eqs. 9–12)
- p. 423: MCMC recipes (two enumerated Markov chains); "HB revolution" framing
- p. 424: HB-MNL model (Eqs. 13–18); 3-step Gibbs sampler; conditional independence simplification
- p. 425: credit-card conjoint data (Table 20.1: 946 respondents, 14,799 obs, 7 attributes + demographics)
- p. 426: Figure 20.1 trace plots; 20,000 iterations; convergence after ~6,000
- pp. 427–428: posterior mean of Γ (Table 20.2) and V_β (Table 20.3); interpreting covariances of heterogeneity
- pp. 428–430: individual-level posteriors (Figs. 20.2–20.3), overconfidence from point estimates, computing posterior summaries from draws 10k–20k
- pp. 430–431: focusing on extremes, distribution of net preference (Fig. 20.4)
- pp. 431–432: challenges — software (WinBUGS, Sawtooth, R code from Rossi/Allenby/McCulloch 2006), burn-in, draws vs. point estimates
- pp. 432–440: references + annotated bibliography of Bayesian applications in marketing
