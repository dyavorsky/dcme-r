# Hung, Kurz, Bailey, Huber & Allenby (2025) — Re-examining the No-Choice Option in Conjoint Analysis

**Full citation:** Hung, C.-Y., Kurz, P., Bailey, R. A., Huber, J., & Allenby, G. M. (2025). "Re-examining the no-choice option in conjoint analysis." *Journal of Choice Modelling*, 57, 100578. DOI: 10.1016/j.jocm.2025.100578.
**Type:** Journal article (economic model of the outside good + two multi-country/multi-condition conjoint studies + dynamic-updating HB model)
**Length:** 16 pages

## One-paragraph summary

Challenges the standard assumption that the no-choice (outside good) option has *constant* utility across a respondent's choice tasks. Economically, selecting no-choice means preferring to keep one's money, which presumes respondents know the value and prices of goods in the marketplace. Using an MP3-player conjoint fielded in France/Italy/UK in 2008 (a then-new category) the authors show model-free evidence that the proportion choosing the outside good *rises* across the 15 tasks (Fig. 4), and a logistic regression shows no-choice depends on the choice set's inclusive value (coefficient ≈ −1, exactly as the standard logit predicts) *plus* an unexpected positive task-number trend — respondents learn about market prices from the conjoint exercise itself and update the value they place on their money. Split-sample analysis (first 8 vs last 7 tasks) shows brand intercepts shift while other attribute part-worths are stable — implicating the outside good's utility (the reference point) as what is being updated. They propose an HB model in which the outside-good utility is probabilistically updated each task to the log-sum (expected maximum utility) of the previous task's inside goods; it beats both the standard model and a linear-trend alternative in LMD across all datasets. A second study (tooth whitening, a mature US category, three information conditions) shows updating is much weaker in familiar categories and essentially eliminated when respondents are shown market price information up front. Implications: screen for category familiarity, define attributes concretely, and consider providing market price information; price coefficients are robust, but brand part-worths (measured relative to the outside good) are not.

## Key contributions relevant to the book

- Derives the standard conjoint logit **from an economic budget-allotment model**: the outside good is unspent money, and the budget E cancels out of the logit — a clean rationale for the "+1" (zero-utility outside good) in the denominator (Sec. 2, pp. 2–3).
- Shows how to *test* the standard model's implication logit(p_out) = −W (negative inclusive value) using posterior draws — a nice example of model checking with HB output (Eq. 5–6, p. 7; Appendix B, p. 13).
- Introduces a **dynamic outside-good utility** with probabilistic log-sum updating — an example of extending MNL with a latent-state process while keeping conjugate-style HB machinery (Sec. 4.2, p. 9).
- Documents *which* parameters are fragile when the outside good drifts: brand intercepts (levels relative to the outside good) shift; within-attribute contrasts and the price coefficient are stable (Fig. 5, p. 8; Sec. 5.3, p. 11).
- Full MCMC algorithm in the appendix (random-walk MH for individual parameters, Bernoulli latent-state draws for updating indicators), plus the data-generating process — reproducible material for an HB chapter (Appendices C–D, pp. 14–15).

## Models & notation

