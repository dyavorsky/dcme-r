# Ben-Akiva, McFadden & Train (2019) — Foundations of Stated Preference Elicitation: Consumer Behavior and Choice-based Conjoint Analysis

**Full citation:** Ben-Akiva, M., McFadden, D., & Train, K. (2019). "Foundations of Stated Preference Elicitation: Consumer Behavior and Choice-based Conjoint Analysis." *Foundations and Trends in Econometrics*, 10(1–2), 1–144. DOI: 10.1561/0800000036.
**Type:** Monograph / comprehensive methodological review (economics-grounded treatment of CBC)
**Length:** 144 pages (10 chapters + appendix)

## One-paragraph summary

The definitive economics-first treatment of choice-based conjoint (CBC). The monograph reviews the history of stated preference methods (Ch. 1), gives a nine-point checklist for CBC study design — familiarity, sampling, outside option, menu design, attribute formatting, elicitation frame, incentive alignment, subject training, calibration (Ch. 2, Table 2.1, p. 13) — then builds the full random-utility apparatus: money-metric/WTP-space utility, choice-probability-generating functions, flat and mixed MNL for "portfolios" of menu choices (Ch. 3), and estimation by maximum simulated likelihood (Ch. 5) and hierarchical Bayes (Ch. 6), including a detailed exposition of the Allenby–Train Gibbs/Metropolis–Hastings procedure and NUTS/Stan, validated in a Monte Carlo study and an empirical video-streaming CBC (Ch. 7). Later chapters extend HB to inter- and intra-consumer heterogeneity (Ch. 8) and show how estimated models feed demand, pricing, and welfare/policy analysis (Ch. 9). Bottom line (Ch. 10): model utility in WTP-space, use mixed logit adapted to the panel structure of CBC data, and estimate with HB (Allenby–Train or NUTS), which is fast and nearly identical to ML in practice.

## Key contributions relevant to the book

