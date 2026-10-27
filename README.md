# STA302 Final Project (Fall 2026) — Group # ___

Linear regression analysis of an open-source dataset. This repo holds everything for
Part 0 (teamwork agreement), Part 1 (proposal), Part 2 (poster + video) and Part 3 (individual reflections).

> 📌 **Start here:** [`TEAM_PLAN.md`](TEAM_PLAN.md) — who does what, by when.
> 🔧 **How we use Git:** [`CONTRIBUTING.md`](CONTRIBUTING.md)

## Team

| Role | Name | GitHub | UofT email |
|---|---|---|---|
| **A — Data Lead & Submitter** | Jessica Guan | @jessicaguan0911 | |
| **B — Literature & Intro Lead** | Estella Zhang | @estellazhang0504 | |
| **C — Modelling & Diagnostics Lead** | Cathy Zhong | @Cathy-Zhong | |
| **D — EDA, Ethics & Plan Lead** | Jesse Zhan | @JunzheZhan | |

## Deadlines (all 11:59 pm ET)

| Part | What | Due | NQA extension | Weight |
|---|---|---|---|---|
| 0 | Teamwork agreement (PDF, signed) | **Thu Nov 5** | Sun Nov 8 | −1 mark on Part 1 if missing |
| 1 | Research proposal (PDF + Rmd + CSVs on OneDrive) | **Thu Nov 5** | Sun Nov 8 | 12.5% |
| 2 | Poster + video presentation | **Thu Dec 3** | Sun Dec 6 | 12.5% |
| 3 | Individual group-work reflection | **Thu Dec 3** | Sun Dec 6 | −1 mark on own Part 2 if missing |

⚠️ **Our internal deadline for Part 0 + Part 1 is Wed Nov 4, 11:59 pm** — one day of buffer.
Using the NQA extension needs **all 4 members to agree**, and only one dropbox should be used.
Group problems must be emailed to sta302@course.utoronto.ca **≥ 5 business days** before a due date.

## Repo layout

```
.
├── TEAM_PLAN.md                  # roles, task list, timeline, checklists
├── CONTRIBUTING.md               # branch / PR / review rules
├── part0_teamwork_agreement/     # draft answers → paste into the .docx, sign, export PDF
├── literature/                   # one notes file per paper (use the template)
├── data/
│   ├── raw/                      # original download — never edit by hand
│   └── clean/                    # produced by proposal.Rmd only
├── proposal/
│   ├── proposal.Rmd              # THE submission: knits to the proposal PDF
│   └── figures/
├── poster/                       # Part 2
└── reflections/                  # Part 3 (individual, optional to store here)
```

## Part 1 submission checklist (one person submits everything)

- [ ] Signed teamwork agreement — **PDF**
- [ ] Proposal — **PDF** (knitted from `proposal/proposal.Rmd`, no R code/output except plots)
- [ ] Code — **`.Rmd`** that reproduces every table/figure from the provided data
- [ ] Original + cleaned **CSV** on **UofT OneDrive**, link permission *"Anyone in UofT with the link"*,
      pasted as a **submission comment** on Quercus
- [ ] Every member's name + contribution in the *Contributions* section