- **Economic setup (Eq. 1, p. 2):** u(x, z) = Σ_k ψ_k x_k + ψ_z z, where z is money unspent (outside good) and ψ_z the marginal utility of money. Alternative utilities: u(x_j=1, z=E−p_j) = ψ_j + ψ_z(E−p_j) + ε_j; outside good u(x=0, z=E) = ψ_z(E) + ε_z.
- **Choice probability (Eq. 2, p. 3):** derivation from Pr(V_j + ε_j > V_k + ε_k ∀k) via the integral over Φ(·); with EV(0,1) errors, Pr(j) = e^{ψ_j − ψ_z p_j} / (1 + Σ_k e^{ψ_k − ψ_z p_k}) — the budget E cancels, outside good's deterministic utility is 0.
- **Part-worths (Eq. 3, p. 3):** ψ_j = β'a_j with dummy or effects coding; **heterogeneity (Eq. 4, p. 3):** (β_h, ψ_zh)' ~ Normal(β̄, Σ).
- **Diagnostic logit (Eqs. 5–6, p. 7):** logit(p^out_ht) = α_0 + α_1 W_ht + α_2 (task number), with inclusive value W_ht = ln Σ_k exp(β'_h a_hkt − ψ_zh p_kt). Standard model implies α_1 = −1, α_2 = 0. Estimates: α_1 ≈ −1.00 to −1.03 (theory holds), α_2 ≈ +0.11 to +0.13 (learning; Table 4, p. 8).
- **Proposed dynamic model (Sec. 4.2, p. 9):** u_out,t = ψ_out,t + ψ_z(E) + ε_out,t, ψ_out,1 = 0; after each task the respondent observes max{u_t} = ln{Σ_k exp(β'a_kt − ψ_z p_kt)} + ψ_z(E) + ε_max,t and, **with probability exp(ρ)/(1+exp(ρ))**, substitutes ψ_out,t+1 = ln[Σ_k exp(β'a_kt − ψ_z p_kt)] (Eq. 7); otherwise ψ_out,t+1 = ψ_out,t.
- **Linear-trend alternative (Eq. 8, p. 9):** ψ_out,t = e^γ (t−1), slope constrained non-negative.
- **HB heterogeneity (Eqs. 9–10, p. 9):** φ_h = (β'_h, ψ_zh, ρ_h)' ~ Normal(φ̄, Σ_φ) (proposed model); γ_h replaces ρ_h in the linear model.

## Estimation details

- Data: (1) MP3 players, 2008, France n=482 / Italy n=452 / UK n=487, 4 brands, 9 attributes, 15 tasks with outside option in each, D-efficient SAS designs randomized across respondents (Tables 1–2, p. 4). (2) Tooth whitening, 2019 US, n=1,141 split across three information conditions (none / market price ranges / brand–price–effectiveness graphics), 3 brands + no-choice per task, 12 tasks (Table 3, Figs. 1–3, pp. 5–6).
- Estimation via **MCMC / hierarchical Bayes** with diffuse proper priors. Appendix D (pp. 14–15): priors φ_h ~ N(φ̄, Σ_φ), φ̄ ~ N(0, 100I), Σ_φ ~ IW(ν, νI); random-walk Metropolis–Hastings for φ_h with step scale s = 2.93/√(L+1) (Rossi et al. 2024); Bernoulli(p_h = 0.05) proposal updates for latent updating indicators {s_ht}; standard Bayesian-linear-regression MH step for (φ̄, Σ_φ).
- To analyze dual/standard structure: standard model (Eq. 2) applied to all tasks; the preliminary diagnostic (Eq. 5) fitted per Monte Carlo posterior draw and averaged (Appendix B, p. 13; hit probabilities ≈ 0.82–0.85, Table 4).
- **Model fit (LMD, Newton–Raftery; Table 5, p. 10):** proposed updating model best everywhere. MP3: e.g., France −3932 (standard) / −3767 (linear) / −3678 (proposed). Tooth whitening: Condition 1 −1656 / −1584 / −1470; Condition 3 −1973 / −1920 / −1824.
- **Updating parameter ρ** (Tables 6–7, pp. 10–11): posterior means ≈ −4.0 to −4.3 (MP3) vs ≈ −4.9 to −5.1 (tooth whitening). Probability of updating at least once over the survey: 0.195 (France MP3) vs 0.067 (tooth whitening Cond. 1) — learning concentrated in the unfamiliar category.
- Findings: brand part-worths shift with the outside-good reference (Fig. 5's parallel off-45° line for brands; Fig. 6 boxplots of outside-good utility across tasks, p. 12); price coefficient unaffected — respondents use price locally to compare inside goods but not globally for affordability (p. 12). Providing full market information (Condition 3) shrinks/eliminates updating but also shrinks coefficients (scale effect, p. 11).

## Relevance to book chapters

- **Choice framework:** the budget-allotment derivation (Eqs. 1–2) is the cleanest short derivation of "outside good = money unspent, deterministic utility zero, budget cancels" for the book's framework chapter; also connects to omitted-budget-constraint work (Pachali et al.).
- **Data organization:** multi-country, randomized-task-order design; the split-sample (first vs last tasks) trick for detecting parameter drift.
- **Likelihood construction:** shows the probit/logit integral derivation explicitly (p. 3), the inclusive-value/log-sum W as the key statistic linking no-choice probability to inside-good quality, and how a latent updating state enters the likelihood.
- **MNL:** Eq. 2 is the canonical MNL-with-outside-good; the α_1 = −1 test is a teachable implication of the logit functional form.
- **HB-MNL:** complete prior/MCMC specification (Appendix D) including random-walk MH tuning and latent discrete states — good template for extending bayesm-style samplers.
- **Conjoint practice:** concrete design advice — screen for category familiarity, define attributes concretely, use instructional videos, consider showing market prices; expect a rising no-choice share in new categories and don't interpret brand intercepts as stable there (pp. 11–13).

## Page pointers

- Introduction, role of brand/price/no-choice in economic conjoint: pp. 1–2
- Budget-allotment utility model and logit derivation (Eqs. 1–4): pp. 2–3
- MP3 study design (Tables 1–2): p. 4; tooth-whitening study design (Table 3, Figs. 1–3): pp. 5–6
- Model-free rising no-choice share (Fig. 4) and diagnostic logit (Eqs. 5–6, Table 4): pp. 7–8
- Split-sample part-worth comparison (Fig. 5): p. 8
- Proposed probabilistic updating model (Eqs. 7–10): p. 9
- Model fit (Table 5) and parameter estimates (Tables 6–7): pp. 10–11
- Outside-good utility trajectories (Fig. 6), discussion, design implications: pp. 11–13
- Screening questions (Appendix A), diagnostic estimation (Appendix B), generating process (Appendix C), MCMC algorithm (Appendix D): pp. 13–15
