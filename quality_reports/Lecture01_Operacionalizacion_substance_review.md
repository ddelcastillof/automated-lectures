# Substance Review: Lecture01_Operacionalizacion.tex
**Agent:** domain-reviewer
**Date:** 2026-04-05
**Domain:** Clinical Research Methods / Epidemiology (introductory)
**Audience:** Medical students in early-stage research seminar (ADIECS, UNMSM)

---

## Summary

Content is accurate and appropriate for the target audience. One medium citation error identified (Bland 1986 cited for Kappa). Two low-level issues with implicit assumptions (sex-specificity of body fat threshold, hard-coded ≥6 rule for discrete variables). All statistical and clinical claims are defensible at the introductory level.

---

## Claim-by-Claim Review

### MEDIUM (1)

**SM1 — Bland 1986 cited for Kappa de Cohen and ICC (both files)**

The citation `[@Bland1986-di]` / `\cite{Bland1986-di}` is placed after "Kappa de Cohen, coeficiente de correlación intraclase (CCI)" in the Precisión slide. The Bland & Altman (1986) Lancet paper is about method agreement via limits of agreement, not about Kappa or ICC as reliability statistics.

Correct citations:
- **Kappa de Cohen:** Cohen, J. (1960). A coefficient of agreement for nominal scales. *Educational and Psychological Measurement*, 20(1), 37–46.
- **ICC:** Shrout, P. E., & Fleiss, J. L. (1979). Intraclass correlations: Uses in assessing rater reliability. *Psychological Bulletin*, 86(2), 420–428. OR McGraw, K. O., & Wong, S. P. (1996). Forming inferences about some intraclass correlation coefficients. *Psychological Methods*, 1(1), 30–46.

*Recommendation:* Add Cohen 1960 and a standard ICC reference to Bibliography_base.bib. Update the Precisión slide to cite Cohen for Kappa and Shrout & Fleiss (or McGraw & Wong) for ICC. Bland 1986 is still relevant to the broader lecture theme and should remain in the bibliography.

### LOW (3)

**SL1 — Body fat 34% = "Obesidad": sex/population assumption not stated**
The case table classifies 34% body fat as "Obesidad." This classification is appropriate for adult women (obesity threshold ~32–35% depending on the guideline) but would not constitute obesity in men (threshold ~25–28%). The fictional case does not specify sex. For a teaching example intended to show that different measures give different classifications, this works pedagogically — but adding a footnote "(asumiendo paciente femenina)" would prevent students from internalizing incorrect cut-points.

**SL2 — "≥6 valores posibles → se comporta como continua": presented as a rule, not a heuristic**
The ≥6 cutoff for treating a discrete variable as continuous is a widely-cited pedagogical heuristic (Norman & Streiner tradition) but lacks a precise mathematical basis. The actual criterion depends on sample size, distribution shape, and the specific analysis. Presenting this as a hard rule ("tipicamente ≥6") is standard at introductory level, but adding "(regla empírica)" would be accurate.

**SL3 — Kappa thresholds (Landis & Koch) presented as definitive**
The cutoffs <0.4 / 0.4–0.6 / 0.6–0.8 / >0.8 are from Landis & Koch (1977) and are widely used. However, they are explicitly described by those authors as "arbitrary" standards. Cicchetti (1994) uses slightly different cutoffs. For an introductory course, the Landis & Koch thresholds are fine. Adding "(Landis & Koch, 1977)" as the source of the table would be more academically precise.

---

## Positive Findings

- The distinction between precision (random error) and accuracy (systematic error/bias) is correctly and consistently maintained throughout.
- Cistatina C vs. creatinina example is clinically accurate and up-to-date. Cystatin C is now recommended by KDIGO 2012 guidelines as a supplement to creatinine for GFR estimation, particularly in patients with altered muscle mass.
- The "regla de oro" for preferring continuous variables over dichotomized ones is strongly evidence-based (see Altman & Royston 2006 for quantification of the power loss; the Browner attribution is appropriate).
- The "fenómeno de interés → medición" framework is consistent with standard measurement theory (Michell 1999; Browner 2022).
- All clinical examples (obesity, anemia, renal function) are appropriate and contextually relevant for Lima/Peru medical students.
- The 5 validity types presented (content, face, construct, predictive, criterion) match the standard taxonomy in Streiner & Norman (2024), which is in the bibliography.
