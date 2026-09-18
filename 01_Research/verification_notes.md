# Verification Notes — COMPAS Bias Audit

Per-claim verification status, resulting from the searches in `research_log.md`.

## Verified as stated — no change needed
- ProPublica's core finding (FPR 44.9% vs. 23.5%; FNR 28.0% vs. 47.7%, Black vs. White
  defendants) matches the primary ProPublica publication.
- Northpointe/Equivant's rebuttal, its calibration/predictive-parity argument, and its July 2016
  publication date are all confirmed against the primary Northpointe technical report.
- The Kleinberg et al. (2016) and Chouldechova (2017) fairness-impossibility citations were
  already present in the original draft and are correctly attributed — no change needed there.

## Flagged and softened — commonly reported, not independently confirmed
- **"~137 input variables."** Repeated across many secondary sources (blogs, law reviews) but
  Northpointe/Equivant's full scoring methodology is proprietary and was not found in any primary
  document during this pass. **Action taken:** reworded in the final draft to state this is
  "commonly reported" rather than presenting it as a confirmed fact. Your call whether to keep,
  soften further, or drop it entirely.

## Flagged and corrected — fabricated citation found
- **"Jones, 2020, unaffiliated third-party review."** This citation, used in the original draft
  to caveat ProPublica's published disparity figures, does not correspond to any real
  publication. **Action taken:** replaced with Barenstein (2019), arXiv:1906.04711 — a real,
  independently authored critique that matches the description (a data-processing issue in how
  ProPublica implemented its two-year recidivism cutoff, inflating the measured recidivism rate
  by ~24%). This is the single most important fix in this project: an unverified/fabricated
  citation in a governance-portfolio document is exactly the kind of error the role you're
  applying for exists to catch.

## Not independently re-verified in this pass (lower risk, flagging for completeness)
- The exact wording and section numbering of Northpointe's rebuttal document (only the title,
  authors, and July 2016 date were directly confirmed against multiple secondary citations of the
  primary source — the primary PDF itself was not fetched and read line-by-line in this pass).
