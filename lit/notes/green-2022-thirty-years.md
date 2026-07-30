# Green, Krieger & Wind (2001) — Thirty Years of Conjoint Analysis: Reflections and Prospects

**Full citation:** Green, P. E., Krieger, A. M., & Wind, Y. (2001). Thirty Years of Conjoint Analysis: Reflections and Prospects. *Interfaces*, 31(3, Part 2), S56-S73.
**Type:** Retrospective / historical survey (note: PDF filename says "2022," which is the JSTOR download year; the paper is Interfaces 2001)
**Length:** 19 pages (S56-S73, incl. JSTOR cover)

## One-paragraph summary

The canonical retrospective on conjoint analysis by its founding academic team. It traces conjoint from Luce & Tukey's (1964) conjoint measurement and Kruskal's MONANOVA, through Green & Rao (1971) and the metric dummy-variable-regression era, to the two defining developments of the '80s (choice-based conjoint via McFadden's MNL, and hybrid/adaptive models like Sawtooth's ACA) and of the '90s (hierarchical Bayes individual-level estimation of choice-based models). It lays out the basic machinery — attribute/level definition, fractional factorial/orthogonal designs, four data-collection formats, the vector/ideal-point/part-worth utility models, and buyer-choice simulators — and illustrates impact with the credit-card study, Courtyard by Marriott, and the EZ-Pass design study (forecast 49% take rate vs. 44% actual seven years later). Valuable to the book mostly as historical framing, terminology, and motivation rather than estimation detail.

## Key contributions relevant to the book

- **Historical arc for an intro chapter:** psychometric origins (Luce & Tukey 1964; Kruskal 1965 MONANOVA; LINMAP) → metric conjoint via dummy-variable regression → CBC (McFadden 1974; Louviere & Woodworth 1983) → hybrid/ACA (Johnson 1987) → latent class (DeSarbo et al. 1992) → HB individual-level estimation (Allenby, Arora & Ginter 1995; Lenk et al. 1996) (pp. S62-S66; Table 2 on p. S64 is a dated but handy literature map, 1974-2000).
- **Four data-collection formats** (pp. S58-S59): (1) full-profile ratings, (2) compositional/self-explicated (CASEMAP), (3) hybrid, (4) adaptive (ACA). CBC is treated as the choice-format extension; useful taxonomy when the book explains why choice data ≠ rating data.
- **Three utility models** (p. S60): vector, ideal-point, part-worth — same trichotomy Eggers et al. (2022) use; Figure 2 is the classic picture, Figure 3 shows part-worth plots from the credit-card study (12 attributes, 35 levels, 186,624 combinations reduced to 64 orthogonal profiles — a vivid design-motivation number, pp. S57-S58).
- **CBC framing** (pp. S64-S66): CBC lets analysts model explicit, active competitors (vs. passive/new-market framing of ratings conjoint); "choice-based conjoint studies can be a mixed bleeding" — extensive respondent tasks; originally estimated at total-sample level, with HB later enabling individual differences. McFadden's MNL called "the seminal precursory paper to choice-based conjoint."
- **HB as the most far-reaching '90s development** (p. S66): individuals whose data are self-consistent and distinct from aggregate get more weight from their own data; poorly estimated individuals borrow from the aggregate — a nice plain-language statement of shrinkage/partial pooling for the HB chapter.
- **Simulators as the payoff** (pp. S56, S68-S69): part-worths are entered into buyer-choice simulators to predict response to new/modified products; future-prospects list includes simulator-optimizers for share or financial return and "dynamic" competitive action-reaction simulators.
- **Flagship applications** (pp. S66-S68, Table 3 p. S67): Courtyard by Marriott (50 attributes, 160 levels, hybrid + early CBC, simulators; implemented nearly wholesale) and NJ/NY EZ-Pass (3,000+ respondents, 7 attributes; 1992 forecast 49% take rate vs. 44% actual). Table 3 lists ~20 more (AT&T cellular, ulcer-drug pricing, litigation uses, etc.) — good motivating anecdotes.
- **Software drives diffusion** (p. S69): Sawtooth/Bretton-Clark PC packages made the method ubiquitous — a theme the book echoes with R packages.

## Models & notation

(p. S60, respondent-level, P attributes, J stimuli, y_jp = desirability of attribute p in stimulus j)
- Vector model: s_j = Σ_p w_p·y_jp
- Ideal-point model: preference inversely related to d_j² = Σ_p w_p (y_jp − x_p)², with ideal point x_p
- Part-worth model: s_j = Σ_p f_p(y_jp), f_p estimated at discrete levels; part-worths scaled so lowest level = 0 within attribute, common vertical scale allows summing across attributes (pp. S60-S61)
No formal choice-model math; MNL is discussed by citation (McFadden 1974) only.

## Estimation details

Thin by design — a reflections piece. Estimation history: MONANOVA/LINMAP (nonmetric) supplanted by OLS dummy-variable regression on ratings (pp. S62); CBC estimated by MNL, pooled or latent-class, later HB (pp. S64-S66); hybrid models via stagewise regression on self-explicated plus profile data (pp. S65-S66). No likelihoods, no algorithms. For HB mechanics the paper points to Allenby/Arora/Ginter (1995) and Lenk et al. (1996).

## Relevance to book chapters

- **Conjoint practice / intro:** primary use — a compact history and vocabulary (full-profile, self-explicated, hybrid, adaptive, CBC) plus credibility-building applications (Marriott, EZ-Pass) for motivating students.
- **Choice framework:** the vector/ideal-point/part-worth trichotomy and the rationale for choice tasks with active competitors.
- **Experimental design:** orthogonal-array motivation via the credit-card example (186,624 → 64 profiles); cites Addelman 1962, Plackett-Burman 1946, Huber & Zwerina 1996 efficient-design lineage.
- **MNL:** historical placement of McFadden's model as CBC's engine; Louviere & Woodworth (1983) for design/aggregate estimation.
- **HB-MNL:** the shrinkage intuition paragraph (p. S66) is quotable; positions Allenby/Ginter and Lenk et al. as the key sources.
- **Post-estimation / market simulation:** simulators framed as the point of the whole exercise; EZ-Pass forecast-vs-actual is a rare external-validity data point.
- **Data organization:** not covered.

## Page pointers

- S56: abstract — design → part-worths → simulators pipeline in one paragraph
- S57-S58: basic ideas; credit-card study, Table 1 attributes/levels; orthogonal arrays; 64-profile design
- S58-S59: four data-collection procedures; Figure 1 prop cards
- S60-S61: vector/ideal-point/part-worth models, Figures 2-3; stimulus presentation
- S61-S63: precursors (cluster analysis, MDS); era of conjoint analysis; Monanova/LINMAP → regression; software diffusion
- S64: Table 2 — contributions 1974-2000 (CBC, latent class, HB, designs)
- S64-S66: choice-based conjoint discussion (McFadden, Louviere & Woodworth); hybrid models; '90s HB developments and shrinkage intuition
- S66-S68: applications — Table 3; Courtyard by Marriott; EZ-Pass with forecast accuracy
- S68-S69: future prospects (simulator-optimizers, bundling, web conjoint); software's role; science-vs-engineering postscript
- S70-S73: references
