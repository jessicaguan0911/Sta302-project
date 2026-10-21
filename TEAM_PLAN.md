# Team Plan & Division of Work

Four leads, one per area. **"Lead" means you own the deliverable and its deadline — not that you
do it alone.** Every piece of writing gets reviewed by one other member before it is merged
(review pairs below), so everybody touches every section at least once.

## 1. Roles at a glance

| | Role | Owns in Part 1 | Proposal words owned | Owns in Part 2 |
|---|---|---|---|---|
| **A** | Data Lead & Submitter | Dataset vetting, cleaning code, OneDrive CSVs, **Data description** | ~300 | Transformations + assumption fixes; reproducible final Rmd |
| **B** | Literature & Intro Lead | Research question wording, 3 peer-reviewed papers, **Introduction**, bibliography | ~400 | Poster intro/background + discussion & limitations |
| **C** | Modelling & Diagnostics Lead | Preliminary model (≥9 predictors + interaction), residual plots, model table, **Preliminary results** | ~400 | Variable selection, multicollinearity, influential points, final model |
| **D** | EDA, Ethics & Plan Lead | Variable summary table, interaction justification figure, **Ethics** + **Plan** (with Gantt), Part 0 agreement | ~500 | Poster layout & figures; video editing & assembly |

Review pairs (each reviews the other's section before merge): **A ↔ D**, **B ↔ C**.
Everyone: finds ≥ 1 candidate paper, reads the whole proposal once before submission, records their part of the video, writes their own Part 3 reflection.

---

## 2. Detailed tasks — Part 0 + Part 1 (due Thu Nov 5)

### 🅰 A — Data Lead & Submitter
- [ ] Vet candidate datasets against the requirements:
  - open-source with a citable URL; **≥ 1000 rows**; 1 continuous-ish response; **≥ 9 predictors** (≥1 categorical, ≥1 numeric)
  - **not** a textbook dataset, **not** Boston Housing or Red Wine Quality
  - original curator + *how/why it was collected* can be found (if not → drop it)
  - if from Kaggle/UCI: our question must differ from the original use
- [ ] Put the original file in `data/raw/` (never edit it); write the cleaning chunk in `proposal.Rmd`
      (subset, rename, handle missing values, recode categoricals) → writes `data/clean/clean_data.csv`
- [ ] Upload original + cleaned CSV to **UofT OneDrive**, set *"Anyone in UofT with the link"*, test the link from another member's account
- [ ] Write **Data description (≤ 300 words)**: where found, how & why originally collected, response summary + why it suits a linear model (reasonably continuous? observations independent?)
- [ ] Final knit check on a clean R session; **submit all components on Quercus** (one submission only) + post OneDrive link as submission comment

### 🅱 B — Literature & Intro Lead
- [ ] Draft the research question so the **response is defined clearly** and predictors are **named explicitly** (no vague "factors")
- [ ] Collect candidate papers from everyone → choose **3 peer-reviewed** papers; fill a notes file in `literature/` for each
- [ ] Write **Introduction (≤ 400 words)**:
  - research question + why a linear model beats a simpler technique, and *which model output answers it* (coefficients / CI / p-value / prediction)
  - literature woven together by theme (not one paragraph per paper), what each says about response ↔ predictors, and the **gap** we fill
  - who benefits from the model and why
- [ ] Own `references.bib` + in-text citations in **APA**; compile the **Bibliography**
- [ ] With C: write the "compare to literature" sentences in Preliminary results

### 🅲 C — Modelling & Diagnostics Lead
- [ ] Fit the preliminary MLR with **≥ 9 predictors** and **1 interaction (categorical × another variable)**
- [ ] Residual analysis (do **not** fix violations yet!):
  - conditions: response vs fitted plot; pairwise scatterplots of numeric predictors
  - assumptions: residuals vs fitted, residuals vs each predictor, normal QQ plot
  - plots arranged **2–3 per row in one figure** (patchwork / `par(mfrow=)`), with axis labels + captions
- [ ] Model table with estimates **and SE and/or 95% CI** (kable, no raw R output)
- [ ] Write **Preliminary results (≤ 400 words incl. captions)**: verdict for each assumption with the plot that shows it; surprises in sign/size/significance vs the literature

### 🅳 D — EDA, Ethics & Plan Lead
- [ ] Lead the Part 0 meeting, fill [`part0_teamwork_agreement/agreement_draft.md`](part0_teamwork_agreement/agreement_draft.md) → paste into the .docx, collect 4 signatures, export PDF
- [ ] Build the **variable summary table** (every variable in the model) with an informative caption: skew, outliers, nonsense values, spread, missing values
- [ ] Make the **figure/table justifying the interaction** (e.g. response vs numeric predictor coloured by category); if a numeric variable was turned categorical, justify the cut points
- [ ] Write **Ethics (≤ 200 words)**: trustworthiness + ethical collection, using **≥ 1 concept from each** part of the Module 3 ethics module
- [ ] Write **Plan (≤ 300 words)**: how we'll reduce/increase predictors, how often assumptions get re-checked, likely transformations (based on C's plots), predictors we must keep and why, plus a **Gantt chart** with dates and names for analysis, poster and video
- [ ] Final formatting pass: headers, word counts (≤ 15 over max), no R code/output visible

---

## 3. Timeline — Part 1

| Date | Milestone | Who |
|---|---|---|
| **Thu Oct 22** | Kick-off meeting: pick roles, agree on Part 0 answers, shortlist 2–3 datasets | All (D runs it) |
| **Sat Oct 24** | ✅ Dataset + research question **locked** | A, B (all approve) |
| **Sun Oct 25** | Raw data in repo, cleaning code merged | A |
| **Tue Oct 27** | 3 papers chosen + notes done; summary table done; preliminary model fitted | B, D, C |
| **Wed Oct 28** | Teamwork agreement signed (PDF) | D (all sign) |
| **Sun Nov 1** | **First full draft of every section merged** | All |
| **Mon Nov 2 – Tue Nov 3** | Cross-review (A↔D, B↔C), then everyone reads the whole thing once | All |
| **Wed Nov 4** | Final knit, word-count check, OneDrive link tested → **ready to submit** | A, D |
| **Thu Nov 5** | Submit (aim for the afternoon, not 11:58 pm) | A |

## 4. Timeline — Part 2 + 3 (tentative; refine in the Plan section)

| Date | Milestone | Lead |
|---|---|---|
| Nov 9 – 15 | Address assumption violations (transformations), re-check residuals | A |
| Nov 16 – 22 | Variable selection (e.g. partial F-tests, AIC/BIC, adjusted R²), VIF, leverage/outliers/influence; final model chosen | C |
| Nov 23 – 27 | Poster draft (intro, methods, results, discussion, limitations) | D (layout), B (text) |
| Nov 28 – 30 | Script + record video, each member presents a section | D (editing), all record |
| Dec 1 – 2 | Final review of poster + video; Rmd reproduces everything | All |
| **Thu Dec 3** | Submit Part 2 (group) + Part 3 (each person individually!) | A / everyone |

---

## 5. Meetings & communication (to be confirmed in Part 0)

- Weekly 45-min check-in (time: ______), plus a quick async update in our group chat every **Mon / Thu**
- Each task = a GitHub Issue assigned to its lead; move it to *done* by closing the issue via a PR
- Blocked or late? Say so in the chat **at least 24 h before** the task's date — no surprises
