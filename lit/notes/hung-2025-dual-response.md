# Hung, Liu, Brazell & Allenby (2025) — Dual Response in Conjoint Analysis

**Full citation:** Hung, C.-Y., Liu, Y. M., Brazell, J. D., & Allenby, G. M. (2025). "Dual response in conjoint analysis." *Marketing Letters* (published online 7 August 2025). DOI: 10.1007/s11002-025-09787-1.
**Type:** Journal article (model development + empirical HB application + design-efficiency and pricing analysis)
**Length:** 17 pages

## One-paragraph summary

Modernizes dual-response conjoint by resolving how the two responses should be modeled jointly. Prior practice either collapses dual responses into a single response (discarding forced-choice information whenever "no" is chosen) or treats the two responses as independent with fresh error draws (Diener et al. 2006, Sawtooth). The authors' **Unified Model** instead assumes the respondent retains the *same* private information (error realizations) across both responses, since the buy/no-buy question immediately follows the forced choice. Under that assumption the joint probabilities have closed logit forms: Pr(j, purchase) = e^{Vj}/(1+Σe^{Vk}) and Pr(j, no-choice) = [e^{Vj}/Σe^{Vk}]·[1/(1+Σe^{Vk})] — algebraically identical to Diener et al.'s DR-AnyMax likelihood but derived from shared errors rather than an "any-max" second question. They further add a **budget constraint** M active only in the second (purchase) response: respondents ignore affordability when stating preference but enforce it when deciding to buy. Using an HB analysis of a TV conjoint (310 respondents, 15 tasks, 6 brands), the Unified Model with a budget constraint on the second response fits best; part-worths agree with the standard model, but the dual-response format delivers ≈30% more Fisher information, and Nash equilibrium pricing shows the standard (no-budget) model wildly overstates optimal prices (e.g., Samsung +85%, LG +77%).

## Key contributions relevant to the book

- Gives dual-response conjoint an explicit random-utility derivation, with a clean Venn-diagram proof (Fig. 1) that Pr(j, nc) = Pr(j best inside good) − Pr(j, purchase) — a nice classroom derivation of joint probabilities from a single set of utility draws.
- Clarifies the relationship among the three modeling options: collapsed single response (Standard Model), independent-errors dual response (Eq. 2, = DR-2Max), and shared-errors Unified Model (Eq. 4, = DR-AnyMax likelihood).
- Shows how a **budget constraint enters the likelihood** as an indicator condition on price (Pachali et al. 2023 lineage), and that budget effects are identified from the second response while price-sensitivity is identified from the first — a concrete example of separating preference from affordability.
- Derives the **Fisher information matrix** for both models, showing the dual-response information equals the standard-model information plus a positive-semidefinite term weighted by the no-choice probability — the formal reason dual response is more efficient (≈30% by the D_B criterion; 10 dual-response tasks beat 15 single-response tasks).
- Demonstrates downstream consequences for **counterfactual pricing** (Nash equilibrium), connecting estimation choices to managerial conclusions.

## Models & notation

