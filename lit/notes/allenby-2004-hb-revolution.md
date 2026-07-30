# Allenby, Bakken & Rossi (2004) — The HB Revolution

**Full citation:** Allenby, G. M., Bakken, D. G., & Rossi, P. E. (2004). "The HB Revolution: How Bayesian Methods Have Changed the Face of Marketing Research." *Marketing Research*, 16(2, Summer), 20–25.

**Type:** Non-technical trade-magazine article (AMA's *Marketing Research*); perspective piece for practitioners
**Length:** 6 pages (magazine pp. 20–25)

## One-paragraph summary

A short, entirely non-technical manifesto for the "HB revolution" in marketing research, written for practitioners. It contrasts classical (frequentist) statistics — uncertainty as variability over hypothetical repeated samples — with the Bayesian view of probability as belief about the one dataset actually observed, presents Bayes' theorem in its odds form, and explains why MCMC unlocked HB estimation of complex models. It writes the HB choice model as a three-level hierarchy of "unpacked" algebraic statements (choice = utility maximization; utility linear in attributes; part-worths normally distributed across respondents), argues that HB solves choice-based conjoint's chief objection (aggregate-only utilities) by giving individual-level estimates, showcases Gilbride & Allenby's Bayesian screening-rule (consideration-set) model for digital cameras as an example of models "beyond the basic HB," and closes with practical challenges: lack of off-the-shelf software beyond Sawtooth/WinBUGS/MCMCPack, the "no convergence to a point" mindset shift, burn-in, and distributions rather than point estimates per respondent.

## Key contributions relevant to the book

- Historical framing: paradigm shift since the early 1990s; 50+ HB papers in top marketing journals by 2004 (Executive Summary, p. 22).
- The cleanest verbal statement of frequentist vs. Bayesian probability for a first lecture (pp. 21–22): classical assumes hypothesis H known and maximizes Pr(D|H); Bayes asks "which hypothesis is most likely given the data" and conditions on D.
- Bayes theorem in both forms: Pr(H|D) = Pr(D|H)Pr(H)/Pr(D) (p. 22) and the odds form (posterior odds = likelihood ratio × prior odds) via a quality-inspector sidebar example (p. 25).
- Motivation for HB from data scarcity: rarely more than ~20 conjoint evaluations per respondent; a 15-part-worth, 500-respondent conjoint means 750 [sic — 7,500] parameters, infeasible to handle analytically (p. 22).
- The three-equation hierarchical choice model (p. 23) — the same skeleton the book's HB-MNL chapter builds on.
- Argument that HB's predictive superiority comes from avoiding restrictive assumptions: demographics too coarse, latent-class ("small number of homogeneous segments") more hope than reality — continuous heterogeneity wins (p. 24). Useful for the latent-class-vs-HB discussion.
- Example of richer Bayesian models: Gilbride & Allenby's conjunctive/disjunctive screening-rule model, estimating consideration sets and decision rules jointly with utilities; most digital-camera consumers screen conjunctively, with 40–41% screening on body style and price (Exhibit 1, p. 24).

## Models & notation

- Hierarchical choice model as three "unpacked" levels (p. 23):
  1. Pr(y_ih = 1) = Pr(V_ih + ε_ih > V_jh + ε_jh for all j) — choice = latent utility maximization
  2. V_ih = x_i'β_h — utility linear in attributes
  3. β_h ~ Normal(β̄, Σ_β) — random-effects (heterogeneity) distribution
- No priors on hyperparameters (β̄, Σ_β) are given — the article stops at the random-effects level. Error distribution for ε is left unspecified (logit or probit both fit this skeleton).
- Bayes theorem odds form (sidebar, p. 25): Pr(B+|D)/Pr(B−|D) = [Pr(D|B+)/Pr(D|B−)] × [Pr(B+)/Pr(B−)].

## Estimation details

Deliberately light — this is the article's least technical treatment of MCMC, useful for framing rather than mechanics:
- MCMC described as a Monte Carlo simulator (draws from distributions) coupled with a Markov chain that turns the simulator into "a rather efficient engine for searching the randomly generated distribution"; models written hierarchically and estimated by MCMC = "hierarchical Bayes" (p. 23).
- Bayes' theorem "bridges" analysis across respondents: individual-level utilities borrow strength via Eq. 3 while exactly accounting for all uncertainty (p. 24). Contrast with individual-level OLS on ratings/rankings, which is unreliable with few observations per person.
- Practitioner adjustments (p. 25): HB does not "converge" on a closed-form solution like MNL-MLE; after several thousand burn-in iterations the variance stabilizes but draws still vary; output is a distribution of estimates per respondent, not a point — powerful for uncertainty but complicates market simulation.
- Software landscape circa 2004 (p. 25): Sawtooth Software's two HB programs (CBC/HB and HB-Reg) as the major adoption impetus but limited to standard models; WinBUGS and MCMCPack (R/S) for custom models; complex HB generally requires custom programming.

## Relevance to book chapters

- **Bayes-MCMC intro:** ideal opening-week reading — zero math prerequisites, strong conceptual contrast of frequentist vs. Bayesian inference, the odds-form Bayes example, and the "why MCMC changed everything" narrative. Pairs with (and largely previews) Allenby & Rossi (2006) handbook chapter, which shares several passages verbatim.
- **HB-MNL:** Eqs. 1–3 (p. 23) are the minimal statement of the hierarchical choice model; good for motivating individual-level part-worths in choice-based conjoint before the full `bayesm` treatment.
- **Latent class:** citable for the argument that finite-mixture/segment heterogeneity is usually dominated by continuous (normal) heterogeneity (p. 24).
- **Applications:** screening rules / consideration sets (Gilbride & Allenby 2004) as an example of what Bayesian machinery enables beyond compensatory models; endogeneity (ad budgets set as % of sales) flagged as a frontier (pp. 24–25).

## Page pointers

- p. 20: title page (magazine spread)
- p. 21: classical vs. Bayesian probability; Bayes historical note (1763)
- p. 22: Executive summary; Pr(H|D) formula; three reasons Bayes lagged; conjoint dimensionality example; data-scarcity motivation; overly aggressive share predictions when uncertainty ignored
- p. 23: "HB Models" section — MCMC description; hierarchical model Eqs. 1–3 and their interpretation
- p. 24: bridging across respondents; individual-level utilities vs. aggregate CBC; critique of demographic and latent-class heterogeneity; screening rules and consideration sets; Exhibit 1 (camera attribute screening frequencies)
- p. 25: Bayes' Theorem quality-inspector sidebar; software (Sawtooth, WinBUGS, MCMCPack); no-convergence-to-a-point discussion; burn-in; distributions per respondent; further reading (Gilbride & Allenby 2004; Rossi & Allenby 2003)
