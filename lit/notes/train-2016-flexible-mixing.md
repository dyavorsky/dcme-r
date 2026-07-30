# Train (2016) — Mixed Logit with a Flexible Mixing Distribution

**Full citation:** Train, K. (2016). "Mixed logit with a flexible mixing distribution." *Journal of Choice Modelling*, 19, 40–53. (Matlab code at http://eml.berkeley.edu/~train/software.html)

**Type:** Methodological journal article — semi-nonparametric mixing distributions for mixed logit ("logit-mixed logit," LML)
**Length:** 14 pages (journal pp. 40–53)

## One-paragraph summary

Most mixed logit applications assume normal or lognormal mixing distributions, which are often unrealistically restrictive. Train proposes the Logit-Mixed Logit (LML) model: discretize the parameter space S into a fine grid and give the probability mass at each grid point β_r a *logit* form, W(β_r | α) = exp(α′z(β_r)) / Σ_s exp(α′z(β_s)), where the researcher-chosen z variables (polynomials, step functions, splines, or combinations) shape the distribution. The logit form guarantees positivity and summation to one, provides the normalizing constant automatically, makes any mixing distribution approximable to any accuracy (via McFadden's mother-logit logic), and yields an easy analytic gradient. Estimation is by maximum simulated likelihood over random subsets S_n of grid points, with a key computational trick: the person-specific conditional likelihoods L_n(β_r) don't depend on α, so they are computed once and reused every optimizer iteration — estimation of a 69-parameter model on 260 respondents took 18 seconds on a GPU. Applied to a video-streaming conjoint (in WTP space), flexible LML distributions reveal bimodal WTP for data-sharing attributes and reject normality (LR statistic 96.02 vs χ²₃₂ critical value 47.40). Estimation here is classical (MSL), but HB estimates are used as MSL starting values, and LML is framed as a generalization of latent class.

## Key contributions relevant to the book

- LML: a single framework nesting and generalizing latent class (grid points = classes with structured, shared shape parameters instead of one free mass per class) — the bridge between the book's mixed-logit and latent-class chapters (Section 4.3, p. 44).
- Double use of the logit formula: one logit for choice given β, one logit for the "selection" of β — elegant and memorable pedagogy (Eqs. 2–3, p. 41).
- Theoretical result (p. 41–42): for any mixing distribution there is a sequence of Eq.-(2) logit distributions converging weakly to it (proof via Chamberlain 1987 discrete approximations + z = log-kernel; McFadden's footnote gives a one-line LLN demonstration).
- Practical z-variable menu (Section 4): second-order polynomial recovers the normal exactly on a grid (Eq. 12, p. 43); Legendre orthogonal polynomials for flexibility with less collinearity (§4.2); overlapping step functions to get marginal shape + correlation with few parameters (13 vs 36 in the 2-D example; Fig. 1, p. 45); linear splines written as α′z(β) (Eq. 14, p. 45); combinations (spline marginals + second-order cross terms for correlation, §4.5); interpretation as method of sieves (§4.6).
- Computational trick — precompute L_n(β_r): the conditional likelihoods never change during optimization; α enters only through weights. The model estimates like "a standard logit with an 'alternative' for each β_r" whose dependent variable is the conditional weight (p. 43).
- WTP-space extension (§5.1, p. 46): replace β′x with −σ_n(r + wtp′x); everything else unchanged — a compact intro to preference-space vs WTP-space.
- Importance sampling of grid points (§5.2, Eqs. 15–16, p. 46): unequal selection probabilities q(β_r) let the researcher widen S and oversample edges.

## Models & notation

- Choice logit given coefficients (Eq. 1, p. 41): Q_ni(β_n) = exp(β_n′x_ni)/Σ_j exp(β_n′x_nj); panels: L_n(β_r) = Π_t Q_{n,i_t,t}(β_r) (Eq. 5, p. 42).
- Mixing distribution as logit over discrete support S (Eq. 2): Prob(β_n = β_r) ≡ W(β_r | α) = exp(α′z(β_r)) / Σ_{s∈S} exp(α′z(β_s)).
- Unconditional probability (Eqs. 3, 6): P_n = Σ_{r∈S} L_n(β_r) W(β_r | α); LL(α) = Σ_n ln P_n (Eq. 7, p. 42).
- Normal as special case (Eq. 12, p. 43): the normal log-density is linear in β and unique elements of ββ′, so z = (β, vech(ββ′)) reproduces it exactly (diagonal case: each element and its square); lognormal via ln β. The constant term drops out in the logit.
- Step functions (Eq. 13, p. 44): partition (possibly overlapping subsets H_g); z = subset indicators; one coefficient normalized to zero.
- Spline (Eq. 14, p. 45): piecewise-linear f(β) written as α′z(β) with hat-function z's; one height normalized (exponentiation makes overall level irrelevant).
- Relation to prior literature (pp. 40–41, 44): approximate generalization of Bajari–Fox–Ryan (2007), Train (2008), Fox et al. (2011) fixed-grid latent class (their parameter count = number of grid points, infeasible for fine grids — 6 points in 7 dimensions is already 279,936 parameters); differs from Fosgerau–Bierlaire (2007) by putting polynomials inside a logit; differs from Fosgerau–Mabit (2013) transformation approach (footnote 2, p. 42).

## Estimation details

- **Maximum simulated likelihood over sampled grid points** (Section 3, pp. 42–43): S can be astronomically large (10²⁴ points in the application), so for each person draw a random subset S_n ⊂ S (equal probability); SLL = Σ_n ln(Σ_{r∈S_n} L_n(β_r) w_n(β_r | α)) with w_n the logit over S_n (Eqs. 8–9). Logit's "uniform conditioning property" means the logit form is preserved on subsets (footnote 4 relates this to McFadden's 1978 subset-of-alternatives sampling; no correction needed here because the "chosen" β is unobserved). Consistent/asymptotically normal if R rises faster than √N (Gourieroux–Monfort, Lee, Train 2009).
- **Analytic gradient** (Eqs. 10–11, p. 43): ∂SLL/∂α = Σ_n Σ_r (h_n(β_r|α) − w_n(β_r|α)) z(β_r), where h_n is the posterior (conditional-on-choices) mass at β_r for person n. Interpretation: at the optimum, z variables are uncorrelated with the difference between each person's posterior and the population weights — the same structure as the logit score. Standard errors: Hessian, BHHH, or sandwich; delta method or bootstrap for functions of α (bootstrap preferred — avoids derivative derivations; p. 43).
- **Computational shortcuts** (p. 43): L_n(β_r) computed once per (n, r) before optimization; only weights are recomputed per iteration. GPU/parallel Matlab implementation.
- **Where Bayes/HB fits in** (Section 6.1, pp. 46–47): the benchmark normal WTP-space model was first estimated by **the HB procedure of Train (2009) modified for WTP space** (Train & Weeks 2005; Scarpa et al. 2008) with a lognormal price/scale coefficient; the HB estimates then served as **starting values for MSL** in Stata (`mixlogitwtp`, ~4 hours; SLL improved from −4017.10 at the HB estimates to −3903.47 at the MSLE). A nice concrete example of HB and MSL as complementary tools.
- **Application** (Section 6, pp. 46–51): Glasgow & Butler video-streaming conjoint; 260 respondents (40 "protestors" dropped), 11 choice situations, 4 services + no-subscription; attributes: price, commercials, speed of availability, catalog, data-sharing policy (Table 1). Grid: mean ± 2 SD from the normal model per dimension, 1,000 points per dimension, |S| = 10²⁴; 2,000 points sampled per person. Polynomial model: 6th-order per parameter + 2nd-order cross terms, 69 parameters, 18 s to estimate (615 iterations from zero starting values), bootstrap (20 resamples) 16 min. Spline model: six-segment splines + 2nd-order cross terms, 83 parameters, ~50 s, 1,669 iterations.
- **Findings** (pp. 47–51): mean WTPs — $1.56/mo to avoid commercials, $3.94 for fast availability, $2.96 for double content, $2.70 to avoid sharing of personal+usage info. Flexible models reveal bimodality (e.g., a subgroup positively values data sharing); LR test of 6th-order vs 2nd-order polynomial LML: 96.02 vs χ²(32) 5% critical 47.40 — normality rejected. SLL: normal −3903.47 (unbounded support), polynomial LML −3864.85, spline −3858.74. Constraining spline endpoints to impose theoretically "correct" signs costs 28 log-likelihood points (−3858.74 → −3886.70) — data can't rule out theoretically implausible tails (p. 51).
- **Caveats** (Section 7, pp. 50–51): researcher must choose the range of S and the z variables; different flexible shapes can fit nearly equally well; tails matter for policy (share of WTP above a threshold) yet are weakly identified — richer data, unequal sampling of S, and study of how summary statistics depend on the assumed range are flagged as open issues.

## Relevance to book chapters

- **Mixed logit:** the state-of-the-art answer to "which mixing distribution?" — worth covering after normal/lognormal HB and MSL treatments; also a clean exposition of MSL mechanics, gradients, and simulation-consistency conditions (Eqs. 5–11).
- **Latent class:** LML *is* a structured latent class model on a fine grid (each point a class, shares tied together by α′z) — ideal for unifying the latent-class and continuous-mixture chapters and for discussing the parameter-proliferation problem of unstructured grids.
- **HB-MNL / Bayes-vs-classical:** documents the practical workflow of using HB output as MSL starting values in WTP space (p. 46–47) and cross-references Train (2009) Ch. 12 HB machinery.
- **Mixed logit / WTP-space:** Section 5.1 is a two-paragraph intro to WTP-space specification (with lognormal price/scale), citing Train & Weeks (2005) and Scarpa et al. (2008).
- **Applications:** the video-streaming conjoint with privacy attributes is a modern, teachable example; bimodal WTP histograms (Fig. 2) make the case that distributional flexibility changes substantive conclusions.

## Page pointers

- p. 40: abstract; motivation — normals/lognormals dominate practice and are limiting; Matlab code footnote
- p. 41: relation to Bajari–Fox–Ryan, Train (2008), Fox et al., Burda et al., Fosgerau–Mabit; LML model — Eq. 1 (choice logit), Eq. 2 (mixing logit), Eq. 3 (double-logit unconditional probability); mother-logit generality result; weak-convergence theorem and McFadden's LLN footnote
- p. 42: proof completion (z as log-kernel, Eq. 4); estimation — panel L_n (Eq. 5), P_n (Eq. 6), LL (Eq. 7), simulated LL over subsets S_n (Eqs. 8–9); consistency conditions; footnote 2 on Fosgerau–Mabit relation
- p. 43: gradient (Eqs. 10–11) and its "uncorrelated with z" interpretation; precompute-L_n trick; standard-logit analogy; Hessian/BHHH/sandwich/bootstrap; §4.1 normal/lognormal as exact logit special cases (Eq. 12)
- p. 44: Legendre polynomials (§4.2); step functions (Eq. 13) and overlapping-subset economy; relation to fixed-grid latent class and its parameter explosion
- p. 45: Fig. 1 (saturated vs overlapping partitions); spline formula (Eq. 14) with hat-function z's; combinations (§4.5); method of sieves (§4.6)
- p. 46: consistency/rates deferred; WTP-space extension (§5.1); unequal-probability sampling (Eqs. 15–16); application data description
- p. 47: Table 1 attributes; HB-then-MSL workflow (SLL −4017.10 → −3903.47); mean WTP results; polynomial specification (10²⁴ grid, 2,000 draws/person, 69 parameters, 18 s GPU, 615 iterations); footnotes 10–12 (estimate normals first; Halton draws; code comparability)
- p. 48: Table 2 (normal vs polynomial vs spline estimates, bootstrap SEs); bimodality discussion
- p. 49: Fig. 2 WTP histograms; significant WTP correlations; LR test 96.02 vs 47.40 rejecting the 2nd-order (normal-shaped) model
- p. 50: spline model (83 parameters, 50 s, 1,669 iterations); correlations replicated; discussion — specification burden, similar LLs across flexible shapes
- p. 51: sign-constrained spline costs 28 LL points; tails weakly identified; four open research topics
- pp. 52–53: references (incl. Train 2008 EM nonparametrics; Train & Weeks 2005; Train 2009 Ch. on HB)
