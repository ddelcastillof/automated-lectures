# Design Spec: Operacionalización de Variables
**Date:** 2026-04-05
**Status:** APPROVED
**Session log:** `quality_reports/session_logs/2026-04-05_operacionalizacion-variables-setup.md`

---

## 1. Project Identity (CLAUDE.md updates)

| Field | Value |
|-------|-------|
| Project name | Operacionalización de Variables |
| Institution | UNMSM — Facultad de Medicina San Fernando |
| Organization | ADIECS — Semillero "ABC of Research" |
| Language | Spanish |
| Audience | Medical students, Peru |
| Branch | main |

---

## 2. Lecture Identity

| Field | Value |
|-------|-------|
| Title | Operacionalización de Variables |
| Subtitle | Cómo convertir conceptos en datos medibles |
| Duration | 30–45 min, instructor-led |
| Format | Remote (shared screen via Zoom/Meet) |
| Theoretical base | Browner et al. — *Designing Clinical Research* (5th ed., 2022), Cap. 4 |
| Beamer file | `Slides/Lecture01_Operacionalizacion.tex` |
| Quarto file | `Quarto/Lecture01_Operacionalizacion.qmd` |
| Slide count | ~24 slides |

---

## 3. Content Architecture

### Approach: Problem-First (Narrativa clínica)

Opens with a clinical question that forces students to confront the measurement problem before introducing any terminology. Concepts arrive as *solutions to a problem*, not as abstract definitions.

### Section Flow

| # | Section | Slides | Key move |
|---|---------|--------|----------|
| 0 | Portada + agenda | 2 | Orient |
| 1 | Caso clínico — el problema de medir obesidad | 3 | Hook |
| 2 | ¿Qué es una variable? ¿Qué es operacionalizar? | 3 | Define |
| 3 | Tipos de variables según escala de medición | 4 | Taxonomy |
| 4 | Precisión y exactitud | 4 | Properties |
| 5 | Confiabilidad y validez | 4 | Properties |
| 6 | Mapa de cierre — Figura Browner 4.1 | 2 | Synthesis |
| 7 | Mensajes clave + referencias | 2 | Close |

---

## 4. Slide-by-Slide Content

### Sección 0 — Portada + agenda
- **Slide 1:** Título, subtítulo, ADIECS / ABC of Research, UNMSM, fecha
- **Slide 2:** Agenda visual con 4 bloques (Caso → Conceptos → Tipos → Propiedades)

### Sección 1 — Caso clínico (3 slides)
- **Slide 3:** *"Quieres estudiar si la obesidad es un factor de riesgo para DM2 en adultos jóvenes de Lima. ¿Cómo mides obesidad?"* — lista: IMC, perímetro abdominal, % grasa corporal, presencia de acantosis nigricans
- **Slide 4:** Las mismas herramientas dan valores distintos para el mismo paciente → ¿Cuál es la "correcta"?
- **Slide 5:** Respuesta: depende de **qué** exactamente quieres medir y **para qué** → esto es operacionalizar

### Sección 2 — Conceptos (3 slides)
- **Slide 6:** ¿Qué es una **variable**? — atributo observable que varía entre individuos; ejemplos clínicos
- **Slide 7:** ¿Qué es **operacionalizar**? — definir con exactitud *cómo* vas a medir un concepto abstracto. Incluir ejemplo concreto: Appendix 4A de Browner (dinamómetro para fuerza de prensión — script verbatim, ángulo del codo, repeticiones)
- **Slide 8:** La brecha **fenómeno → medición** (adaptación de Figura 4.1 Browner). La validez del estudio depende de qué tan bien la medición representa el fenómeno de interés

### Sección 3 — Tipos de variables (4 slides)
- **Slide 9:** Dos familias: **categóricas** vs **numéricas** (diagrama árbol simple)
- **Slide 10:** Categóricas — dicotómica (vivo/muerto), nominal (tipo de sangre, identidad de género), ordinal (dolor: ninguno/leve/moderado/severo)
- **Slide 11:** Numéricas — continua (hemoglobina, IMC), discreta/conteo (número de gestaciones, número de parejas sexuales)
- **Slide 12:** **Regla de oro** (de Tabla 4.1 Browner): jerarquía de poder estadístico — continua > discreta > ordinal > nominal/dicotómica. *"No conviertas IMC en obeso/no obeso si puedes quedarte con el número"*

### Sección 4 — Precisión y exactitud (4 slides)
- **Slide 13:** Retomar caso obesidad → ¿Por qué dos médicos que usan la misma balanza obtienen valores distintos? → introduce **error aleatorio**
- **Slide 14:** **Precisión** = reproducibilidad. 3 fuentes de error aleatorio: observador, instrumento, participante. Sinónimos: reproducibilidad, confiabilidad, consistencia
- **Slide 15:** **Exactitud** = qué tan cerca del valor verdadero. Introduce **sesgo** (error sistemático). Mismas 3 fuentes. Gold standard
- **Slide 16:** **Figura TikZ — las 4 dianas** (2×2): Alta/baja precisión × Alta/baja exactitud. Diagrama original creado en TikZ con paleta del tema

