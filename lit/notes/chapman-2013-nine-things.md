# Chapman (2013) — 9 Things Clients Get Wrong about Conjoint Analysis

**Full citation:** Chapman, C. (2013). 9 things clients get wrong about conjoint analysis. In B. Orme, ed., *Proceedings of the 2013 Sawtooth Software Conference*, Dana Point, CA, October 2013.
**Type:** Practitioner conference paper (reflections from 100+ industry CA projects; author was at Google)
**Length:** 10 pages

## One-paragraph summary

Chapman catalogs nine (plus one) common client misunderstandings about conjoint analysis, drawn from observing/conducting over 100 CA projects. The recurring theme: CBC produces *relative preference* estimates conditional on the attributes, levels, and alternatives tested — not absolute market forecasts, absolute feature worth, or optimal prices. He argues analysts should communicate distributions of individual-level HB estimates rather than average utilities, treat respondents as "tendencies rather than types," and favor multiple smaller studies with varied methods over one giant-N study. All illustrative data come from a didactic R simulation ("Rcbc" R code: design a CBC, simulate choices, estimate via HB-MNL), making it a natural companion to a hands-on estimation book.

## Key contributions relevant to the book

The nine mistakes (with Chapman's corrective one-liners, italicized in the paper):
1. **CA tells us how many people will buy** — no; preference share ≠ market share. Share is computed via the MNL share formula (Table 1, p. 2) but omits awareness, distribution, promotion, competitive response, and the outside good. *"CA assesses how many respondents prefer each product, relative to the tested alternatives."*
2. **CA assesses how good/bad a feature is** — part worths are relative within attribute and conditional on the levels shown; cross-attribute comparisons require rescaling (e.g., zero-centered diffs) and are best resolved in a market simulator. (p. 3)
3. **CA directly tells us where to set prices** — three seductive price-utility patterns (inelastic, elastic, "curved"/reversal; Figure 1, p. 3): flat slopes often reflect method effects understating elasticity; upward-sloping segments usually signal a design/task problem, not genuine preference for high prices. Recommends constrained (monotone-declining) price utilities and multiple methods, incl. incentive-aligned CA (Ding 2007). (pp. 3-4)
4. **The average utility is the best measure** — show the distribution of individual-level HB estimates (Figure 3, p. 5): a low-mean feature may be polarizing (high variance) and right for a portfolio, while a high-mean one is broadly acceptable.
5. **There is a true score** — even within one respondent, MCMC draws show wide within-person posterior uncertainty (Figures 4-5, pp. 5-6); credible intervals overlap heavily. Tendency, not type.
6. **CA tells us the best product to make (easily)** — max-utility products capitalize on error; better to search for many near-optimal products and examine commonalities, or model competitive response — requires custom R code and strong data. (pp. 6-7)
7. **Get as much sample as possible** — CI shrinks with 1/sqrt(N) (diminishing returns) and big-N doesn't fix non-probability sampling bias; prefer several smaller studies with varied methods/samples. (The 60-task CBC schematic, Figure 6, p. 7, is a nice cautionary example on task count.)
8. **Make CA fit what you want to know** — attributes must be things respondents can evaluate (the winemaker CBC parody, Figure 7, p. 8); pretest attributes, levels, and tasks.
9. **(non-mistake) It's better than using our instincts** — a well-designed CA beats expert opinion in expected payoff (Figure 8, p. 9); when data and opinion disagree, run another study.
10. **"Mistake #10" (Chrzan)** — attribute "importance" is design-dependent: adding/omitting an extreme level on one attribute changes every other attribute's importance. (p. 9)

## Models & notation

Not a modeling paper. Uses the aggregate MNL share formula (exp of summed utilities normalized; Table 1, p. 2) and HB-MNL individual-level betas/MCMC draws informally (Figures 3-5).

## Estimation details

Data generated and estimated with the author's "Rcbc" R code (Chapman, Alford, and Ellis 2013): simulated CBC responses, HB multinomial logit estimation via MCMC (p. 2). No new estimation methodology; the value is interpretive practice around HB output (posterior draws, credible intervals, distributions vs. means).

## Relevance to book chapters

- **Conjoint practice:** the core reading — a checklist of interpretation pitfalls for students to internalize before touching client-style questions.
- **Post-estimation / market simulation:** #1, #2, #6 motivate simulators over raw utilities and warn that share simulations are relative preference, not demand forecasts; #10 cautions on "importance" scores.
- **HB-MNL:** #4 and #5 are a direct payoff argument for hierarchical Bayes — the deliverable is the *distribution* of part worths and its posterior uncertainty, not a table of means.
- **Experimental design:** #7 (task count/sample size trade-offs) and #8 (attribute/level formulation, pretesting).
- **Choice framework:** #3's price-reversal discussion connects to constrained/monotone utility specifications and to incentive alignment.

## Page pointers

- p. 1: abstract; intro; footnote 1 lists published CA validity/success references
- p. 2: MNL share calculation (Table 1); Rcbc R code provenance; Mistake #1
- p. 3: Mistakes #2-#3; Figure 1 price-utility patterns
- p. 4: price reversals as red flags; Mistake #4; Table 2 average utilities
- pp. 5-6: Figures 3-5 — distributions of HB betas across and within respondents; Mistake #5
- pp. 6-7: Mistake #6 product optimization; Mistake #7 sample size, Figure 6 (60-task CBC)
- p. 8: Mistake #8, wine CBC (Figure 7); pretesting plea
- p. 9: Mistake #9 data vs. instinct (Figure 8); Chrzan's #10 on attribute importance
- p. 10: conclusion; references (Ding 2007 incentive alignment; Chapman & Alford 2010 portfolio search)
