# Research Log — COMPAS Bias Audit
Date: 2026-09-13

Dated log of what was searched, in order, and why. See `verification_notes.md` for the
resulting verification status of each claim in the draft.

## Search 1 — "ProPublica Machine Bias COMPAS methodology 2016 Broward County"
Purpose: verify the original study's dataset, methodology, and headline finding before citing them.
Result: Confirmed ProPublica (Angwin, Larson, Mattu, Kirchner, May 2016) analyzed COMPAS scores
for Broward County, Florida defendants assessed in 2013–2014, tracking two-year reoffending.
Headline finding: Black defendants who did not reoffend were misclassified as high-risk at
roughly twice the rate of White defendants who did not reoffend (45% vs. 24% in ProPublica's
own published numbers).

## Search 2 — "Kleinberg Mullainathan Raghavan 'Inherent Trade-Offs' fairness impossibility 2016"
Purpose: verify the academic source for the fairness-impossibility claim before attributing it.
Result: Confirmed — Kleinberg, Mullainathan & Raghavan, "Inherent Trade-Offs in the Fair
Determination of Risk Scores" (arXiv:1609.05807, Sept 2016; published ITCS 2017). Proves it's
mathematically impossible to satisfy calibration and equalized error rates simultaneously except
in constrained special cases (equal base rates, or a perfectly accurate predictor).

## Search 3 — "Northpointe 'COMPAS Risk Scales' Dieterich Mendoza Brennan response ProPublica 2016"
Purpose: verify the vendor's actual rebuttal — title, authors, date, and core argument.
Result: Confirmed — Dieterich, Mendoza & Brennan, "COMPAS Risk Scales: Demonstrating Accuracy
Equity and Predictive Parity" (Northpointe Inc. Research Dept., dated July 8, 2016). Core
argument: the FPR/FNR disparity is a mathematical consequence of different base rates of
reoffending between Black and White defendants in the sample, not evidence the tool itself is
racially miscalibrated.

## Search 4 — "Jones 2020 COMPAS ProPublica methodology critique 'follow-up time' score validity"
Purpose: the original draft cited "Jones, 2020, unaffiliated third-party review" for a critique
of ProPublica's handling of score validity and follow-up time. This citation looked generic, so
it was checked directly rather than taken at face value.
Result: No such paper exists under this description. Flagged as a fabricated citation.

## Search 5 — "Rudin Wang Coker 'age of secrecy and unfairness' COMPAS recidivism 2020" and
"Barenstein 2019 'ProPublica's COMPAS Data Revisited' two-year window arXiv"
Purpose: find the real paper "Jones, 2020" appears to have been standing in for, since the
description (a critique of ProPublica's two-year follow-up handling) matches a known, real
critique.
Result: Confirmed — Barenstein (2019), "ProPublica's COMPAS Data Revisited" (arXiv:1906.04711).
Found that ProPublica applied an inconsistent two-year cutoff rule (correctly excluding
non-recidivists screened after April 1, 2014, but not applying the equivalent cutoff to
recidivists), inflating the measured two-year recidivism rate by roughly 24%. This is the real,
citable, independently-authored critique — used in the final draft in place of "Jones, 2020."