- Utility: U_j = β'x_j + β_p p_j + ε_j, ε_j ~ EV(0,1); **no-choice utility U_nc = ε_nc** (deterministic part normalized to 0 for identification) (p. 3).
- **Standard Model (Eq. 1, p. 3):** Pr(j) = e^{Vj}/(1+Σ_k e^{Vk}), Pr(nc) = 1/(1+Σ_k e^{Vk}) — the "1+" in the denominator is the outside good.
- **Independent-errors dual response (Eq. 2, p. 4):** stage 1 forced-choice logit over inside goods; stage 2 binary logit Pr(i, second) = e^{Vi}/(1+e^{Vi}) — equivalent to Diener et al.'s DR-2Max.
- **Unified Model (Eqs. 3–4, pp. 4):** same ε draws in both responses. Pr(j, purchase) = Pr(U_j > U_k ∀k, incl. nc) = e^{Vj}/(1+Σe^{Vk}); Pr(j, nc) = e^{Vj}/Σe^{Vk} × 1/(1+Σe^{Vk}). Identical in form to DR-AnyMax (noted explicitly, pp. 4–5); Diener et al. found AnyMax fits dual-response data better, consistent with the shared-error story.
- **Budget constraint (Eq. 5, p. 5):** with budget M and C = {j : p_j ≤ M}: Pr(j, purchase) = e^{Vj}/(1+Σe^{Vk}) if p_j ≤ M, else 0; Pr(j, nc) = [e^{Vj}/Σe^{Vk}]·[1/(1+Σe^{Vk})] if p_j ≤ M, else e^{Vj}/Σe^{Vk} (an above-budget preferred good is *never* purchased). Budget can in principle be imposed on first, second, or both responses; second-only fits best.
- **Sign restriction on price (Eq. 6, p. 6):** β_p = −exp(β*_p), with β*_p estimated unrestricted.
- **Heterogeneity (Eq. 7, p. 6):** φ_h = (β'_h, β*_{ph}, M_h)' ~ Normal(φ̄, Σ_φ) — the budget M_h is a respondent-level random effect alongside part-worths.

## Estimation details

- Data: large-screen TV conjoint (Liu et al. 2025), MTurk panel, 6 brands × 6 attributes + 5 price levels (Table 1, p. 6); 15 dual-response tasks (choose preferred of 6, then buy/no-buy); 318 respondents, 8 who never chose "buy" dropped (they identify neither part-worths nor price sensitivity, and retaining them inflates equilibrium prices), n = 310 (p. 7).
- Single-response comparison dataset built by deleting inside-good information whenever "No" was chosen in the second response (p. 7).
- All models estimated as **hierarchical Bayes** with diffuse proper priors; MCMC 400,000 iterations, 200,000 burn-in, thin 10; price scaled in $100s (p. 7).
- Fit via **log marginal density (Newton–Raftery)**: single-response data — standard model −4524 vs −4418 with budget (Table 2, p. 7); dual-response data — unified −5961, budget on both −5939, **budget on second only −5735** (Table 3, p. 8). (LMDs across data formats are not comparable; hence the Fisher-information comparison.)
- Part-worth estimates (Table 4, p. 8): standard and unified models agree within 2 posterior sds absent budget constraints; adding a budget to the standard model *drops* the price coefficient (the no-budget model overstates price sensitivity to mimic non-purchase of expensive items), while the unified model's price coefficient is stable because price sensitivity is identified from the first response (pp. 8–9).
- **Fisher information (Sec. 5.1 + Appendix A, pp. 9–10, 13–15):** I(X,β) = Σ_t [X'_t diag(P_t)X_t − X'_t P_t P'_t X_t] (Huber–Zwerina form for the standard model, outside good included); unified model adds Σ_t P_{t,nc} [X'_t diag(P*_t)X_t − X'_t P*_t P*'_t X_t], where P*_t are forced-choice (inside-good-only) probabilities. Unified log-likelihood per task: log L̃_t = Σ_j y_tj log(P_tj) − y_t,nc log(W_t), W_t = Σ_k e^{β'x_tk} (p. 15). Efficiency compared via Bayesian D-criterion (D_B) integrated over posterior draws: ~30% average gain; 10 tasks (unified) > 15 tasks (standard) (pp. 10–11).
- **Nash pricing (Sec. 5.2 + Appendix B, pp. 11–12, 16):** profit π(p_j|p_−j) = MS·E[Pr(j|p,A)](p_j − c_j); expected shares by Monte Carlo over posterior draws, with the budget model adding indicator 1(p_j ≤ M_h^{(d)}). Standard-model equilibrium prices ($2,035–$4,271) vs unified-with-budget ($1,597–$2,199); the standard model lets share decay too slowly in price, so markups explode (p. 12).

## Relevance to book chapters

- **Choice framework:** exemplary treatment of how the outside option's utility is normalized (U_nc = ε_nc) and how behavioral assumptions (shared vs independent errors; budget screening) map to different probability models.
- **Data organization:** defines dual-response data vs the "collapsed" single-response construction; useful when teaching how survey formats translate into estimation datasets.
- **Likelihood construction:** Eqs. 1–5 are a compact progression from standard MNL with outside good to joint dual-response likelihoods to constrained (budget) likelihoods; Appendix A gives full score/Hessian/Fisher-information derivations, ideal for a likelihood-theory chapter.
- **MNL:** the "1 + Σ exp(V)" denominator convention for the outside good.
- **HB-MNL:** normal random effects over part-worths, transformed price coefficient, and budget; MCMC settings and Newton–Raftery LMD model comparison — all directly reproducible in R (bayesm-style).
- **Conjoint practice:** design-efficiency argument for dual response (fewer tasks for equal precision) and the caution that ignoring budgets distorts price counterfactuals/equilibrium pricing.

## Page pointers

- Motivation, prior approaches to dual-response data: pp. 1–2
- Standard model, no-choice normalization (Eq. 1): p. 3
- Independent-errors model (Eq. 2) and Unified Model derivation (Eqs. 3–4, Fig. 1): pp. 3–5
- Equivalence to DR-2Max / DR-AnyMax: pp. 4–5
- Budget constraint likelihood (Eq. 5), price transform (Eq. 6), heterogeneity (Eq. 7): pp. 5–6
- TV data and design (Table 1): pp. 6–7
- HB setup, LMD fit (Tables 2–3): pp. 7–8
- Parameter estimates and interpretation (Table 4): pp. 8–9
- Fisher information & D_B efficiency comparison: pp. 9–11 (derivations pp. 13–15)
- Nash equilibrium pricing: pp. 11–12 (share approximation p. 16)
