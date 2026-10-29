# Plan: Improve income.png Figure in Slide 24b

**Status:** APPROVED — Option C selected (split into two slides)
**Date:** 2026-04-11

---

## Root Cause

`income.png` is **1417 × 2268px at 72 DPI** → natural LaTeX height ≈ 2268pt.

Panel B starts at ~row 1295px from top = ~973pt from bottom.
Current `trim=0 430pt 0 0` removes only 430pt → Panel B (graph + heading) still bleeds into the crop. The `width=0.52\textwidth` also leaves the figure small and off-centre.

---

## Alternatives

### Option A — Fix trim to show Panel A only (recommended)
Properly crop to the income-measure flowchart, displayed larger.

```latex
\includegraphics[width=0.72\textwidth,
  trim=0 1000pt 0 0, clip]{../Figures/income.png}
```

**Pro:** Clean, focused on the content relevant to this lecture (variable operationalisation).
Panel A has ~1:1 aspect ratio at this crop, so `width=0.72` fills the slide nicely.
**Con:** Loses Panel B (causal-contrast diagram), but that content is out of scope here.

---

### Option B — Show full figure (both panels) with height constraint
Remove all trimming; scale by height to fit the slide.

```latex
\includegraphics[height=0.70\textheight,
  keepaspectratio]{../Figures/income.png}
```

**Pro:** Complete figure as published; no subjective cropping decision.
**Con:** Both panels together produce a tall, narrow image (aspect ~1:1.6) — each panel will be small on a 16:9 slide. Panel B adds limited pedagogical value for this lecture.

---

### Option C — Split into two slides
Slide 24b shows Panel A (Panel A crop, `trim=0 1000pt 0 0`).
New slide 24b2 shows Panel B (Panel B crop, `trim=0 0pt 0 900pt`), with a caption about causal contrast timing.

```latex
% Slide 24b — Panel A
\includegraphics[width=0.72\textwidth,
  trim=0 1000pt 0 0, clip]{../Figures/income.png}

% Slide 24b2 — Panel B
\includegraphics[width=0.72\textwidth,
  trim=0 0pt 0 900pt, clip]{../Figures/income.png}
```

**Pro:** Each panel gets full space; causal-contrast diagram could connect to the discussion of income changes over time (Igelström §4).
**Con:** Adds a 5th slide to the section; Panel B may be off-topic for this lecture's scope.

---

## Recommendation

**Option A** — clean crop to Panel A at `trim=0 1000pt 0 0, width=0.72\textwidth`. Fast, focused, visually correct.

---

## Verification (all options)

One XeLaTeX pass (no bib changes needed).

```bash
cd Slides
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```

Open PDF → confirm figure renders cleanly at target slide.
