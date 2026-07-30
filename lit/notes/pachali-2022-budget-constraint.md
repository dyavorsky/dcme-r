# Pachali, Kurz & Otter (2022) — Omitted Budget Constraint Bias and Implications for Competitive Pricing

**Full citation:** Pachali, M.J., Kurz, P., & Otter, T. (2022/2023). Omitted Budget Constraint Bias and Implications for Competitive Pricing. *Journal of Marketing Research* (online first; © 2023), 1–19. DOI 10.1177/00222437221145283
**Type:** Journal article (methodology: Bayesian inference of latent budget constraints in CBC + simulation + industry-grade empirical application)
**Length:** 19 pages

## One-paragraph summary

Standard choice-based conjoint (CBC) models use quasi-linear utility (linear price term), implicitly assuming every respondent can afford every price shown — an assumption strongly at odds with economic theory for high-ticket durables (laptops, smartphones, cars). The authors build a discrete-choice model in which each respondent has a latent budget τ_i that screens out alternatives priced above it; within the feasible set, utility responds to log(τ_i − p) (a BLP-style logarithmic indirect utility that keeps simulated demand continuous in price, as required for computing Nash equilibria). Budgets are inferred by combining three information sources: choice data, respondents' *stated* budgets treated as noisy indicators (b_i ~ N(τ_i, σ²_error) in the individual likelihood), and financial demographics (disposable income, liquid funds, payment method) entering as covariates in the hierarchical prior — the "causal parents" of budgets per household finance theory. A sign-constrained mixture-of-normals hierarchical prior (via the marginal-conditional decomposition of Pachali, Kurz & Otter 2020) and a Metropolis-within-Gibbs MCMC deliver posterior budgets. In simulations and in a 1,000-respondent industry CBC on premium laptops (prices up to 4,000 EUR), the budget model dominates: the standard linear-price model overstates demand at high prices, overstates equilibrium prices of premium brands (Dell +20.65%, Apple +24.82%, even after censoring information-poor respondents), while the "flexible" dummy-coded price model performs worst (RMSE worst; implied demand curves flat at high prices; profit losses up to ~38–200% in cost scenarios) because K−1 price dummies cannot approximate heterogeneous budget cutoffs in finite, shallow panel data. Accounting for budgets cut aggregate-demand RMSE by ~65% relative to the best benchmark.

## Key contributions relevant to the book

- Identifies "omitted budget constraint bias": ignoring budgets biases estimated price response, aggregate demand at high prices, counterfactual equilibrium prices, and profits (pp. 1–2, 6–9).
- Theoretically motivated utility with a hard budget screen and log-price response inside the budget — a concrete example of moving beyond the linear-in-price MNL while retaining tractability (Eq. 2, p. 5).
- Shows why the dummy-coded (nonlinear, "nonparametric") price specification fails in practice: each price level gets its own parameter; low-choice-probability high prices sit on the flat part of the sigmoid where the data are barely informative, so finite data cannot pin the dummies down; the implied indirect utility is discontinuous, breaking existence of pure-strategy Nash equilibria (needs smoothing splines to even compute equilibria) (pp. 3, 7–8, 16, 18).
- Demonstrates budgets are theoretically identified from choice data alone (violation of Slutsky symmetry of the quasi-linear model; Web Appendix C) but that stated budgets + financial demographics greatly discipline the tails of the inferred budget distribution (pp. 2, 6, 13).
- Measurement-error treatment of stated budgets: respondents underreport ("expenditure goal" vs. "cap"; 54.43% chose prices above stated budget; stated budget on average 10.4% below max price chosen) — so stated budgets enter as fallible indicators, not truth (pp. 4, 9).
- Design implication: price ranges must extend well above typical budgets (up to 4,000 EUR for laptops) to identify the budget distribution's upper tail, and prices should be positively correlated with attribute quality (non-orthogonal design) to preserve statistical efficiency (p. 2, fn. 3).
- Practical relevance of alternatives: incentive alignment is prohibitively expensive for high-ticket categories and distorts via income effects (96% of 613 surveyed industry studies not incentive-aligned); sample censoring (Allenby et al. 2014a) helps little here (p. 3, Table 8, Table 10).
- Empirically validates the budget interpretation: inferred budgets increase with disposable income and liquid funds and are independent of them for the price coefficient α; in the standard model, the price coefficient soaks up income effects instead (Table 7, pp. 13–15).

