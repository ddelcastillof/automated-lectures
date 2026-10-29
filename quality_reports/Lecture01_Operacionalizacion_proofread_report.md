# Proofreading Report: Lecture01_Operacionalizacion.tex
**Date:** 2026-04-05
**Reviewer:** Proofreader Agent

---

## Summary
- **Total issues: 21**
- Grammar: 2 | Typos: 1 | Overflow: 9 | Consistency: 4 | Academic Quality: 5

---

## Issues by Category

### GRAMMAR

| # | Line / Frame | Current Text | Proposed Fix | Severity |
|---|---|---|---|---|
| G1 | Line 490 / Slide 17 "Confiabilidad en la práctica" | `¿Qué tan seguido coinciden?` | `¿Con qué frecuencia coinciden?` | Medium |
| G2 | Line 530 / Slide 18 "Validez" | `Un paciente con poca masa puede tener insuficiencia renal crónica (IRC) con creatinina normal.` | `Un paciente con poca masa muscular puede tener insuficiencia renal crónica (IRC) con creatinina sérica normal.` | Low |

**G1 Notes:** "Qué tan seguido" is a colloquial regionalism (predominantly Mexican and Central American usage) that is out of register for a formal academic lecture at a Peruvian medical school. "Con qué frecuencia" is neutral standard Spanish and more appropriate for this audience and register.

**G2 Notes:** "poca masa" is ambiguous without the noun it modifies ("muscular") explicitly stated; and "creatinina normal" lacks the qualifier "sérica" which is implied but not explicit — important in a clinical context where "creatinina" can also refer to urine creatinine.

---

### TYPOS

| # | Line / Frame | Current Text | Proposed Fix | Severity |
|---|---|---|---|---|
| T1 | Line 91 / Slide 4 "El problema" | `Resistencia a insulina` | `Resistencia a la insulina` | Medium |

**T1 Notes:** In Spanish, a definite article is required before "insulina" in this context: "resistencia a la insulina" is the standard clinical and biochemical term. The omission of "la" reads as a typo or anglicism ("insulin resistance" → missing article).

---

### OVERFLOW

All overflow warnings are taken directly from the `.log` file.

| # | Type | Magnitude | Frame / Slide | Severity |
|---|---|---|---|---|
| O1 | `\vbox` | 16.67 pt too high | Slide 1 — Title frame (`\maketitle`) | Low |
| O2 | `\hbox` | 0.51 pt too wide | Slide 9 — "Dos grandes familias" (TikZ tree, node "Dicotómica") | Low |
| O3 | `\vbox` | 31.39 pt too high | Slide 16 — "Precisión vs. exactitud: las 4 dianas" | Medium |
| O4 | `\vbox` | 3.91 pt too high | Slide 17 — "Confiabilidad en la práctica" | Low |
| O5 | `\vbox` | 20.35 pt too high | Slide 18 — "Validez" | Medium |
| O6 | `\vbox` | 40.31 pt too high | Slide 20 — "El estándar de oro" | **High** |
| O7 | `\hbox` | 18.84 pt too wide | Slide 21 — "El mapa completo" (TikZ flow diagram) | Medium |
| O8 | `\vbox` | 50.94 pt too high | Slide 22 — "¿Cómo medirías obesidad ahora?" | **High** |
| O9 | `\vbox` | 71.07 pt too high | Slide 23 — "Mensajes clave" | **High** |

**O1:** Minor vbox overflow on title frame; caused by progress bar + institute block. Generally acceptable.

**O2:** Sub-millimeter hbox overflow; "Dicotómica" protrudes 0.51 pt in TikZ tree node. Barely visible.

**O3:** The 4-target TikZ diagram (scale=0.82) overflows by ~31 pt. Consider reducing `scale` to `0.72`.

**O5:** Slide 18 "Validez" overflows by 20 pt. The left column's long sentence (creatinine/muscle mass limitation) pushes beyond the frame. Consider splitting or shortening.

**O6:** Slide 20 "El estándar de oro" overflows by 40 pt. Frame contains `definicion` box + `columns` + `nota` box — too much content. Remove `\vspace{8pt}` before `nota`, or reduce column text.

