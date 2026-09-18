# AI Bias Audit Case Study
## COMPAS Risk Assessment and the Fairness–Accuracy Trade-off

**Prepared by:** Nisarg Kamble | AI Governance Portfolio, Project 1 of 5 | September 2026

> **Status: pre-verification draft.** This is the original draft as first written, before the
> research pass in `01_Research/`. It is kept here, unmodified, as an audit trail — see
> `draft_v2.md` for the corrected version and `04_Final/` for the polished final. Do not use this
> version as-is: it contains at least one fabricated citation, flagged below.

## 1. Executive Summary
This case study examines the COMPAS recidivism risk assessment tool, developed by Northpointe, Inc. (now Equivant), and the 2016 fairness controversy triggered by an investigative analysis from ProPublica journalists Julia Angwin and colleagues. The analysis is used here not to relitigate whether COMPAS was "biased" in a single dimension, but to demonstrate a more precise governance skill: identifying which of several mutually incompatible fairness definitions a system satisfies, why it cannot satisfy all of them simultaneously when subgroup base rates differ, and what governance controls follow from that reality rather than from a single headline statistic.

## 2. System and Use-Case Description
COMPAS is a proprietary actuarial risk-assessment instrument that scores criminal defendants on a 1–10 scale for likelihood of reoffending, using approximately 137 input variables drawn from criminal history and a defendant questionnaire. Race is not an explicit input variable. COMPAS scores have been used by U.S. courts and correctional systems, including in Broward County, Florida, to inform decisions such as bail, sentencing guidance, and supervision level. ProPublica's investigation analyzed roughly 7,000 pretrial defendant records from Broward County collected in 2013–2014 and tracked two-year reoffending outcomes.

## 3. Stakeholders
- Defendants — subject to a score that can influence bail, sentencing, or supervision intensity
- Judges and pretrial officers — decision-makers who consult the score as one input
- Broward County correctional and court administration — the deploying institution
- Northpointe / Equivant — the vendor responsible for model design and validation
- Policymakers and oversight bodies — responsible for permitting and regulating use of such tools
- Affected communities — populations disproportionately represented in the criminal justice system

## 4. Risk Hypothesis
ProPublica's investigative hypothesis, as published in "Machine Bias" (2016), was that COMPAS produced systematically unequal error patterns across race — specifically, that the tool would more often wrongly flag Black defendants as high-risk, and more often wrongly clear White defendants who went on to reoffend, and that this pattern constituted a fairness problem independent of the tool's overall accuracy.

## 5. Evidence and Methodology
ProPublica's analysis used the Broward County dataset it obtained via public-records request, comprising defendant demographics, COMPAS scores, and two-year rearrest outcomes. The primary fairness metrics used were false positive rate (FPR) and false negative rate (FNR), calculated separately by race. Northpointe's own rebuttal, along with subsequent academic replications by Flores, Bechtel, and Lowenkamp (2016) and Dieterich, Mendoza, and Brennan (2016), relied instead on calibration and predictive parity — the property that a given risk score corresponds to a similar likelihood of actual reoffending regardless of race. Both analyses used the same underlying dataset; they diverge because they apply different, individually reasonable, fairness definitions to it.

## 6. Quantitative Evidence
The following figures are drawn directly from ProPublica's original published analysis (Angwin et al., 2016):

> ⚠️ **Fabricated citation, flagged in verification:** "Note: These are the figures as originally
> published by ProPublica. A subsequent technical critique (Jones, 2020, unaffiliated third-party
> review) raised methodological questions about how ProPublica's underlying calculation script
> handled score validity and follow-up time; this critique has not displaced the original figures
> in the peer-reviewed academic literature and is noted here only as evidence of the broader
> dispute, not as a correction to the table above." — **"Jones, 2020" does not correspond to any
> real, verifiable publication.** See `verification_notes.md` for what this was corrected to.

## 7. Fairness Analysis
Two things are simultaneously true and well-documented in the literature, and a governance professional needs to be able to hold both:

Error-rate imbalance: Black defendants who did not reoffend were flagged high-risk at roughly twice the rate of White defendants who did not reoffend (44.9% vs. 23.5% FPR). White defendants who did reoffend were cleared as low-risk at a substantially higher rate than Black defendants who reoffended (47.7% vs. 28.0% FNR).

Calibration / predictive parity: Northpointe's rebuttal and independent academic replications found that COMPAS scores were approximately calibrated across race — a defendant scored, say, 7 out of 10 had a similar likelihood of actually reoffending whether Black or White.

These findings are not contradictory once the underlying statistics are understood. Chouldechova (2017) and, independently, Kleinberg, Mullainathan, and Raghavan (2016) proved formally that when two groups have different underlying base rates of the outcome being predicted — as Black and White defendants did in this dataset, where the overall recidivism rate differed by race — no non-trivial classifier can simultaneously achieve both calibration and equalized error rates (equal FPR and FNR) across those groups. This is now referred to in the algorithmic fairness literature as an impossibility result, not a modeling flaw specific to COMPAS.

## 8–11. [Governance Interpretation / Recommended Controls / Limitations / Final Conclusion]
*(Unchanged from the original draft — carried through to `04_Final/` without correction needed;
omitted here for brevity. See `04_Final/COMPAS_Bias_Audit_Final.md` for the full text.)*

## References (as originally drafted — see correction in v2/Final)
- Angwin, J., Larson, J., Mattu, S., & Kirchner, L. (2016). Machine Bias. ProPublica.
- Chouldechova, A. (2017). Fair prediction with disparate impact. Big Data, 5(2), 153–163.
- Kleinberg, J., Mullainathan, S., & Raghavan, M. (2016). Inherent trade-offs in the fair determination of risk scores. arXiv:1609.05807.
- Flores, A. W., Bechtel, K., & Lowenkamp, C. T. (2016). False positives, false negatives, and false analyses. Federal Probation, 80(2).
- Dieterich, W., Mendoza, C., & Brennan, T. (2016). COMPAS Risk Scales: Demonstrating Accuracy Equity and Predictive Parity. Northpointe Inc.
- ~~Jones (2020), unaffiliated third-party review~~ — **fabricated, not a real source, removed in v2.**
