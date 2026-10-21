# How we use this repo

Never used Git before? That's fine — the short version is: **pull, branch, commit, push, open a PR.**

## Everyday workflow

```bash
git checkout main && git pull          # 1. get the latest version
git checkout -b B/intro-draft          # 2. new branch: <your letter>/<what-you-are-doing>
# ... edit files, knit to check it runs ...
git add proposal/proposal.Rmd
git commit -m "Intro: first draft of literature paragraph"   # 3. small, clear commits
git push -u origin B/intro-draft       # 4. push
```
5. On GitHub, open a **Pull Request** into `main`, write `Closes #<issue number>`, and request your review partner
   (A ↔ D, B ↔ C).
6. Reviewer leaves comments or approves → author merges.

## Rules

- **Don't push straight to `main`.** Everything goes through a PR so someone else has read it.
- **Merge conflicts in `proposal.Rmd`:** each person edits only their own section between the
  `<!-- ===== X START ===== -->` / `<!-- ===== X END ===== -->` markers. This avoids almost all conflicts.
- **Never edit `data/raw/`.** All cleaning happens in code so the grader can reproduce it.
- **Before opening a PR, knit `proposal.Rmd`.** If it doesn't knit, it isn't ready.
- Don't commit `.html` / `.pdf` knits or `.Rhistory` (the `.gitignore` handles this). The final PDF is made on submission day.
- Large data (> 50 MB)? Don't commit it — keep it on OneDrive and note the link in `data/README.md`.

## Writing tips that the rubric rewards

- Name predictors explicitly ("age, BMI, smoking status"), never just "factors".
- Every claim about an assumption points to a specific plot ("Figure 2b shows a fan shape → non-constant variance").
- Use course vocabulary: *conditional mean response*, *linearity*, *uncorrelated errors*, *constant variance*, *normality*.
- Keep each section within its word limit (≤ 15 words over is tolerated). Check with the word count in the knitted PDF.