### Sección 5 — Confiabilidad y validez (4 slides)
- **Slide 17:** **Confiabilidad** en la práctica — dos médicos que examinan el mismo paciente: ¿llegan al mismo diagnóstico? Introduce Kappa de Cohen *conceptualmente* (sin fórmula). Tabla 4.3 de Browner simplificada
- **Slide 18:** **Validez** = dimensión cualitativa de la exactitud. Creatinina vs cistatina C — ambas precisas para medir función renal, pero ¿cuál representa mejor el fenómeno?
- **Slide 19:** 5 tipos de validez — una línea por tipo con ejemplo clínico mínimo: contenido, apariencia, constructo, predictiva, de criterio
- **Slide 20:** El **estándar de oro** (*gold standard*) — cómo se usa para evaluar exactitud y validez; cuándo no existe (variables subjetivas como dolor, calidad de vida)

### Sección 6 — Mapa de cierre (2 slides)
- **Slide 21:** Figura 4.1 de Browner completa — *"ahora que conoces los conceptos, ¿puedes leer este diagrama?"* — síntesis visual
- **Slide 22:** Vuelta al caso: *"¿Cómo medirías obesidad ahora?"* — resolución con los conceptos aprendidos. Bonus: ejercicio 1 de Appendix 4B como actividad interactiva de 3 min (opcional según tiempo disponible)

### Sección 7 — Cierre (2 slides)
- **Slide 23:** 5 mensajes clave (adaptados del Summary p.49 de Browner)
- **Slide 24:** Bibliografía + QR o URL a slides en GitHub Pages

---

## 5. Figures to Create (TikZ)

### Figure 1: Las 4 dianas (Slide 16)
- **Layout:** 2×2 grid of bullseye targets
- **Panels:**
  - ↖ Alta precisión, alta exactitud → puntos agrupados al centro
  - ↗ Alta precisión, baja exactitud → puntos agrupados pero desplazados (sesgo)
  - ↙ Baja precisión, alta exactitud → puntos dispersos alrededor del centro
  - ↘ Baja precisión, baja exactitud → puntos dispersos y desplazados
- **Colors:** target rings in `#ECF0F1` / `#BDC3C7`, dots in `#1A7A8A` (teal)
- **Labels:** bold headers per panel, check/cross icons for precision/exactitud

### Figure 2: Fenómeno → Medición (Slide 8)
- **Layout:** simple flow arrow diagram
- **Boxes:** "Fenómeno de interés" → (brecha) → "Medición en el estudio"
- **Style:** consistent with theme colors, minimal

---

## 6. Visual Theme

### Beamer Setup
- **Base theme:** `metropolis`
- **XeLaTeX** (as per project convention)
- **Font:** Fira Sans (included with metropolis)

### Color Palette

| Role | Name | Hex |
|------|------|-----|
| Primary | Slate blue-gray | `#2C3E50` |
| Accent | Soft teal | `#1A7A8A` |
| Background | Off-white | `#FAFAFA` |
| Surface | Light gray | `#ECF0F1` |
| Text | Dark gray | `#2D2D2D` |

### Custom Beamer Environments

| Environment | Visual style | Use |
|------------|-------------|-----|
| `definicion` | Teal left border, light gray bg | Formal definitions (Slides 6, 7, 8) |
| `caso` | Amber/cream bg, stethoscope icon | Clinical scenarios (Slides 3–5, 22) |
| `clave` | Dark teal bg, white text | Key messages (Slide 23) |
| `nota` | Reduced font, gray | Secondary information |

---

## 7. Bibliography

All entries in `Bibliography_base.bib`:

| Key | Reference | Used in |
|-----|-----------|---------|
| `Browner2022-yv` | Browner et al., *Designing Clinical Research*, 5th ed. 2022 | Primary source throughout |
| `Streiner2024-my` | Streiner, Norman & Cairney, *Health Measurement Scales*, 6th ed. 2024 | Slide 19 (types of validity), Slide 23 |
| `Bland1986-di` | Bland & Altman, *Lancet* 1986 | Slide 14 (precision/reliability) |

---

## 8. Files to Create / Modify

| File | Action | Notes |
|------|--------|-------|
| `CLAUDE.md` | Update | Fill project identity placeholders |
| `Preambles/header.tex` | Create | metropolis theme + colors + custom environments |
| `Slides/Lecture01_Operacionalizacion.tex` | Create | Main Beamer source (~24 slides) |
| `Quarto/Lecture01_Operacionalizacion.qmd` | Create | Derived from Beamer after compilation |
| `Quarto/_quarto.yml` | Create | Quarto project config (does not exist yet) |
| `Quarto/theme-template.scss` | Adapt | Already exists — update with project colors |
| `Figures/tikz_dianas.tex` | Create | TikZ source for the 4-targets figure |
| `Figures/tikz_fenomeno_medicion.tex` | Create | TikZ source for the flow diagram |

---

## 9. Verification Steps

1. `xelatex` compiles without errors (3-pass + bibtex)
2. All 24 slides render correctly — no overflow, no missing refs
3. TikZ figures render at correct size in slide
4. Quarto renders to HTML with RevealJS
5. GitHub Pages deploy via `./scripts/sync_to_docs.sh Lecture01`
6. Quality score ≥ 80/100

---

## 10. Out of Scope (for this lecture)

- Strategies for enhancing precision/accuracy (Tables 4.2 and 4.4) — too operational for 30 min intro
- Measurements on stored materials (Table 4.5) — not relevant at this level
- Statistical formulas (kappa, ICC, CV) — conceptual intro only
- Other lectures in the series (will connect after series order is known)
