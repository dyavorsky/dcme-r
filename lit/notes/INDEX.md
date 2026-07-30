# Literature Index

Master index of the reference notes in this directory. Each note summarizes one PDF in `lit/` and contains page pointers for locating specific material. Notes were generated 2026-07-03; verify quotes and page numbers against the PDFs before citing in the book.

## Companion texts and general references

| Note | Source | What it's for |
|---|---|---|
| [train-2009-dcms.md](train-2009-dcms.md) | Train (2009), *Discrete Choice Methods with Simulation*, 2e | **Primary companion text ("DCMS").** Chapter-by-chapter index with algorithm/pseudo-code page locations. Ch. 8 (numerical maximization), Ch. 9 (drawing from densities), Ch. 12 (HB for mixed logit) are the most load-bearing. PDF page = book page + 11. |
| [hess-daly-2024-handbook.md](hess-daly-2024-handbook.md) | Hess & Daly (2024), *Handbook of Choice Modelling*, 2e | Edited handbook. Ch. 21 (Bunch: frequentist optimization), Ch. 22 (Lenk: HB blueprint), Ch. 14 (latent class vs. mixed logit), Ch. 11 (nonparametric mixing). **Warning:** PDF has chapters 4/5 and 11/12 physically swapped; note gives actual PDF page ranges. |
| [greene-2008-discrete-choice-modeling.md](greene-2008-discrete-choice-modeling.md) | Greene (2008), Handbook chapter, 78 pp. | Best single cross-reference across model classes: binary choice MLE in full detail (gradients, covariance estimators, tests), Albert–Chib Bayesian probit, GHK, ordered, MNL/MNP/nested/mixed (§0.7). |
| [rao-applied-conjoint.md](rao-applied-conjoint.md) | Rao (2014), *Applied Conjoint Analysis* | Experimental design (Ch. 2, 4: fractional factorials, D-efficiency, Bayesian designs), applied MNL and HB-MNL with WinBUGS code (Ch. 4), Gibbs primer for ratings conjoint (Ch. 3 App. 3). PDF page = book page + 16. |

## History and framing

| Note | Source | What it's for |
|---|---|---|
| [mcfadden-2001-economic-choices.md](mcfadden-2001-economic-choices.md) | McFadden (2001), AER Nobel lecture | RUM history, MNL/EV1 foundations, GEV generating functions, MMNL universal approximation. §IV is a compact syllabus on simulation-assisted estimation. |
| [green-2022-thirty-years.md](green-2022-thirty-years.md) | Green, Krieger & Wind (2001), *Interfaces* (filename year is download date) | Founders' retrospective on conjoint: ratings → CBC → HB. Historical framing and motivation; no estimation math. |
| [allenby-2004-hb-revolution.md](allenby-2004-hb-revolution.md) | Allenby et al. (2004), *Marketing Research* | Zero-prerequisite HB intro: frequentist vs. Bayesian, minimal 3-equation hierarchical choice model. First-week reading. |
| [chapman-2013-nine-things.md](chapman-2013-nine-things.md) | Chapman (2013), Sawtooth proceedings | Nine practitioner misunderstandings of conjoint (preference share ≠ market share, part-worths are relative, averages hide the posterior). Interpretation-pitfalls material. |

## Economic foundations and utility specification

| Note | Source | What it's for |
|---|---|---|
| [allenby-2015-economic-models-of-choice.md](allenby-2015-economic-models-of-choice.md) | Allenby, Kim & Rossi (2015), Handbook chapter | Derives MNL from direct utility maximization with budget and outside good; Kuhn–Tucker volumetric models with satiation. Theory backbone for utility specification. |
| [allenby-2019-economic-foundations-conjoint.md](allenby-2019-economic-foundations-conjoint.md) | Allenby, Hardt & Rossi (2019), Handbook chapter | Conjoint as designed demand experiment; WTP/WTB/EPP value measures; list of invalid practices (dummy-coded price, raw part-worth comparison); frozen-pizza validation. |
| [allenby-2014-economic-valuation.md](allenby-2014-economic-valuation.md) | Allenby et al. (2014), QME | Feature valuation = change in Nash-equilibrium profit; true WTP (log-sum) vs. pseudo-WTP (β/β_p, dismissed); rich bayesm HB detail (sign-constrained price coefficient, prior tightening). |
| [pachali-2022-budget-constraint.md](pachali-2022-budget-constraint.md) | Pachali, Kurz & Otter (2022), JMR | Omitted-budget-constraint bias; latent budget screening + log(τ−p) utility; stated budgets as noisy indicators. Model example for a "build your own extension" chapter. |

