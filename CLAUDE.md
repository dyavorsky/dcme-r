# CLAUDE.md

Quarto book: **"Discrete Choice Model Estimation with R"** (dcme-r). Teaches first-year PhD students to estimate discrete choice models (logit, MNL, MNP, mixed / hierarchical Bayes) by hand-coding everything in R. The *estimation* is the point, not the models per se; the reader should finish able to build and estimate custom models. Published at dcme-r.danyavorsky.com from `docs/` (GitHub Pages).

## Build

- Full book (HTML + PDF): `quarto render` — output to `docs/`; PDF via pdflatex (TinyTeX).
- One chapter: `quarto render chapters/NN_name.qmd --to html` (renders within book context).
- `freeze: auto` — chapter code re-executes only when its qmd changes. MCMC/MSL chapters (13, 15, 17, 19, 20, 22) take minutes each on first execution.
- **Cold-start render order matters**: chapters save/load data artifacts in `data/` (`laptop_study.rds` ← ch 7, `mixed_study.rds` ← ch 13, `mnp_study.rds` ← ch 18, `hb_mnl_fit.rds` ← ch 17). Book-order rendering satisfies all dependencies; single-chapter renders require the upstream .rds files to exist.
- R packages needed to execute: ggplot2, mlogit, dfidx, gmnl, mixl, Rchoice, bayesm, mvtnorm, ordinal, pdftools (page counts).

## Structure

Five parts, 22 chapters + appendix (see `_quarto.yml`): I Foundations (1–6) → II MNL by likelihood (7–14, ends at "limits of likelihood" pivot) → III MNL by Bayes (15–17, HB-MNL is the book's centerpiece) → IV MNP (18–20, both estimation routes) → V post-estimation + extensions (21–22). The narrative arc: climb the likelihood mountain until person-specific parameters break it, then rebuild on Bayes.

## Conventions (do not drift)

- **Notation registry**: the appendix's notation table (`@tbl-notation` in `chapters/appendix.qmd`) is authoritative. Highlights: n/t/j/k/r/s index people/tasks/alternatives/parameters/draws/MCMC-iterations; `\bfbeta`, `\x`, `\y`, `\beps`, `\bftheta` macros (defined in `latex-header.tex`); true values get `^\ast`; estimates get hats — **always brace hats over bold macros**: `\hat{\bftheta}` (pdflatex rejects `\hat\bftheta`).
- **Running example**: one laptop CBC study threads the whole book. Brands Acer/Dell/Apple, ram 8/16/32, screen 13/15, price $0.8–2.4k. True parameters: dell .5, apple 1.0, ram16 .6, ram32 .9, screen15 .3, price −1.2; mixed sds (apple, ram32, price) = (.8, .6, .7); nested λ = .5; MNP Ω has Acer–Dell correlation .6. New examples must extend this study, not introduce new domains.
- **Code style**: base R + ggplot2 (`theme_minimal()`), `set.seed()` in every stochastic chunk, transparent loop version before vectorized version, stacked-matrix data representation (X + `task_id` + 0/1 `choice`), log-sum-exp max-shifts in every softmax, validation against a package or independent implementation in every estimation chapter, chapters end with "## Key Learnings". No exercises.
- **Prose style**: conversational first person, direct address, footnoted asides, `---` em-dashes, cite `@train2009`/`@hrg2015` etc. but never abbreviate as DCMS/ACA (removed by design). Derivation standard: every asserted result is either derived step-by-step or explicitly cited-not-derived.
- Every chapter starts with the `::: {.content-hidden}` latex-header include block and a hidden ggplot2 setup chunk.

## Reference material

- `lit/notes/` — summaries with page pointers for all 29 lit PDFs; `lit/notes/INDEX.md` ends with a topic→source map. The `lit/` PDFs are copyrighted: **never commit them**.
- `_drafting-notes.md` — working conventions, per-chapter progress log, validation results, known quirks.

## Gotchas

- PDF (pdflatex + scrreprt + mathastext): no `\rm`-style old font commands (use `\mathrm`); no literal Unicode math (`≈` → `$\approx$`); brace `\hat{...}` over bold macros. MathJax tolerates all three, so HTML success does not imply PDF success.
- `gmnl`'s latent-class model is broken against current mlogit (fails on its own docs example) — ch 11 validates EM vs direct BFGS instead, documented in a footnote.
- `bayesm::rmnpGibbs` differencing base is alternative *p* (last), and this dev version wants `lgtdata[[i]]$X` as a list of per-task matrices — both handled in ch 17/19.
- Site domain: `dcme-r.danyavorsky.com` everywhere (root `CNAME`, `_quarto.yml` site-url, index colophon). The `CNAME` previously read `dcms-r`, which has no DNS record and left Pages serving a 404 — reconciled 2026-07-30.
- R's lazy argument evaluation breaks naive timing harnesses (`system.time(expr)` inside `replicate`) — ch 9 documents the fix.

## Progress ledger

- 2026-07-03: Book restructured to the 5-part/22-chapter plan (committed: "Update book structure."). Literature notes built (`lit/notes/`). Heading skeletons drafted for all chapters.
- 2026-07-04/05: **Full text drafted for all 22 chapters + appendix** with executed code, figures, simulate-and-recover throughout. Dan's choices: laptops example, ggplot2, no exercises, realistic MCMC chains. Every estimator validated (mlogit ch 8/10/13; EM-vs-BFGS ch 11; pmvnorm ch 19; bayesm ch 17/19; two-route agreement ch 19).
- 2026-07-05/06: **Notation & exposition consistency pass**: 5 reviewers, ~85 findings, all fixes applied (details in `_drafting-notes.md`). Caught: ch 9 timing-harness bug, ch 10 wrong IIA-boundary claim, ch 12 Halton comment/code mismatch, several notation collisions; added ~20 written-out derivations.
- 2026-07-06: **Final render verified**: HTML clean (0 crossref warnings), PDF builds at 260 pages. All drafting work is **uncommitted** in the working tree, awaiting Dan's read-through.
- NEXT: Dan reads the draft; revision passes; commit when approved.
