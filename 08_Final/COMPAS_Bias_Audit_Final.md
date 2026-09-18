# AI Bias Audit Case Study
## COMPAS Risk Assessment and the Fairness–Accuracy Trade-off

**Prepared by:** Nisarg Kamble | AI Governance Portfolio, Project 1 of 5 | September 2026

---

## 1. Executive Summary
This case study examines the COMPAS recidivism risk assessment tool, developed by Northpointe, Inc. (now Equivant), and the 2016 fairness controversy triggered by an investigative analysis from ProPublica journalists Julia Angwin and colleagues. The analysis is used here not to relitigate whether COMPAS was "biased" in a single dimension, but to demonstrate a more precise governance skill: identifying which of several mutually incompatible fairness definitions a system satisfies, why it cannot satisfy all of them simultaneously when subgroup base rates differ, and what governance controls follow from that reality rather than from a single headline statistic.

## 2. System and Use-Case Description
COMPAS is a proprietary actuarial risk-assessment instrument that scores criminal defendants on a 1–10 scale for likelihood of reoffending. It is commonly reported to use roughly 137 input variables drawn from criminal history and a defendant questionnaire — this figure is widely repeated across secondary sources but could not be independently confirmed against a Northpointe/Equivant primary document, since the full scoring methodology is proprietary; it is presented here as commonly reported rather than verified. Race is not an explicit input variable. COMPAS scores have been used by U.S. courts and correctional systems, including in Broward County, Florida, to inform decisions such as bail, sentencing guidance, and supervision level. ProPublica's investigation analyzed defendant records from Broward County collected in 2013–2014 and tracked two-year reoffending outcomes; ProPublica's own methodology reports the core two-year general-recidivism analysis sample at 7,214 individuals.

## 3. Stakeholders
- **Defendants** — subject to a score that can influence bail, sentencing, or supervision intensity
- **Judges and pretrial officers** — decision-makers who consult the score as one input
- **Broward County correctional and court administration** — the deploying institution
- **Northpointe / Equivant** — the vendor responsible for model design and validation
- **Policymakers and oversight bodies** — responsible for permitting and regulating use of such tools
- **Affected communities** — populations disproportionately represented in the criminal justice system

## 4. Risk Hypothesis
ProPublica's investigative hypothesis, as published in "Machine Bias" (2016), was that COMPAS produced systematically unequal error patterns across race — specifically, that the tool would more often wrongly flag Black defendants as high-risk, and more often wrongly clear White defendants who went on to reoffend, and that this pattern constituted a fairness problem independent of the tool's overall accuracy.

## 5. Evidence and Methodology
ProPublica's analysis used the Broward County dataset it obtained via public-records request, comprising defendant demographics, COMPAS scores, and two-year rearrest outcomes. The primary fairness metrics used were false positive rate (FPR) and false negative rate (FNR), calculated separately by race. Northpointe's own rebuttal — Dieterich, Mendoza & Brennan (2016), "COMPAS Risk Scales: Demonstrating Accuracy Equity and Predictive Parity," published July 8, 2016, roughly seven weeks after ProPublica's article — along with the independent academic rejoinder by Flores, Bechtel & Lowenkamp (2016), relied instead on calibration and predictive parity: the property that a given risk score corresponds to a similar likelihood of actual reoffending regardless of race. Both analyses used the same underlying dataset; they diverge because they apply different, individually reasonable, fairness definitions to it.

## 6. Quantitative Evidence
The following figures are drawn directly from ProPublica's original published analysis (Angwin et al., 2016):

| Metric | Black defendants | White defendants |
|---|---|---|
| False positive rate (flagged high-risk, did not reoffend) | 44.9% | 23.5% |
| False negative rate (flagged low-risk, did reoffend) | 28.0% | 47.7% |

**Note on methodological critique:** These are the figures as originally published by ProPublica. A subsequent, independent technical critique — Barenstein (2019), "ProPublica's COMPAS Data Revisited" (arXiv:1906.04711) — found that ProPublica's data-processing script applied an inconsistent two-year cutoff rule (correctly excluding non-recidivists screened after April 1, 2014, but not applying the equivalent cutoff to recidivists), which inflated the overall measured recidivism rate by roughly 24%. This is a genuine, citable, peer-reviewed-adjacent methodological finding — not a rebuttal of the racial-disparity result itself, which multiple independent replications have separately confirmed — but it is a legitimate caveat on the precision of ProPublica's specific published rate figures, and is noted here for that reason.

## 7. Fairness Analysis
Two things are simultaneously true and well-documented in the literature, and a governance professional needs to be able to hold both:

**Error-rate imbalance:** Black defendants who did not reoffend were flagged high-risk at roughly twice the rate of White defendants who did not reoffend (44.9% vs. 23.5% FPR). White defendants who did reoffend were cleared as low-risk at a substantially higher rate than Black defendants who reoffended (47.7% vs. 28.0% FNR).

**Calibration / predictive parity:** Northpointe's rebuttal and independent academic replications found that COMPAS scores were approximately calibrated across race — a defendant scored, say, 7 out of 10 had a similar likelihood of actually reoffending whether Black or White.

These findings are not contradictory once the underlying statistics are understood. Chouldechova (2017) and, independently, Kleinberg, Mullainathan & Raghavan (2016, arXiv:1609.05807) proved formally that when two groups have different underlying base rates of the outcome being predicted — as Black and White defendants did in this dataset, where the overall recidivism rate differed by race — no non-trivial classifier can simultaneously achieve both calibration and equalized error rates (equal FPR and FNR) across those groups, except in constrained special cases (equal base rates, or a perfectly accurate predictor). This is now referred to in the algorithmic fairness literature as an impossibility result, not a modeling flaw specific to COMPAS. In other words: COMPAS could not have satisfied both fairness definitions at once, given a real difference in base rates between groups, regardless of how the model was engineered.

