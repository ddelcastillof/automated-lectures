# Plan: Worked Example — Operacionalización del Ingreso

**Status:** DRAFT
**Date:** 2026-04-11
**Branch:** main

---

## Context

The user wants to add a worked example at the **end of the seminar** (after the "Mensajes clave" section, before "Referencias") showing how different income operationalizations can impact the research pipeline. The example should mirror the pattern already established with the obesity/DM2 case (Section 1) and explicitly connect to every core concept taught during the lecture.

Source material: Igelström et al. (2024), *BMC Public Health* 24:1572 — a taxonomy paper showing that "income" is not a single definable construct and that different definitions lead to substantially different causal estimates.

Figure available: `Figures/income.png` — Fig. 1 from Igelström, showing Panel A (income measure taxonomy flowchart) and Panel B (causal contrast timeline).

---

## Files to Modify

| File | Change |
|------|--------|
| `Bibliography_base.bib` | Add Igelström 2024 entry (`Igelstrom2024-bq`) |
| `Slides/Lecture01_Operacionalizacion.tex` | Insert new section + 4 slides + update `\nocite` |

---

## Slide Design (4 slides, new Section 7)

Insert between the existing Slide 23b ("Mensajes clave 2/2") and Slide 24 ("Referencias").

### Section header
```
\section{Ejemplo integrador: el ingreso}
```

### Slide A — "¿Cómo mides ingreso?" (`caso` environment)
Mirror the obesity case opener (Slide 3). Case: researcher wants to study the effect of **income on health** in Lima. Ask: ¿qué variable mides?

List the candidate operationalizations in two columns:
- Ingreso bruto / ingreso neto
- Ingreso disponible / ingreso equivalizado del hogar
- Quintil de ingreso / estado de pobreza (dicotómica)

### Slide B — "La taxonomía del ingreso" (figure slide)
Include `Figures/income.png` (Panel A only, cropped via `trim` and `clip`).
Caption: Adaptado de Igelström et al. (2024), Fig. 1. Connect to the fenómeno → medición diagram.

### Slide C — "Mismo hogar, distintos resultados" (table slide)
Show a small numeric table:

> Hogar con 2 adultos + 2 niños (<13 años), ingresos totales S/ 3,000/mes

| Operacionalización | Valor | Tipo de variable |
|--------------------|-------|-----------------|
| Ingreso bruto (individual) | S/ 1,500 | Continua |
| Ingreso neto (tras impuestos) | S/ 1,350 | Continua |
| Ingreso disponible | ~S/ 900 | Continua |
| Ingreso equivalizado (OCDE) | S/ 1,429 | Continua |
| Quintil de ingreso | 2.º quintil | Ordinal |
| Estado de pobreza | Sí / No | Dicotómica |

Cite Igelström et al. (2024). Connect to the "regla de oro: prefiere continuas" slide.

### Slide D — "¿Qué nos enseña este caso?" (`clave` environment)
Key messages:
1. La operacionalización del ingreso **cambia la pregunta causal**, no sólo la medición.
2. Cada elección en la cadena (fuente → ajuste → unidad → comparación) afecta precisión, exactitud y validez.
3. Conectar explícitamente al **mapa del estudio** (pipeline diagram, Slide 2b): la elección en "Diseño de mediciones" determina la inferencia.

Citation: Igelström et al. (2024).

---

## Bibliography Entry

```bibtex
@Article{Igelstrom2024-bq,
  author    = {Igelström, Erik and Kopasker, Daniel and Craig, Peter and
               Lewsey, Jim and Katikireddi, Srinivasa Vittal},
  title     = {Estimating the causal effects of income on health:
               how researchers' definitions of {``income''} matter},
  journal   = {BMC Public Health},
  year      = {2024},
  volume    = {24},
  number    = {1},
  pages     = {1572},
  doi       = {10.1186/s12889-024-19049-w},
}
```

---

## Update `\nocite`

Change:
```latex
\nocite{Browner2022-yv, Streiner2024-my, Bland1986-di}
```
To:
```latex
\nocite{Browner2022-yv, Streiner2024-my, Bland1986-di, Igelstrom2024-bq}
```

---

## Connections to Existing Slides

| New content | Connects to |
|-------------|-------------|
| "¿Cómo mides ingreso?" opener | Slide 3 (obesity case) — same rhetorical pattern |
| Income taxonomy figure | Slide 6 (fenómeno → medición TikZ) — same concept |
| Numeric table (bruto → dicotómica) | Slide 12 (regla de oro: continuas > categóricas) |
| Clave: operacionalización cambia la pregunta | Slide 5 (definición de operacionalizar) |
| Pipeline reference in closing | Slide 2b + Slide 21 (advance organizer / mapa completo) |

---

## Verification

```bash
cd Slides
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
BIBINPUTS=..:$BIBINPUTS bibtex Lecture01_Operacionalizacion
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```

Check: 4 new slides appear after "Mensajes clave", figure renders, Igelström citation appears in references.