## Estimation: Bayesian / MCMC

| Note | Source | What it's for |
|---|---|---|
| [allenby-rossi-2006-hb-practitioners-guide.md](allenby-rossi-2006-hb-practitioners-guide.md) | Allenby & Rossi (2006), Handbook chapter | Gentle HB intro with full HB-MNL conjoint case study (trace plots, posterior summaries). Template for presenting HB-MNL output. |
| [mcculloch-rossi-1994-exact-mnp.md](mcculloch-rossi-1994-exact-mnp.md) | McCulloch & Rossi (1994), J. Econometrics | **The Bayesian MNP paper** (behind `bayesm::rmnpGibbs`): 3-block data-augmentation Gibbs (truncated-normal latents / normal β / Wishart Σ⁻¹), identification via post-hoc σ₁₁ normalization, hierarchical extension. |
| [rossi-1996-purchase-history.md](rossi-1996-purchase-history.md) | Rossi, McCulloch & Allenby (1996), Marketing Science | Hierarchical MNP with demographics (β_h = Δz_h + v_h); Appendix A has code-ready Gibbs conditionals; continuous heterogeneity vs. finite mixture comparison (App. B). |
| [train-hb-vs-msl.md](train-hb-vs-msl.md) | Train (2001), working paper (→ DCMS Ch. 12) | HB mixed-logit sampler details (adaptive M-H step, ~0.3 acceptance target); Bernstein–von Mises argument; HB-vs-MSL run-time scoreboard. Greek symbols garbled in PDF; verify equations against DCMS. |

## Estimation: classical / simulation-assisted

| Note | Source | What it's for |
|---|---|---|
| [mcfadden-train-2000-mixed-mnl.md](mcfadden-train-2000-mixed-mnl.md) | McFadden & Train (2000), JAE | Foundational mixed logit: MMNL approximates any RUM (Thm 1); full MSLE/MSM machinery (draw counts, Halton, sandwich covariance); LM specification tests for mixing. |
| [train-2016-flexible-mixing.md](train-2016-flexible-mixing.md) | Train (2016), J. Choice Modelling | Logit-Mixed Logit: flexible mixing distribution on a grid, MSL with precomputed likelihoods; generalizes latent class; WTP-space variant. Extension-chapter material. |

## Conjoint practice, design, and the no-choice option

| Note | Source | What it's for |
|---|---|---|
| [ben-akiva-2019-stated-preference.md](ben-akiva-2019-stated-preference.md) | Ben-Akiva, McFadden & Train (2019), FnT Econometrics, 144 pp. | Economics-first CBC monograph: design checklist, WTP-space RUM, MSL vs. HB Monte Carlo comparison (incl. Stan/NUTS). R code at eml.berkeley.edu/~train/foundations_R.txt. |
| [cbc-handbook-2022.md](cbc-handbook-2022.md) | Eggers et al. (2022), Handbook of Market Research | **Best end-to-end CBC tutorial**: design → data → aggregate MLE (fit stats, effect coding) → importance/WTP → market simulation → latent class/HB, with one dataset and complete mlogit R code. Workflow template. |
| [marshall-bradlow-2002-unified.md](marshall-bradlow-2002-unified.md) | Marshall & Bradlow (2002), JASA | Unified framework: conjoint variants (rating/ranking/choice/constant-sum) differ only in the likelihood layer over shared latent utilities; Gibbs + data augmentation. Bridge into HB architecture. |
| [brazell-2006-no-choice.md](brazell-2006-no-choice.md) | Brazell et al. (2006), Marketing Letters | Foundational dual-response paper: no-choice as 0/1 ASC; RMSE gains; format equivalence tests. |
| [diener-2006-dual-response.md](diener-2006-dual-response.md) | Diener, Orme & Yardley (2006), Sawtooth | Practitioner likelihoods for DR-2Max / DR-AnyMax; stacked-two-task data setup that works with standard MNL/HB code. |
| [hung-2025-dual-response.md](hung-2025-dual-response.md) | Hung et al. (2025), Marketing Letters | Unified dual-response model with shared errors + budget constraint on the buy/no-buy response; Fisher-information gains; equilibrium-price overstatement. |
| [hung-2025-no-choice.md](hung-2025-no-choice.md) | Hung et al. (2025), J. Choice Modelling | Relaxes constant-utility no-choice: outside-good utility updates toward prior task's log-sum; full MCMC in appendix. Extension-chapter material. |

