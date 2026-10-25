# Team Plan & Division of Work

## 0. Project at a glance

| | |
|---|---|
| **Dataset** | Hotel Booking Demand — 119,390 bookings × 32 variables from two hotels in Portugal (a **City Hotel** in Lisbon and a **Resort Hotel** in the Algarve), arrivals Jul 2015 – Aug 2017 |
| **Original source** | Antonio, N., de Almeida, A., & Nunes, L. (2019). Hotel booking demand datasets. *Data in Brief, 22*, 41–49. https://doi.org/10.1016/j.dib.2018.11.126 |
| **Download** | TidyTuesday 2020-02-11 (`hotels.csv`, both hotels combined): https://github.com/rfordatascience/tidytuesday/tree/master/data/2020/2020-02-11 |
| **Response (Y)** | `adr` — average daily rate (€ per night) of a **realised (not cancelled)** stay |
| **Interaction** | `lead_time × hotel` — does booking earlier change the price differently at the city vs the resort hotel? |
| **Why it's novel** | Almost all existing uses of this data predict *cancellations* (classification). We model the *price* with linear regression. |

**Draft research question** (B refines it):
> Among realised bookings at a Portuguese city hotel and resort hotel (2015–2017), how is the average daily rate associated with booking lead time, and does this association differ between the two hotels, after accounting for arrival month, length of stay (weekend and week nights), party size (adults, children), meal plan, market segment, customer type, reserved room type, repeat-guest status and number of special requests?

Quick feasibility check already done (all 4 can relax 😌): after cleaning ≈ 73k rows; a trial model with 13 predictors + the interaction gives R² ≈ 0.60, and the `lead_time × hotel` term is clearly significant (city hotel: about −€0.10 per extra day booked ahead; resort hotel: close to zero).

---

## 1. Roles at a glance

| | Role | Name | Owns in Part 1 | Words | Owns in Part 2 |
|---|---|---|---|---|---|
| **A** | Data Lead & Submitter | Jessica Guan | Cleaning code, OneDrive CSVs, **Data description**, final submission | ~300 | log/Box-Cox transformation of ADR, re-checking assumptions |
| **B** | Literature & Intro Lead | | Research question, 3 papers, **Introduction**, bibliography | ~400 | Poster background, discussion & limitations |
| **C** | Modelling & Diagnostics Lead | | Preliminary model, residual plots, model table, **Preliminary results** | ~400 | Variable selection, VIF, outliers/leverage/influence, final model |
| **D** | EDA, Ethics & Plan Lead | | Summary table, interaction figure, **Ethics** + **Plan** (Gantt), Part 0 agreement | ~500 | Poster layout & figures, video editing |