## Models & notation

- Individual likelihood (Eq. 1, p. 4): y_i ~ MNL(τ_i, α_i, β_i) × p(b_i | τ_i, σ²_error), where b_i is the stated budget, b_i ~ N(τ_i, σ²_error) — a normal measurement-error penalty on deviations between stated and latent budgets.
- Choice probability (Eq. 2, p. 5): MNL over feasible alternatives,
  Pr(k) ∝ exp(β_i′a_tk + α_i log(τ_i − p_tk)) · 1{τ_i > p_tk},
  with denominator summing over j with 1{τ_i > p_tj}. Logarithmic indirect utility (à la Berry, Levinsohn & Pakes 1995) chosen so simulated demand is continuous in price — necessary for equilibrium computation; choice probabilities smoothly approach zero as p → τ_i.
- Random coefficients (Eq. 3, p. 5): (log(τ_i), log(α_i), β_i′)′ ~ Σ_s η_s N(μ*_s + (Δ*)′Z̄_i, V*_s) — S-component mixture of normals with demeaned financial demographics Z̄_i (disposable income, liquid funds, installment payment) shifting the component means; log transforms impose the economic sign constraints (τ_i > 0, α_i > 0) via the marginal-conditional decomposition of Pachali, Kurz & Otter (2020).
- Benchmark 1 — standard quasi-linear model (Eq. 4, p. 6): Pr_k(β, β_p) = exp(β′a_k − β_p p_k)/Σ_j exp(β′a_j − β_p p_j); equivalent to the budget model when τ_i exceeds all design prices. Also run with sample censoring à la Allenby et al. (2014a).
- Benchmark 2 — dummy-coded price model: K−1 price dummies with sign/order constraints for downward-sloping demand (p. 6, fn. 12; five-component mixture prior in the empirical app, fn. 26).
- Market share / posterior predictive (Eq. 5, p. 7): MS(k|p, A) integrates the budget-screened logit over the posterior of (β, α, τ) and hyper-parameters.
- Nash equilibrium: brand profit π(p_k|p_−k) ∝ MS(k|p, A)(p_k − c_k) (Eq. 6); FOCs (Eq. 7); solved by iterative best response until ||p^r − p^{r−1}|| < .001 (p. 7).

## Estimation details

- MCMC (Algorithm 1, p. 6): (1) Metropolis update of individual (τ_i, α_i, β_i) using likelihood Eq. 1 conditional on stated budget b_i and σ²_error (Rossi, Allenby & McCulloch 2005 style RW step); (2) update upper-level mixture parameters {μ*_s, V*_s, η_s, Δ*} treating individual coefficients as data, per Pachali, Kurz & Otter (2020); (3) conjugate inverse-chi-square update of σ²_error from squared residuals τ_i − b_i.
- Priors: subjective priors on upper-level coefficients as in Pachali, Kurz & Otter (2020), adjusted for the change of variables imposing economic constraints; inverse chi-square prior for σ²_error per Rossi, Allenby & McCulloch (2005) (pp. 5–6).
- Empirical run: R = 2,000,000 iterations, keep every 200th, burn first 5,000 of kept draws, analyze remaining 5,000 (fn. 23, p. 13). Number of mixture components chosen by marginal-likelihood comparison (à la Dubé, Hitsch & Rossi 2010); one component sufficed for budgets in the application (p. 13, Web App. F).
- Model variants: full model (choice + stated budgets + demographics); "inferred budgets" variant omitting b_i, σ²_error (budgets identified from choices + demographics alone) — used for convergent-validity checks (posterior budgets correlate strongly with held-out stated budgets, Web App. H; stated budgets thin the tails, Web App. G).
- Simulation study (pp. 6–9): N=1,000, T=4, two brands + outside good, prices {.5,…,4.5}, 80% budget-constrained; RMSE vs. data-based demand curve: standard 1.51, inferred budgets 1.36, dummy 2.42 (Table 1); standard model overstates Brand A share at p=4.5 (5.05 vs. 3.48 true), dummy worse (8.25) (Table 2); equilibrium prices: dummy model hits the design ceiling 4.50 vs. true 2.99 (Table 3); average profit losses: standard 3.31%, budgets .57%, dummy 37.96% (Table 4); dummy losses explode when marginal cost is high (Figs. 3–4). Differences vs. standard model vanish when <20% of consumers are budget-constrained (dummy model bad even at 10%) (p. 9, Web App. D).
- Empirical application (pp. 9–17): 1,000 respondents (643 after quality screens incl. removing those exceeding stated budget by ≥50%, not reporting income, or always choosing outside good), 15 choice tasks, 3 inside options + outside good, 8 attributes, 7 brands, prices 600–4,000 EUR (Tables 5–6). Only 3.58% ever chose at 4,000 EUR; choice share ~1.7% at 4,000 (Figs. 5–6). Mean stated budget 1,157 EUR (Fig. 7); posterior: ~96.4% of consumers have budgets below 4,000 EUR (Fig. 8, p. 13). Fit: RMSE .83 (budget model) vs. 2.40 standard, 2.58 standard-censored, 3.05 dummy (Table 8, p. 15) — 65.42% RMSE reduction. Market shares at 4,000 EUR: standard model leaves ~10% in-market vs. 3.49% for budget model (Table 10, p. 16). Equilibrium prices: Dell 2,230 (standard) vs. 1,822 (budgets) = +20.65% overstatement (Apple +24.82% vs. censored standard); dummy model wildly overstates premium brands (Lenovo 4,000) (Table 11, p. 17).
- Robustness: shift-and-scale measurement error model b_i ~ N(γ + ψτ_i, σ²_error) does not improve fit (pp. 17–18, Web App. I).