## 8. Governance Interpretation
What should an AI governance professional conclude from these findings? Three conclusions follow directly from the evidence above, and they are more useful than a single-sentence verdict on whether COMPAS "is biased":

1. **Fairness is a choice of metric, not a single measurable property.** An organization deploying a risk-scoring tool must decide, explicitly and in advance, which fairness definition matters most for the use case — and document that choice and its trade-offs, rather than discovering the trade-off after deployment.
2. **Calibration alone is an insufficient governance standard for high-stakes decisions.** A tool can be well-calibrated in aggregate while still producing materially different real-world consequences (wrongful pretrial detention, unwarranted supervision) for different groups, because error rates are what individuals actually experience.
3. **Base-rate differences between groups are themselves a governance-relevant fact that must be investigated, not assumed to be neutral.** Where base rates differ because of unequal enforcement, reporting, or historical policing patterns rather than genuine differences in underlying behavior, an ostensibly "fair" calibrated model can still encode and reproduce that upstream inequity.

## 9. Recommended Controls
- **Pre-deployment subgroup performance testing** — evaluate both calibration and error-rate parity across all relevant demographic subgroups before go-live, and document which metric(s) were prioritized and why.
- **Independent third-party validation** — do not rely solely on vendor-provided calibration studies (Northpointe's own validation was central to this dispute); commission or require independent replication.
- **Threshold and use-case review** — assess whether a single risk threshold is being applied uniformly for a decision (e.g., pretrial detention) whose consequences are not symmetric across false positives and false negatives.
- **Human oversight and appeal mechanism** — ensure the score functions as one input to a human decision-maker with documented discretion to override, and that defendants have a route to contest a score.
- **Ongoing monitoring** — track subgroup FPR/FNR and calibration post-deployment on an ongoing basis, since population and base-rate shifts over time can change which fairness trade-offs apply.
- **Documentation of fairness-metric selection** — record, at the governance-committee level, which fairness definition was prioritized for this use case and the reasoning, so the decision is auditable rather than implicit.

## 10. Limitations
- **Data limitations:** the analysis relies on rearrest, not reoffense, as the outcome measure — rearrest rates can themselves reflect unequal policing intensity across communities, which is a limitation of the underlying data rather than of either analytical approach. Separately, Barenstein (2019) identified a data-construction inconsistency in ProPublica's own two-year cutoff logic (Section 6) that inflated the measured overall recidivism rate — a limitation of the published dataset's precision, not of the disparity finding itself.
- **Metric limitations:** no single fairness metric (FPR/FNR parity, calibration, predictive parity, demographic parity) captures "fairness" in full; each formalizes a different ethical intuition, and the impossibility results above establish that not all can be jointly satisfied.
- **Causal limitations:** the case study demonstrates statistical disparities and their formal incompatibility; it does not, on its own, establish the causal mechanism by which those disparities arose (e.g., feature proxies for race, upstream policing patterns, or base-rate differences in the underlying population).
- **Context limitations:** findings from a 2013–2014 Broward County dataset should not be assumed to generalize without validation to other jurisdictions, time periods, or versions of the tool.

## 11. Final Governance Conclusion
The COMPAS case does not support the simple claim that "COMPAS is biased" as a settled, single-dimension fact — nor does it support Northpointe's claim that calibration alone resolves the fairness question. The defensible governance conclusion is narrower and more useful: COMPAS exhibited statistically significant error-rate disparities by race (documented above) while also satisfying calibration in aggregate, and these two findings are mathematically compatible only because Black and White defendants in this dataset had different underlying base rates of the outcome being predicted. For an organization considering deployment of a similar tool, the governance takeaway is procedural: fairness-metric selection must be an explicit, documented, pre-deployment decision tied to the specific harms of the use case, subgroup performance must be monitored on an ongoing basis, and no single aggregate statistic — including calibration — should be treated as sufficient proof of fairness for a high-stakes automated decision system.

---

## References
- Angwin, J., Larson, J., Mattu, S., & Kirchner, L. (2016). *Machine Bias.* ProPublica. https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing
- Larson, J., Mattu, S., Kirchner, L., & Angwin, J. (2016). *How We Analyzed the COMPAS Recidivism Algorithm.* ProPublica.
- Dieterich, W., Mendoza, C., & Brennan, T. (2016). *COMPAS Risk Scales: Demonstrating Accuracy Equity and Predictive Parity.* Northpointe Inc. Research Department.
- Flores, A. W., Bechtel, K., & Lowenkamp, C. T. (2016). *False Positives, False Negatives, and False Analyses: A Rejoinder to "Machine Bias."* Federal Probation, 80(2).
- Kleinberg, J., Mullainathan, S., & Raghavan, M. (2016). *Inherent Trade-Offs in the Fair Determination of Risk Scores.* arXiv:1609.05807.
- Chouldechova, A. (2017). *Fair Prediction with Disparate Impact: A Study of Bias in Recidivism Prediction Instruments.* Big Data, 5(2), 153–163.
- Barenstein, M. (2019). *ProPublica's COMPAS Data Revisited.* arXiv:1906.04711.

**Note on evidence verification:** Every source above was independently checked against a live web search in September 2026. One claim from an earlier draft of this document — an "unaffiliated third-party review" attributed to "Jones, 2020" — could not be verified as a real publication and has been replaced with the real, matching, peer-reviewed-adjacent critique it appears to have been describing (Barenstein, 2019). The COMPAS input-variable count ("~137") remains flagged as commonly reported but not independently confirmed, since Northpointe/Equivant's full scoring methodology is proprietary and not published.