Review pairs (each reviews the other's section before merge): **A ↔ D**, **B ↔ C**.
Everyone: suggests ≥ 1 candidate paper to B, reads the whole proposal once before submission, records their part of the video, writes their own Part 3 reflection.

---

## 2. Detailed tasks — Part 0 + Part 1 (due Thu Nov 5)

### 🅰 A — Jessica Guan · Data Lead & Submitter
- [ ] Put `hotels.csv` in `data/raw/` (never edit it by hand)
- [ ] Cleaning chunk in `proposal.Rmd` → writes `data/clean/hotels_clean.csv`. Agreed rules:
  - keep realised stays only: `is_canceled == 0`
  - drop stays with 0 nights (`stays_in_weekend_nights + stays_in_week_nights == 0`) and `adr <= 0` (complimentary / data errors)
  - `meal`: merge `"Undefined"` into `"SC"` (both mean *no meal package* per the data paper)
  - drop the 1 row with `distribution_channel == "Undefined"` and the 4 rows with `reserved_room_type == "L"`
  - make `arrival_date_month` a factor in calendar order; create `domestic` (= `country == "PRT"`) instead of the 170+-level `country`
  - remove columns that are IDs or only known *after* the stay: `reservation_status`, `reservation_status_date`, `assigned_room_type`, `agent`, `company`, `arrival_date_week_number`, `arrival_date_day_of_month`
  - report the row count after every step (goes in the Data description)
- [ ] Upload raw + clean CSV to **UofT OneDrive**, permission *"Anyone in UofT with the link"*, test the link from a teammate's account
- [ ] **Data description (≤ 300 words)**: where found (cite the paper + TidyTuesday), how and why it was collected (hotels' property-management-system databases, extracted by the authors for research on booking demand / cancellations), summary of `adr` (right-skewed, median ≈ €95), why it suits a linear model (continuous; each row is a separate booking)
- [ ] Final knit on a clean R session; **submit everything on Quercus** + OneDrive link as a submission comment

### 🅱 B — Literature & Intro Lead
- [ ] Polish the research question above (response clearly defined, predictors named — never "factors")
- [ ] Find **3 peer-reviewed** papers; one notes file each in `literature/`. Search terms to start with (Google Scholar / UofT Library):
  - `hotel "advance booking" price "lead time"`, `hotel dynamic pricing evidence`
  - `hedonic pricing hotel room rates regression`
  - `resort vs urban hotel pricing seasonality`
  - also read the data paper (Antonio et al., 2019) for context — it can be cited, but it doesn't count as one of the 3 relationship papers
- [ ] **Introduction (≤ 400 words)**: question; why a linear model (the `lead_time` slope and the `lead_time:hotel` coefficient + CI directly answer it); literature organised by theme; gap = price (not cancellations), city vs resort comparison; who benefits (hotel revenue managers setting early-booking discounts, travellers deciding when to book)
- [ ] Own `references.bib` (APA) + in-text citations; with C, write the "compare to literature" sentences

### 🅲 C — Modelling & Diagnostics Lead
- [ ] Preliminary model, e.g.
  `adr ~ lead_time * hotel + arrival_date_month + stays_in_weekend_nights + stays_in_week_nights + adults + children + meal + market_segment + customer_type + reserved_room_type + is_repeated_guest + total_of_special_requests + domestic`
- [ ] Residual analysis (**do not fix anything yet**):
  - conditions: response vs fitted; pairwise scatterplots of numeric predictors
  - assumptions: residuals vs fitted, residuals vs each predictor, normal QQ — 2–3 plots per row
  - things to look out for with this data: ADR is right-skewed → likely fan shape (non-constant variance) and a heavy right tail in the QQ plot; group bookings (`market_segment == "Groups"`) may share prices → possible correlated errors
  - with ~73k rows almost everything is "significant" → discuss size of effects and CIs, not just p-values
- [ ] Model table with estimates, SE and 95% CI (kable, no raw R output)
- [ ] **Preliminary results (≤ 400 words incl. captions)**

### 🅳 D — EDA, Ethics & Plan Lead
- [ ] Run the Part 0 meeting, fill [`part0_teamwork_agreement/agreement_draft.md`](part0_teamwork_agreement/agreement_draft.md), paste into the .docx, collect 4 signatures, export PDF
- [ ] **Summary table** for every model variable: numeric (mean, SD, min, median, max) + categorical (counts / %); caption points out ADR right skew, very long lead times (> 600 days), rare categories (e.g. `FB` meal, `Aviation` segment), big `adults` values
- [ ] **Interaction figure**: ADR vs lead time, coloured by hotel, with a straight-line fit per hotel → the different slopes justify `lead_time × hotel`
- [ ] **Ethics (≤ 200 words)**: trustworthiness (peer-reviewed data paper, real hotel system records, but only 2 hotels in 1 country → limited generalisability) + ethical collection (data anonymised — no names/IDs; hotels' consent; `country` is sensitive-ish, so we only use domestic vs international). Use ≥ 1 term from each part of the Module 3 ethics module
- [ ] **Plan (≤ 300 words)**: log or Box-Cox transform of ADR; variable selection (partial F-tests, AIC/BIC, adjusted R²); VIF for multicollinearity (e.g. `market_segment` vs `customer_type`); leverage/outliers/influence; must-keep predictors: `lead_time`, `hotel`, their interaction; Gantt chart with names and dates
- [ ] Final formatting pass: headers, word counts (≤ 15 over), no R code/output visible

---

## 3. Timeline — Part 1

| Date | Milestone | Who |
|---|---|---|
| ✅ **Sun Oct 25** | Dataset locked: Hotel Booking Demand | All |
| **Mon Oct 26** | Raw data + cleaning code merged; clean CSV available to everyone | A |
| **Tue Oct 27** | Part 0 meeting held, agreement drafted | D (all attend) |
| **Wed Oct 28** | 3 papers chosen + notes; summary table + interaction figure; preliminary model + residual plots; agreement **signed** | B, D, C, all |
| **Fri Oct 30** | OneDrive link set up and tested | A |
| **Sun Nov 1** | **First full draft of every section merged** | All |
| **Mon Nov 2 – Tue Nov 3** | Cross-review (A↔D, B↔C), then everyone reads the whole thing | All |
| **Wed Nov 4** | Final knit, word counts, link check → **ready to submit** | A, D |
| **Thu Nov 5** | Submit (afternoon, not 11:58 pm) | A |

## 4. Timeline — Part 2 + 3 (tentative; refine in the Plan section)

| Date | Milestone | Lead |
|---|---|---|
| Nov 9 – 15 | Transform ADR (log / Box-Cox), re-check residuals | A |
| Nov 16 – 22 | Variable selection, VIF, leverage/outliers/influence → final model | C |
| Nov 23 – 27 | Poster draft (intro, methods, results, discussion, limitations) | D (layout), B (text) |
| Nov 28 – 30 | Script + record video, each member presents a section | D (editing), all record |
| Dec 1 – 2 | Final review of poster + video; Rmd reproduces everything | All |
| **Thu Dec 3** | Submit Part 2 (group) + Part 3 (each person individually!) | A / everyone |

---

## 5. Meetings & communication (confirm in Part 0)

- Weekly 45-min check-in (time: ______), plus a quick async update in the group chat every **Mon / Thu**
- Each task = a GitHub Issue assigned to its lead; close it via a PR
- Blocked or late? Say so in the chat **at least 24 h before** the task's date — no surprises