**O7:** TikZ flow diagram on Slide 21 has an 18.84 pt hbox overflow. The rightmost node ("Inferencia sobre el fenómeno") likely extends beyond slide width. Reduce `node distance` or use `\resizebox`.

**O8:** Slide 22 overflows by 51 pt. The long parenthetical `(absorciometría de rayos X de energía dual, DEXA)` in the `p{7.0cm}` table column is the primary cause. Abbreviate to `(DEXA)` in the table.

**O9:** Slide 23 "Mensajes clave" overflows by 71 pt — largest overflow in the deck. The 5-item list inside the `clave` tcolorbox exceeds the frame. Items 4–5 will be cut off when projected.

---

### CONSISTENCY

| # | Lines / Frames | Issue | Current Text | Proposed Fix | Severity |
|---|---|---|---|---|---|
| C1 | Lines 57 vs 638 | "diabetes tipo 2" vs "DM2" — abbreviation introduced without expansion | Line 638: `DM2` without prior expansion | Introduce `diabetes mellitus tipo 2 (DM2)` at line 57 (Slide 3), then `DM2` is fine on Slide 22 | Medium |
| C2 | Lines 155, 204, 313, 476 | In-text Browner references use two formats: bare "Browner" vs "Browner et al. (2022)" | `(Browner, Apéndice 4A)` vs `Browner et al. (2022), Figura 4.1` | Standardize to `Browner et al. (2022)` or use `\citet{Browner2022-yv}` with locator | Medium |
| C3 | Lines 402, 569 vs 591 | "gold standard" italicized in two places, plain text in one | Lines 402, 569: `\textit{gold standard}` / Line 591: `gold standard` | Apply `\textit{gold standard}` at line 591 | Low |
| C4 | Lines 379 vs 497 | Kappa symbol $\kappa$ introduced at Slide 17 but referenced at Slide 14 without symbol | Slide 14: `Kappa de Cohen` / Slide 17: `Kappa de Cohen ($\kappa$)` | Add `($\kappa$)` at first mention on Slide 14, line 379 | Low |

---

### ACADEMIC QUALITY

| # | Line / Frame | Issue | Current Text | Proposed Fix | Severity |
|---|---|---|---|---|---|
| AQ1 | Line 104 / Slide 5 | `definicion` box used for a non-definition | `Depende de qué exactamente quieres medir y para qué.` | Rewrite as a proper definition or change box type to `nota` | Medium |
| AQ2 | Line 278 / Slide 10 | Oversimplified power hierarchy notation | `dicotómica $\approx$ nominal $<$ ordinal` | `nominal/dicotómica $<$ ordinal` (remove ≈ or add clarifying footnote) | Low |
| AQ3 | Line 652 / Slide 22 | Long parenthetical in table cell causes overflow and is hard to read | `(absorciometría de rayos X de energía dual, DEXA)` | Shorten to `(DEXA)` in the table; add full name in a `nota` box below | Medium |
| AQ4 | Line 591 / Slide 20 | "gold standard" without italics in body text | `gold standard` | `\textit{gold standard}` or use `estándar de oro` | Low |
| AQ5 | Lines 204, 476 / Slides 8, 16 | Figure captions use prose attribution instead of `\cite` | `Adaptado de Browner et al. (2022), Figura 4.1` | `Adaptado de \citet{Browner2022-yv}, Figura 4.1` | Low |

---

## Critical Issues (must fix before teaching)

### O6 — Slide 20 "El estándar de oro": +40 pt overflow
Part of the slide content (the `nota` box) will be clipped or hidden when projected. **Fix:** Remove `\vspace{8pt}` before `nota`, reduce column text, or move `nota` to a new slide.

### O8 — Slide 22 "¿Cómo medirías obesidad ahora?": +51 pt overflow
The summary table overflows. The DEXA parenthetical is the primary cause. **Fix:** Abbreviate table cell to `(DEXA)` and add expansion in a note below the table.

### O9 — Slide 23 "Mensajes clave": +71 pt overflow — CRITICAL
Items 4–5 will be cut off when the slide is projected. **Fix:** Split into two slides ("Mensajes clave 1/2" and "2/2"), or reduce to 4 items.

---

*Report generated by Proofreader Agent on 2026-04-05. Source files were not modified.*
