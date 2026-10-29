# Visual Audit: Lecture01_Operacionalizacion.qmd
**Agent:** slide-auditor
**Date:** 2026-04-05
**File:** Quarto/Lecture01_Operacionalizacion.qmd

---

## Summary

No catastrophic overflows detected. Several medium and low issues related to font legibility at projection distance, SCSS color system inconsistency, and one dense slide.

---

## Issues Found

### CRITICAL (0)
None.

### MEDIUM (3)

**M1 — SCSS color conflict (theme-template.scss lines 6–12 vs 73–82)**
The file defines `$accent: #1A7A8A` at line 9, then redefines `$accent: $primary-blue` (= `#012169`) at line 82 inside the `/*-- scss:rules --*/` block. The custom div rules (`.definicion`, `.caso`, `.clave`, `.nota`) are defined between lines 30–61 using the first `$accent` value. Post-redefinition, any SCSS that references `$accent` will use the Emory blue. This creates a split color system. The `.definicion` border and `.clave` background will render in `#1A7A8A` (teal), but heading elements and other theme components using `$accent` after the redefinition will render in `#012169` (deep blue). This inconsistency may be intentional (hybrid theme) but is undocumented and fragile.
*Recommendation:* Rename the first block's accent to `$accent-adiecs: #1A7A8A` or place all ADIECS custom div rules after the `$accent` override so both use the same color.

**M2 — Mensajes clave slide: potential overflow**
The `.clave` box contains 5 numbered items, each multi-sentence. At the default `font-size: 0.88em` and standard padding, this may overflow the slide boundary on some viewports. The `.tex` version uses the `clave` Beamer environment, which handles pagination gracefully. The Quarto version has no escape valve.
*Recommendation:* Break into two slides, or use `.smaller` wrapper, or reduce to 5 one-sentence bullets with key terms bolded.

**M3 — 4-diana SVG labels: legibility at projection**
The inline SVG target diagrams use `font-size: 0.72em` for labels. At typical projector resolution and viewing distance (5–10 meters), this is likely below readable threshold. The labels ("Alta precisión, alta exactitud" etc.) carry essential pedagogical meaning.
*Recommendation:* Increase to at minimum `0.85em`, or replace the inline SVG with a proper figure image that can scale.

### LOW (4)

**L1 — `.nota` opacity: 0.75**
The `.nota` CSS class sets `opacity: 0.75`. On bright projector backgrounds, this may render as grey-on-white, potentially unreadable. The `.tex` equivalent uses standard text color.
*Recommendation:* Remove opacity and use a lighter color value (e.g., `color: #555`) instead.

**L2 — Three-column slide "Variables categóricas": narrow columns**
At 33% width each, the third column "Ordinal — Con orden; intervalos no cuantificables" will wrap. Not a critical issue but may look cramped. The `.tex` uses `0.32\textwidth` which is similar, but Beamer handles line-breaking differently.

**L3 — 4-diana TikZ dividing lines invisible**
`color=bglight` for the cross-hairs in the precision/accuracy diagram renders the dividers near-invisible. Use `color=primary!30` or `color=gray!40`.

**L4 — HTML flow diagram: arrow character legibility**
The `→` arrow in the "La brecha fenómeno → medición" HTML slide uses a plain `→` character at `font-size:1.4em`. This is fine but a styled SVG arrow would scale better.

---

## Font/Color Consistency
- Primary content font: inherits from theme (Source Sans Pro / Fira Sans split — see SCSS M1 above)
- Box environments use two different accent colors due to SCSS conflict
- Heading border-bottom correctly uses `rgba($primary-gold, 0.3)` — not affected by the conflict

## Spacing Assessment
- Most slides have adequate breathing room
- "¿Qué es operacionalizar?" slide is the densest (definition + long quotation) but fits at current font size