- The clearest bridge between the marketing practice of conjoint and formal discrete-choice econometrics; ideal background reading for a course on estimating logit/MNL/mixed-MNL from conjoint data.
- Careful economic treatment of the **outside ("no purchase") option** (§2.1.3, pp. 16–18): for a neoclassical consumer, buying means max purchase utility exceeds the option value of "no purchase" (future opportunities). A CBC without a no-purchase option can predict shares but not category demand; the two remedies are (i) external calibration of the no-purchase utility to market data, or (ii) including a no-purchase alternative in the menus.
- Explicit discussion of the **dual-response idea** (p. 18): "ask first for the best product choice from a menu without a 'no purchase' option, and follow up the response by asking if the subject would in fact buy this chosen product." Advantage: prevents respondents from using no-choice to avoid effort. Drawbacks: unless strong separability holds, forced-choice probabilities need not coincide with purchase-conditioned probabilities, and the conditional choice may color the stated purchase decision.
- Stresses that the *meaning* of "no purchase" must be made specific and explicit to respondents (p. 18) or forecasts fail mechanical accounting consistency.
- Concrete worked example (table grapes, §2.2, pp. 30–34) showing menu design, incentive alignment, and the long-format estimation data layout.
- Side-by-side MSL vs HB comparison on the same data, with run times and practical tuning advice — directly relevant to an R-based estimation course (R code for all procedures at https://eml.berkeley.edu/~train/foundations_R.txt, cited pp. 79, 84).

## Models & notation

- Notation summary: Table 3.1 (p. 41). Menus m = 1,...,M; alternatives j ∈ J_m including in general a "no purchase" alternative whose attributes and price are **normalized to zero** (p. 40).
- **Money-metric / WTP-space utility** (Eq. 3.1, p. 45): u_jm = I − p_jm + X(W,A,T−p_jm,s,z_jm)β(ρ_m) + σ(ρ_m)ε_j, with U(...|j0) ≡ I for the designated no-purchase alternative — so the outside good's utility is just (unspent) income and its systematic part-worth is zero by construction. WTP-space vs preference-space normalizations discussed pp. 43–46.
- **Expected maximum utility / CPGF** (Eq. 3.2, p. 51) with logsum form under i.i.d. EV1; choice probabilities as its gradient (Eq. 3.3, p. 52).
- **Mixed MNL** (Eqs. 3.4–3.5, p. 53); **flat MNL** with homogeneous (σ, β) (Eq. 3.6, p. 53), with the j = 0 outside alternative appearing in the denominator sum from k = 0.
- **Portfolio (panel) likelihood** for a respondent's whole sequence of menu choices: mixed MNL with the taste draw held fixed across menus (Eqs. 3.7–3.9, p. 55) — the "nearly neoclassical" random-effects model that is the monograph's workhorse; Eq. 3.10 (p. 56) gives the conditional (individual-level posterior) taste distribution given observed choices.
- Ch. 8 three-level model: population (μ, Ω^b), individual (ζ_n, Ω^w), menu-level ρ_mn for intra-consumer taste perturbations (p. 98).

## Estimation details

- **Flat MNL log-likelihood** over subjects × menus × alternatives (Eq. 5.1, p. 61) — includes the j = 0 outside alternative in the choice-set sum.
- **Mixed logit likelihood** as an integral over the taste distribution (Eq. 5.2, p. 62); BHHH iteration (Eqs. 5.4–5.5, p. 62); MSL and method-of-simulated-scores with R simulation draws, requiring R to rise faster than √(MN) (p. 63); analytic gradients for the multivariate-normal case (Eqs. 5.6–5.7, p. 64). Software pointers: Stata `mixlogit`/`mixlogitwtp`, and Train's Matlab/Gauss/R MSL code (p. 65, fn. 3).
- **HB (Ch. 6):** Bayes asymptotics and MLE-equivalence (§6.1, pp. 67–68); conjugate priors — Dirichlet for multinomial, Normal/inverted-Wishart for the taste distribution (§6.2, p. 69); survey of A/R sampling, slice sampling, Metropolis–Hastings, Gibbs, annealing, and HMC/NUTS (pp. 72–78).
- **Allenby–Train procedure** (pp. 80–81): three-layer Gibbs — (1) draw μ | Ω, ζ_n (normal); (2) draw Ω | μ, ζ_n (inverted Wishart with dof T+N); (3) MH step for each respondent's ζ_n with normal jumping distribution, acceptance tuned to ≈ 0.30. Sign restrictions imposed by exponentiation/censoring of components of ζ (p. 80).
- **NUTS/Stan** alternative (pp. 81–82) with LKJ prior on the correlation matrix; noted as best general-purpose but out-performed by Allenby–Train when normality permits Gibbs steps (p. 79).
- Monte Carlo (grapes, §6.4, pp. 83–90): 1,000 subjects × 8 menus, WTP-form utility (Eq. 6.15, p. 84) with a purchase-alternative dummy B_jmn (the no-purchase alternative gets zeros). All three estimators (HB-AT, HB-NUTS, MSL) recover truth (Table 6.3, pp. 87–89); run times: HB-AT 12 min, MSL ~3 hrs, NUTS overnight (pp. 86, 90). Two cautions: the inverted-Wishart prior is informative (data scaling needed) and weakly identified models need very long chains — 200K iterations, thin 10 (p. 108).
- Empirical study (Ch. 7, video streaming, 260 respondents, 11 menus, 4 services + "no service" fifth alternative): WTP-space HB (Table 7.2, p. 94) vs MSL (Table 7.3, p. 95) closely agree on means; preference-space vs WTP-space comparison shows preference space fits better (LL −3863.9 vs −3903.5) but yields implausible WTP dispersion (mean $6.99, sd $98.95 vs $2.71, sd $6.75 in WTP-space), mirroring Train & Weeks 2005 (p. 96).
- Ch. 8 five-step Gibbs sampler for inter+intra-consumer heterogeneity (pp. 99–100); ignoring intra-consumer heterogeneity inflates estimated inter-consumer heterogeneity and shrinks the scale parameter (Tables 8.4–8.5, pp. 106–107).
- Ch. 9: policy simulation with synthetic populations (pp. 111–113), demand/revenue derivatives and MNL elasticity formulas (Eqs. 9.1–9.4, pp. 114–115), welfare analysis discussion (pp. 115–116).

## Relevance to book chapters

- **Choice framework:** Ch. 3 is a rigorous RUM foundation (utility, CPGF, IIA discussion p. 53, WTP-space vs preference-space) — the theory backbone for the book's framework chapter.
- **Data organization:** Table 2.3 (p. 32) shows exactly the long-format (subject, menu, alternative, choice-indicator, attributes) layout the book teaches; the no-purchase row has all-zero attributes and a "bunch intercept" dummy = 0.
- **Likelihood construction:** Eqs. 5.1–5.2 give flat-MNL and mixed-logit likelihoods including the outside alternative; Eq. 3.7–3.9 formalize the panel/portfolio structure.
- **MNL:** Eq. 3.6 (flat MNL) and the grape example.
- **HB-MNL:** Ch. 6 is one of the best compact expositions of the Allenby–Train sampler and its comparison with NUTS and MSL; directly parallels bayesm-style estimation in R.
- **Conjoint practice:** Ch. 2's design checklist (familiarity, incentive alignment, outside-option wording) is the practice-oriented framing for the book's conjoint application chapter.

## Page pointers

- CBC design checklist: Table 2.1, p. 13
- Outside option / no-purchase discussion + dual-response format: §2.1.3, pp. 16–18
- Grape CBC example, menu and data layout: pp. 30–34 (Tables 2.2, 2.3)
- Utility notation and money-metric utility: Table 3.1 p. 41; Eq. 3.1 p. 45
- Choice probabilities, MNL, mixed MNL, portfolios: pp. 51–56 (Eqs. 3.2–3.10)
- MSL: pp. 61–65 (Eqs. 5.1–5.7); software footnote p. 65
- HB: Bayes basics pp. 67–71; MCMC methods pp. 72–78; Allenby–Train pp. 80–81; NUTS pp. 81–82; Monte Carlo pp. 83–90
- MSL vs HB empirical comparison: pp. 91–97; WTP-space vs preference-space p. 96
- Inter/intra-consumer heterogeneity five-step Gibbs: pp. 98–101
- Policy/demand/welfare analysis: pp. 109–116
- Conclusions and recommendations: pp. 117–118
- R code: https://eml.berkeley.edu/~train/foundations_R.txt (pp. 79, 84)