## R packages (validation targets and design references)

| Note | Package | What it's for |
|---|---|---|
| [pkg-mlogit.md](pkg-mlogit.md) | mlogit (Croissant) | Canonical package; source of the standard choice-data format (`dfidx`, wide vs. long). MNL, nested, mixed (MSLE), probit. Primary validation target. |
| [pkg-gmnl.md](pkg-gmnl.md) | gmnl (Sarrias & Daziano) | MIXL, S-MNL, G-MNL, latent class, WTP-space, individual conditional estimates. Frequentist heterogeneity counterpart to HB. |
| [pkg-mixl.md](pkg-mixl.md) | mixl (Molloy et al.) | Speed-focused MSLE architecture (C++ pre-compilation, running logsum). Reference for the code-performance chapter. |
| [pkg-rchoice.md](pkg-rchoice.md) | Rchoice (Sarrias) | Random-parameter binary/ordered models. §2.3 and §4 are the most compact tutorial on SML mechanics and draw-transformation formulas. |

## Quick map: book topic → best sources

- **Choice framework / RUM:** DCMS Ch. 1–2; McFadden (2001); Allenby, Kim & Rossi (2015)
- **Drawing from densities:** DCMS Ch. 9; Rchoice §2.3/§4 (draw transformations)
- **Simulate-and-recover workflow:** DCMS Ch. 1, 10; Chapman (2013) (Rcbc simulation)
- **Choice data organization:** pkg-mlogit (dfidx format); Diener (2006) (stacked dual-response); Eggers et al. (2022)
- **MNL + MLE:** DCMS Ch. 3; Greene (2008); Eggers et al. (2022, worked example)
- **Numerical optimization:** DCMS Ch. 8; Hess & Daly Ch. 21 (Bunch)
- **Bayesian MNL / MCMC intro:** Allenby et al. (2004); Allenby & Rossi (2006); Hess & Daly Ch. 22 (Lenk); Rao Ch. 3 App. 3
- **Nested / GEV:** DCMS Ch. 4; McFadden (2001); Greene (2008) §0.7
- **MNP:** DCMS Ch. 5 (GHK); McCulloch & Rossi (1994); Rossi et al. (1996); Greene (2008)
- **MSL / simulation-assisted estimation:** DCMS Ch. 10; McFadden & Train (2000); pkg-mixl
- **Latent class:** DCMS Ch. 6, 14; Hess & Daly Ch. 14; gmnl
- **Mixed logit / HB-MNL:** DCMS Ch. 6, 12; Train (2001); Ben-Akiva et al. (2019) Ch. 5–7; Allenby & Rossi (2006)
- **HB-MNP:** McCulloch & Rossi (1994); Rossi et al. (1996)
- **Post-estimation (WTP, market simulation):** Allenby et al. (2014, 2019); Eggers et al. (2022); Chapman (2013)
- **No-choice / dual response:** Brazell (2006); Diener (2006); Hung (2025) ×2; Ben-Akiva et al. (2019) §2.1.3
- **Custom extensions:** Pachali (2022); Hung (2025) ×2; Train (2016); Marshall & Bradlow (2002)
- **Experimental design:** Rao Ch. 2, 4; Hess & Daly Ch. 7; Ben-Akiva et al. (2019) Ch. 2
