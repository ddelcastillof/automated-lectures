# Content Parity Report: Lecture01_Operacionalizacion (.qmd vs .tex)
**Agent:** parity-reviewer
**Date:** 2026-04-05
**Files:** Quarto/Lecture01_Operacionalizacion.qmd vs Slides/Lecture01_Operacionalizacion.tex

---

## Summary

The .qmd is a faithful structural translation of the .tex. 2 medium content drifts identified where the Beamer source carries pedagogically important material absent from the Quarto version.

---

## Frame Count

| Format | Slides (approx.) | Notes |
|--------|-----------------|-------|
| .tex | 24 slides | Title + 22 content + 1 References |
| .qmd | ~30 rendered frames | 22 `##` slides + 7 `#` section breaks (auto-rendered) + title + references |

Content coverage is equivalent. The additional rendered frames in .qmd are section break slides generated automatically from `#` headings.

---

## Parity Issues

### MEDIUM (2)

**PM1 — "Tipos de validez" table: examples missing in .qmd**

In `.tex` (slide 19), the second column includes parenthetical examples:
- "De contenido: ¿La medida cubre todos los aspectos? (SF-36 para calidad de vida)"
- "De apariencia: ¿parece razonable? (fragilidad = debilidad + fatiga + pérdida de peso)"
- "De constructo: (aislamiento social separa a quienes tienen pocas amistades)"
- "Predictiva: (fragilidad predice institucionalización)"
- "De criterio: (nueva prueba de masa muscular vs. fuerza de prensión)"

The `.qmd` version shows only the type and question, omitting all examples. These examples are essential for making abstract validity types memorable and clinically grounded.

*Recommendation:* Restore the parenthetical examples to the .qmd Tipos de validez table.

**PM2 — "El estándar de oro" nota box missing in .qmd**

The `.tex` (slide 20) ends with a `\begin{nota}` box:
> "Elegir el gold standard puede ser difícil y requiere consenso de expertos y revisión de la literatura."

This is absent from the .qmd slide. It is a pedagogically important caveat that prevents students from thinking gold standards are always obvious.

*Recommendation:* Add a `::: {.nota}` block to the .qmd gold standard slide with equivalent text.

### LOW (4)

**PL1 — Precisión slide: "porcentaje de acuerdo" omitted in .qmd**
The .tex lists "porcentaje de acuerdo, Kappa de Cohen, CCI." The .qmd omits "porcentaje de acuerdo." Minor but creates asymmetry with the nota on that slide which explains why % agreement alone is misleading.

**PL2 — Browner quotation: one sentence truncated in .qmd**
The .tex includes "Repita el procedimiento para el brazo izquierdo." The .qmd omits this. Low impact on understanding.

**PL3 — "La respuesta" slide: definition label absent in .qmd**
The Beamer `.definicion[Operacionalizar]` environment displays "Operacionalizar" as the box header. The .qmd `.definicion` block has no visible label. The CSS class does not render a title. Students reading the .qmd version may not immediately identify this as the definition of operationalization.

**PL4 — "El mapa completo" sub-label: "Escala de medición" omitted in .qmd**
The .tex sub-label reads "Precisión · Exactitud · Validez\nEscala de medición." The .qmd HTML version includes only "Precisión · Exactitud · Validez" in a slightly different format. Low impact.

---

## Structural Consistency
- All section titles match between .tex and .qmd
- All clinical cases translated correctly
- All table structures preserved (with PM1 exception)
- Color palette consistent (though see SCSS color conflict in visual audit)
- No frames in .tex without equivalent in .qmd, and vice versa