## Relevance to book chapters

- **Choice framework / utility specification:** the paper's contrast of quasi-linear utility vs. budget-constrained (feasible-set) utility is the natural "advanced specification" companion to the budget-allotment discussion in Allenby, Kim & Rossi (2015) and Allenby, Hardt & Rossi (2019, p. 156 cites Pachali et al. on price screening). Shows concretely how E/τ enters the likelihood when it does not cancel.
- **Price coefficient treatment:** three-way comparison — linear price, log(τ−p) with screen, dummy-coded price — with theory and evidence on why dummy-coded price fails in hierarchical finite-data settings and breaks equilibrium computation; strong material for the book's "how to specify price" section.
- **WTP-and-post-estimation:** posterior predictive market shares (Eq. 5) and Nash equilibrium pricing (Eqs. 6–7) computed by integrating over hyper-parameter posteriors — same discipline as Allenby et al. (2014); shows counterfactual price/profit consequences of misspecification.
- **HB-MNL:** state-of-the-art hierarchical machinery: sign constraints by log transformation, mixture-of-normals priors with demographic covariates via the marginal-conditional decomposition, augmenting the individual likelihood with auxiliary survey data (stated budgets) plus a conjugate error-variance step, marginal-likelihood model comparison, long thinned MCMC runs.
- **Conjoint practice:** design guidance for high-ticket categories — extend price grids beyond typical budgets, correlate price with quality levels, collect stated budgets (after glossary, before tasks) and financial demographics routinely; data-quality screens; why incentive alignment is impractical here.

## Page pointers

- p. 1: abstract; motivation (Apple v. Samsung; ~20,000 CBC applications/year)
- p. 2: contribution summary; stated budgets as noisy data; design requirements (fn. 3); Dell +20.65% headline
- p. 3: related literature — incentive alignment survey (96% not aligned), sample censoring, flexible price responses, screening rules
- p. 4: budget theory (household finance, two-stage budgeting); Eq. 1 likelihood with measurement error
- p. 5: Eq. 2 budget-screened MNL; Eq. 3 mixture prior with financial demographics; Fig. 1 DAG
- p. 6: Algorithm 1 (MCMC); benchmark models (Eq. 4, dummy-coded); simulation setup
- pp. 7–9: simulation results — fit (Fig. 2, Table 1), shares (Table 2), equilibrium prices (Table 3, Eqs. 5–7), profit losses (Table 4, Figs. 3–4)
- pp. 9–12: laptop study design (Tables 5–6), data quality screens, model-free evidence (Figs. 5–6), stated budgets (Fig. 7)
- pp. 13–15: inferred budget distribution (Fig. 8: 96.4% below 4,000 EUR); demographics–parameter relations (Table 7); fit comparison (Fig. 9, Table 8)
- pp. 16–17: market scenario (Table 9), predictive shares (Table 10), demand curves (Fig. 10), equilibrium prices (Table 11)
- pp. 17–18: measurement-error robustness; discussion and future directions (menu-based choice, aggregate logit)
