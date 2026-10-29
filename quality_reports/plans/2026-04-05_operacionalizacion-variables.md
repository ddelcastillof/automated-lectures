# Operacionalización de Variables — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a complete 24-slide Beamer + Quarto lecture deck on "Operacionalización de Variables" for ADIECS ABC of Research semillero at UNMSM, deployable to GitHub Pages.

**Architecture:** Beamer `.tex` is the authoritative source (XeLaTeX, metropolis theme); Quarto `.qmd` derives from it for web deployment. Two TikZ figures are created inline. All content is in Spanish, pitched at introductory medical students using a problem-first narrative structure.

**Tech Stack:** XeLaTeX + metropolis + tcolorbox + TikZ + biblatex/bibtex | Quarto RevealJS | GitHub Pages

**Design spec:** `quality_reports/specs/2026-04-05_operacionalizacion-variables-design.md`

---

## File Map

| File | Action | Responsibility |
|------|--------|---------------|
| `CLAUDE.md` | Modify | Fill project identity placeholders |
| `Preambles/header.tex` | Create | Theme, colors, fonts, custom environments |
| `Slides/Lecture01_Operacionalizacion.tex` | Create | Full Beamer source (24 slides) |
| `Quarto/_quarto.yml` | Create | Quarto project config |
| `Quarto/theme-template.scss` | Modify | Project colors for RevealJS |
| `Quarto/Lecture01_Operacionalizacion.qmd` | Create | RevealJS version derived from Beamer |

TikZ figures are embedded inline in the `.tex` file (not separate files).

---

## Task 1: Update CLAUDE.md with project identity

**Files:**
- Modify: `CLAUDE.md`

- [ ] **Step 1.1: Replace project name and institution**

Replace the placeholder header block:
```markdown
**Project:** [YOUR PROJECT NAME]
**Institution:** [YOUR INSTITUTION]
**Branch:** main
```
With:
```markdown
**Project:** Operacionalización de Variables — ADIECS ABC of Research
**Institution:** UNMSM — Facultad de Medicina San Fernando
**Branch:** main
```

- [ ] **Step 1.2: Update Current Project State table**

Replace:
```markdown
| 1: [Topic] | `Lecture01_Topic.tex` | `Lecture1_Topic.qmd` | [Brief description] |
| 2: [Topic] | `Lecture02_Topic.tex` | -- | [Brief description] |
```
With:
```markdown
| 1: Operacionalización de Variables | `Lecture01_Operacionalizacion.tex` | `Lecture01_Operacionalizacion.qmd` | Variable types, precision, accuracy, validity — Browner Ch. 4 |
```

- [ ] **Step 1.3: Update Beamer Environments table**

Replace the placeholder row and example comments with:
```markdown
| `definicion` | Teal left border, light gray bg | Formal definitions |
| `caso` | Cream background | Clinical scenarios |
| `clave` | Dark teal bg, white text | Key messages |
| `nota` | Reduced font, gray text | Secondary information |
```

- [ ] **Step 1.4: Update Quarto CSS Classes table**

Replace the placeholder row with:
```markdown
| `.definicion` | Teal left border box | Definitions in RevealJS |
| `.caso` | Cream background box | Clinical scenarios |
| `.clave` | Dark teal bg, white text | Key messages |
```

- [ ] **Step 1.5: Commit**
```bash
git add CLAUDE.md
git commit -m "chore: update CLAUDE.md with project identity (ADIECS ABC of Research)"
```

---

## Task 2: Create Preambles/header.tex

**Files:**
- Create: `Preambles/header.tex`

- [ ] **Step 2.1: Create header.tex**

Create `Preambles/header.tex` with the full content below:

```latex
% =============================================================
% header.tex — Preamble for Operacionalización de Variables
% ADIECS ABC of Research — UNMSM San Fernando
% XeLaTeX + Metropolis
% =============================================================

% --- Theme ---------------------------------------------------
\usetheme[progressbar=frametitle, numbering=fraction]{metropolis}

% --- Fonts ---------------------------------------------------
\usepackage{fontspec}
\setsansfont{Fira Sans}[
  BoldFont = {Fira Sans Bold},
  ItalicFont = {Fira Sans Italic}
]
\setmonofont{Fira Mono}

% --- Language ------------------------------------------------
\usepackage[spanish, es-noquoting]{babel}
\usepackage{csquotes}

% --- Colors --------------------------------------------------
\usepackage{xcolor}
\definecolor{primary}{HTML}{2C3E50}    % slate blue-gray
\definecolor{accent}{HTML}{1A7A8A}     % soft teal
\definecolor{bglight}{HTML}{ECF0F1}   % light gray surface
\definecolor{offwhite}{HTML}{FAFAFA}  % background
\definecolor{textdark}{HTML}{2D2D2D}  % body text
\definecolor{casebg}{HTML}{FEF9EE}    % warm cream for caso boxes
\definecolor{amber}{HTML}{D4A017}     % amber accent for caso border

% Apply metropolis color scheme
\setbeamercolor{frametitle}{fg=white, bg=primary}
\setbeamercolor{title separator}{fg=accent}
\setbeamercolor{progress bar}{fg=accent, bg=bglight}
\setbeamercolor{normal text}{fg=textdark, bg=offwhite}
\setbeamercolor{alerted text}{fg=accent}
\setbeamercolor{example text}{fg=primary}
\setbeamercolor{block title}{fg=white, bg=accent}
\setbeamercolor{block body}{fg=textdark, bg=bglight}

% --- TikZ ----------------------------------------------------
\usepackage{tikz}
\usetikzlibrary{arrows.meta, positioning, shapes.geometric}

% --- Boxes (tcolorbox) ---------------------------------------
\usepackage{tcolorbox}
\tcbuselibrary{skins, breakable}

% definicion: teal left-rule box
\newtcolorbox{definicion}[1][]{
  enhanced,
  colback=bglight,
  colframe=accent,
  leftrule=4pt,
  toprule=0pt,
  bottomrule=0pt,
  rightrule=0pt,
  arc=0pt,
  boxsep=4pt,
  left=6pt,
  title={\textbf{\textcolor{accent}{#1}}},
  detach title,
  before upper={\tcbtitle\par\smallskip},
  fontupper=\small,
}

% caso: warm cream box for clinical scenarios
\newtcolorbox{caso}[1][Caso clínico]{
  enhanced,
  colback=casebg,
  colframe=amber,
  leftrule=4pt,
  toprule=0.5pt,
  bottomrule=0.5pt,
  rightrule=0.5pt,
  arc=2pt,
  boxsep=4pt,
  left=6pt,
  title={\textbf{\textcolor{amber}{#1}}},
  detach title,
  before upper={\tcbtitle\par\smallskip},
  fontupper=\small,
}

% clave: dark teal bg, white text
\newtcolorbox{clave}[1][Mensaje clave]{
  enhanced,
  colback=accent,
  colframe=accent,
  colupper=white,
  arc=2pt,
  boxsep=4pt,
  left=6pt,
  title={\textbf{\textcolor{white}{#1}}},
  detach title,
  before upper={\tcbtitle\par\smallskip},
  fontupper=\small\color{white},
}

% nota: subtle gray smaller text
\newtcolorbox{nota}[1][Nota]{
  enhanced,
  colback=bglight,
  colframe=bglight,
  arc=2pt,
  boxsep=2pt,
  fontupper=\footnotesize\color{textdark!70},
}

% --- Bibliography -------------------------------------------
\usepackage[backend=bibtex, style=numeric, sorting=none]{biblatex}
\addbibresource{../Bibliography_base.bib}

% --- Hyperlinks ---------------------------------------------
\usepackage{hyperref}
\hypersetup{colorlinks=true, linkcolor=accent, urlcolor=accent}

% --- Misc ---------------------------------------------------
\usepackage{booktabs}
\usepackage{graphicx}
\usepackage{microtype}
```

- [ ] **Step 2.2: Commit**
```bash
git add Preambles/header.tex
git commit -m "feat: add Beamer preamble (metropolis, teal palette, custom environments)"
```

---

## Task 3: Create Beamer skeleton (compiles clean)

**Files:**
- Create: `Slides/Lecture01_Operacionalizacion.tex`

Goal: a minimal file that compiles without errors before any content is added.

- [ ] **Step 3.1: Create the skeleton file**

Create `Slides/Lecture01_Operacionalizacion.tex`:

```latex
\documentclass[aspectratio=169, 12pt, xcolor=table]{beamer}
\input{../Preambles/header}

% ============================================================
% Metadata
% ============================================================
\title{Operacionalización de Variables}
\subtitle{Cómo convertir conceptos en datos medibles}
\author{} % Fill in presenter name
\institute{%
  ADIECS --- Semillero ``ABC of Research''\\
  UNMSM --- Facultad de Medicina San Fernando
}
\date{2026}

% ============================================================
\begin{document}
% ============================================================

\maketitle

% PLACEHOLDER — content tasks will fill this in
\begin{frame}{En construcción}
  Contenido próximamente.
\end{frame}

\end{document}
```

- [ ] **Step 3.2: Compile (verify skeleton builds)**
```bash
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: exit 0, PDF generated, no fatal errors. Warnings about missing fonts or undefined references are OK at this stage.

- [ ] **Step 3.3: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: add Beamer skeleton (compiles clean)"
```

---

## Task 4: Add Sección 0 — Portada y agenda (Slides 1–2)

**Files:**
- Modify: `Slides/Lecture01_Operacionalizacion.tex`

- [ ] **Step 4.1: Replace placeholder frame with Sección 0**

Replace the `\begin{frame}{En construcción}` block with:

```latex
% ============================================================
% SECCIÓN 0: Portada + Agenda
% ============================================================

% Slide 1: Title — generated by \maketitle above

% Slide 2: Agenda
\begin{frame}{Agenda}
  \begin{columns}[T]
    \begin{column}{0.48\textwidth}
      \textbf{\textcolor{accent}{1.}} Caso clínico\\[4pt]
      \textbf{\textcolor{accent}{2.}} ¿Qué es operacionalizar?
    \end{column}
    \begin{column}{0.48\textwidth}
      \textbf{\textcolor{accent}{3.}} Tipos de variables\\[4pt]
      \textbf{\textcolor{accent}{4.}} Precisión, exactitud y validez
    \end{column}
  \end{columns}
\end{frame}
```

- [ ] **Step 4.2: Compile and verify**
```bash
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: 2 slides in PDF (title + agenda), no errors.

- [ ] **Step 4.3: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: add portada and agenda slides"
```

---

## Task 5: Add Sección 1 — Caso clínico (Slides 3–5)

**Files:**
- Modify: `Slides/Lecture01_Operacionalizacion.tex`

- [ ] **Step 5.1: Add section heading and Slides 3–5 after the agenda frame**

```latex
% ============================================================
% SECCIÓN 1: Caso clínico
% ============================================================
\section{El problema de medir}

% Slide 3
\begin{frame}{¿Cómo mides obesidad?}
  \begin{caso}[Caso clínico]
    Quieres estudiar si la \textbf{obesidad} es un factor de riesgo
    para diabetes tipo~2 en adultos jóvenes de Lima.\\[6pt]
    \textit{¿Qué variable mides?}
  \end{caso}

  \vspace{8pt}
  \begin{columns}[T]
    \begin{column}{0.48\textwidth}
      \begin{itemize}
        \item Índice de masa corporal (IMC)
        \item Perímetro abdominal
      \end{itemize}
    \end{column}
    \begin{column}{0.48\textwidth}
      \begin{itemize}
        \item Porcentaje de grasa corporal
        \item Presencia de acantosis nigricans
      \end{itemize}
    \end{column}
  \end{columns}
\end{frame}

% Slide 4
\begin{frame}{El problema}
  Las cuatro medidas aplicadas al \textbf{mismo paciente} dan resultados distintos.

  \vspace{10pt}
  \begin{center}
    \begin{tabular}{lcc}
      \toprule
      \textbf{Medida} & \textbf{Valor} & \textbf{Clasificación} \\
      \midrule
      IMC             & 28.4 kg/m²    & Sobrepeso \\
      Perímetro abd.  & 94 cm         & Riesgo aumentado \\
      \% grasa corp.  & 34\%          & Obesidad \\
      Acantosis       & Presente      & Resistencia a insulina \\
      \bottomrule
    \end{tabular}
  \end{center}

  \vspace{8pt}
  \begin{center}
    \textcolor{accent}{\textbf{¿Cuál es la «correcta»?}}
  \end{center}
\end{frame}

% Slide 5
\begin{frame}{La respuesta}
  \begin{definicion}[Operacionalizar]
    Depende de \textbf{qué} exactamente quieres medir y \textbf{para qué}.
    No hay una medida «correcta» universal: hay medidas más o menos
    adecuadas según la pregunta de investigación.
  \end{definicion}

  \vspace{8pt}
  A este proceso de definir \textit{cómo} medir un concepto abstracto
  lo llamamos \textbf{operacionalización}.
\end{frame}
```

- [ ] **Step 5.2: Compile and verify (5 slides)**
```bash
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: 5 slides, tcolorbox environments render, table renders without overflow.

- [ ] **Step 5.3: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: add caso clinico slides (obesidad DM2)"
```

---

## Task 6: Add Sección 2 — Conceptos + TikZ fenómeno→medición (Slides 6–8)

**Files:**
- Modify: `Slides/Lecture01_Operacionalizacion.tex`

- [ ] **Step 6.1: Add Sección 2 content after Sección 1 frames**

```latex
% ============================================================
% SECCIÓN 2: ¿Qué es una variable? ¿Qué es operacionalizar?
% ============================================================
\section{Conceptos fundamentales}

% Slide 6
\begin{frame}{¿Qué es una variable?}
  \begin{definicion}[Variable]
    Atributo observable que \textbf{varía} entre individuos y que
    puede ser medido o clasificado.
  \end{definicion}

  \vspace{8pt}
  \textbf{Ejemplos clínicos:}
  \begin{itemize}
    \item Edad, sexo, nivel de hemoglobina
    \item Diagnóstico de hipertensión (sí/no)
    \item Grado de dolor (ninguno / leve / moderado / severo)
    \item Número de gestaciones previas
  \end{itemize}
\end{frame}

% Slide 7
\begin{frame}{¿Qué es operacionalizar?}
  \begin{definicion}[Definición operacional]
    Especificación \textbf{exacta} de cómo se medirá un concepto abstracto:
    instrumento, unidad, punto de corte, protocolo.
  \end{definicion}

  \vspace{6pt}
  \textbf{Ejemplo (Browner, Apéndice 4A):}

  \begin{nota}
    \textit{Fuerza de prensión con dinamómetro.}
    «Coloque el dinamómetro en la mano derecha con el dial hacia la palma.
    El brazo debe estar flexionado a 90° con el antebrazo paralelo al suelo.
    Apriete tan fuerte como pueda mientras cuento hasta tres.
    Registre en kilogramos, al 0.5 kg más cercano.
    Repita el procedimiento para el brazo izquierdo.»
  \end{nota}
\end{frame}

% Slide 8 — TikZ diagram: fenómeno → medición
\begin{frame}{La brecha fenómeno → medición}
  \begin{center}
  \begin{tikzpicture}[
    node distance=1.4cm,
    box/.style={
      rectangle, rounded corners=4pt,
      draw=accent, line width=1.5pt,
      fill=bglight, text width=3.2cm,
      align=center, font=\small\bfseries,
      minimum height=1cm, inner sep=6pt
    },
    arrow/.style={-{Stealth[length=6pt]}, line width=1.5pt, color=primary}
  ]
    \node[box] (fenomeno) {Fenómeno\\de interés\\{\footnotesize(obesidad)}};
    \node[box, right=2.2cm of fenomeno] (medicion) {Medición\\en el estudio\\{\footnotesize(IMC, cm, \%)}};

    \draw[arrow] (fenomeno) -- node[above, font=\footnotesize\itshape, color=textdark]
      {operacionalización} (medicion);

    \node[below=0.5cm of fenomeno, font=\footnotesize, color=textdark, text width=3.2cm, align=center]
      {Concepto abstracto};
    \node[below=0.5cm of medicion, font=\footnotesize, color=textdark, text width=3.2cm, align=center]
      {Valor observable};

    \draw[decorate, decoration={brace, amplitude=6pt, raise=4pt},
          color=accent, line width=1pt]
      (medicion.north east) -- (fenomeno.north west)
      node[midway, above=10pt, font=\footnotesize\itshape, color=accent]
        {La validez del estudio depende de esta distancia};
  \end{tikzpicture}
  \end{center}

  \vspace{4pt}
  \begin{center}
    \footnotesize\textit{Adaptado de Browner et al. (2022), Figura 4.1}
  \end{center}
\end{frame}
```

- [ ] **Step 6.2: Compile and verify (8 slides, TikZ renders)**
```bash
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: 8 slides, TikZ arrow diagram renders on slide 8, no overflow.

- [ ] **Step 6.3: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: add conceptos section + TikZ fenomeno-medicion diagram"
```

---

## Task 7: Add Sección 3 — Tipos de variables (Slides 9–12)

**Files:**
- Modify: `Slides/Lecture01_Operacionalizacion.tex`

- [ ] **Step 7.1: Add Sección 3 after Sección 2**

```latex
% ============================================================
% SECCIÓN 3: Tipos de variables
% ============================================================
\section{Tipos de variables}

% Slide 9
\begin{frame}{Dos grandes familias}
  \begin{center}
  \begin{tikzpicture}[
    font=\small,
    box/.style={rectangle, rounded corners=3pt, draw=primary,
                fill=bglight, text width=2.6cm, align=center,
                minimum height=0.8cm, inner sep=4pt},
    root/.style={rectangle, rounded corners=3pt, draw=accent,
                 fill=accent, text=white, font=\small\bfseries,
                 text width=2.8cm, align=center,
                 minimum height=0.9cm, inner sep=4pt},
    line/.style={draw=primary, line width=1pt}
  ]
    \node[root] (var) {Variable};
    \node[box, below left=0.8cm and 1.2cm of var]  (cat) {Categórica};
    \node[box, below right=0.8cm and 1.2cm of var] (num) {Numérica};
    \draw[line] (var) -- (cat);
    \draw[line] (var) -- (num);

    \node[box, below=0.6cm of cat, text width=1.8cm, xshift=-1.2cm]
      (dic) {Dicotómica};
    \node[box, below=0.6cm of cat, text width=1.8cm]
      (nom) {Nominal};
    \node[box, below=0.6cm of cat, text width=1.8cm, xshift=1.2cm]
      (ord) {Ordinal};
    \draw[line] (cat) -- (dic);
    \draw[line] (cat) -- (nom);
    \draw[line] (cat) -- (ord);

    \node[box, below=0.6cm of num, text width=1.8cm, xshift=-0.8cm]
      (con) {Continua};
    \node[box, below=0.6cm of num, text width=1.8cm, xshift=0.8cm]
      (dis) {Discreta};
    \draw[line] (num) -- (con);
    \draw[line] (num) -- (dis);
  \end{tikzpicture}
  \end{center}
\end{frame}

% Slide 10
\begin{frame}{Variables categóricas}
  \begin{columns}[T]
    \begin{column}{0.32\textwidth}
      \textbf{\textcolor{accent}{Dicotómica}}\\[4pt]
      Dos categorías\\[4pt]
      \textit{Vivo / muerto}\\
      \textit{Embarazada / no}
    \end{column}
    \begin{column}{0.32\textwidth}
      \textbf{\textcolor{accent}{Nominal}}\\[4pt]
      Categorías sin orden\\[4pt]
      \textit{Tipo de sangre}\\
      \textit{Identidad de género}
    \end{column}
    \begin{column}{0.32\textwidth}
      \textbf{\textcolor{accent}{Ordinal}}\\[4pt]
      Categorías con orden; intervalos no cuantificables\\[4pt]
      \textit{Dolor: ninguno /}\\
      \textit{leve / moderado / severo}
    \end{column}
  \end{columns}

  \vspace{8pt}
  \begin{nota}
    Poder estadístico: dicotómica ≈ nominal $<$ ordinal
  \end{nota}
\end{frame}

% Slide 11
\begin{frame}{Variables numéricas}
  \begin{columns}[T]
    \begin{column}{0.48\textwidth}
      \textbf{\textcolor{accent}{Continua}}\\[4pt]
      Infinitos valores posibles en una escala\\[6pt]
      \begin{itemize}
        \item Hemoglobina (g/dL)
        \item Presión arterial (mmHg)
        \item IMC (kg/m²)
      \end{itemize}
    \end{column}
    \begin{column}{0.48\textwidth}
      \textbf{\textcolor{accent}{Discreta (conteo)}}\\[4pt]
      Número finito de valores, típicamente enteros\\[6pt]
      \begin{itemize}
        \item N.º de gestaciones
        \item N.º de hospitalizaciones
        \item N.º de medicamentos
      \end{itemize}
    \end{column}
  \end{columns}

  \vspace{8pt}
  \begin{nota}
    Una variable discreta con ≥6 valores posibles se comporta como continua en análisis.
  \end{nota}
\end{frame}

% Slide 12
\begin{frame}{Regla de oro: prefiere variables continuas}
  \textbf{Jerarquía de poder estadístico} (Browner, Tabla 4.1):

  \vspace{8pt}
  \begin{center}
    \begin{tikzpicture}[font=\small]
      \foreach \lbl/\col/\x in {
        {Continua}/{accent}/{0},
        {Discreta}/{primary!70}/{2.5},
        {Ordinal}/{primary!50}/{5},
        {Nominal/Dicotómica}/{primary!30}/{7.5}
      }{
        \node[rectangle, fill=\col, text=white, rounded corners=2pt,
              minimum width=2.0cm, minimum height=0.7cm, align=center,
              font=\footnotesize\bfseries] at (\x, 0) {\lbl};
      }
      \draw[-{Stealth}, line width=1.5pt, color=accent]
        (8.8,0) -- (10.2,0)
        node[right, font=\footnotesize, color=textdark] {más poder};
    \end{tikzpicture}
  \end{center}

  \vspace{8pt}
  \begin{clave}
    No conviertas IMC en «obeso / no obeso» si puedes quedarte con el
    número. Más información = mayor poder = menor tamaño de muestra.
  \end{clave}
\end{frame}
```

- [ ] **Step 7.2: Compile and verify (12 slides)**
```bash
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: 12 slides, all three TikZ diagrams render, columns balanced, no text overflow.

- [ ] **Step 7.3: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: add tipos de variables section (slides 9-12)"
```

---

## Task 8: Add Sección 4 — Precisión y exactitud + TikZ dianas (Slides 13–16)

**Files:**
- Modify: `Slides/Lecture01_Operacionalizacion.tex`

- [ ] **Step 8.1: Add Sección 4 after Sección 3**

```latex
% ============================================================
% SECCIÓN 4: Precisión y exactitud
% ============================================================
\section{Precisión y exactitud}

% Slide 13
\begin{frame}{¿Por qué dos médicos obtienen valores distintos?}
  \begin{caso}[Retomamos el caso]
    Dos residentes toman la presión arterial al mismo paciente con el
    mismo tensiómetro, tres veces cada uno. Los valores difieren.\\[4pt]
    ¿Por qué?
  \end{caso}

  \vspace{8pt}
  \textbf{Fuentes de \textcolor{accent}{error aleatorio}:}
  \begin{itemize}
    \item \textbf{Observador:} velocidad de deflación del manguito, técnica
    \item \textbf{Instrumento:} manómetro descalibrado, temperatura
    \item \textbf{Participante:} variación fisiológica, esfuerzo, ansiedad
  \end{itemize}
\end{frame}

% Slide 14
\begin{frame}{Precisión}
  \begin{definicion}[Precisión]
    Grado en que una variable produce el \textbf{mismo valor} cuando se
    mide repetidamente. Sinónimos: reproducibilidad, confiabilidad,
    consistencia.\\[4pt]
    Mayor precisión = menor error aleatorio = \textbf{mayor poder estadístico}.
  \end{definicion}

  \vspace{8pt}
  \textbf{¿Cómo se evalúa?}
  \begin{itemize}
    \item Variables continuas: desviación estándar intra-sujeto, coef.\ de variación
    \item Variables categóricas: porcentaje de acuerdo, \textbf{Kappa de Cohen},
          coeficiente de correlación intraclase (CCI)
  \end{itemize}
  \begin{nota}
    \fullcite{Bland1986-di}
  \end{nota}
\end{frame}

% Slide 15
\begin{frame}{Exactitud}
  \begin{definicion}[Exactitud]
    Grado en que una variable se \textbf{aproxima al valor verdadero}.
    Depende de minimizar el \textbf{sesgo} (error sistemático), además
    de maximizar la precisión.
  \end{definicion}

  \vspace{8pt}
  \textbf{Fuentes de \textcolor{accent}{sesgo}:}
  \begin{itemize}
    \item \textbf{Observador:} tendencia inconsciente a redondear valores
    \item \textbf{Instrumento:} balanza no calibrada → pesos consistentemente bajos
    \item \textbf{Participante:} sesgo de recuerdo, deseabilidad social
  \end{itemize}

  \vspace{4pt}
  \textbf{¿Cómo se evalúa?} Comparación con un \textbf{estándar de oro}
  (\textit{gold standard}).
\end{frame}

% Slide 16 — TikZ: Las 4 dianas
\begin{frame}{Precisión vs.\ exactitud: las 4 dianas}
  \begin{center}
  \begin{tikzpicture}[scale=0.85]
    % Helper command for a target at position (cx, cy)
    % with dots offset by (dx, dy) from center and scatter (sc)
    % Panel labels via text nodes

    % --- Panel TL: Alta precisión, alta exactitud ---
    \begin{scope}[shift={(-3.2, 1.8)}]
      \fill[bglight!60] (0,0) circle (1.4);
      \fill[white]      (0,0) circle (0.95);
      \fill[bglight!60] (0,0) circle (0.5);
      \fill[primary, opacity=0.3] (0,0) circle (0.08);
      \foreach \dx/\dy in {0.08/0.06, -0.07/0.09, 0.05/-0.08, -0.09/-0.05, 0.1/0.03}
        \fill[accent] (\dx,\dy) circle (0.1);
      \node[above, font=\scriptsize\bfseries, color=primary] at (0,1.5)
        {Alta precisión};
      \node[below, font=\scriptsize\bfseries, color=primary] at (0,-1.5)
        {Alta exactitud};
    \end{scope}

    % --- Panel TR: Alta precisión, baja exactitud ---
    \begin{scope}[shift={(3.2, 1.8)}]
      \fill[bglight!60] (0,0) circle (1.4);
      \fill[white]      (0,0) circle (0.95);
      \fill[bglight!60] (0,0) circle (0.5);
      \fill[primary, opacity=0.3] (0,0) circle (0.08);
      \foreach \dx/\dy in {0.78/0.56, 0.72/0.62, 0.80/0.50, 0.76/0.58, 0.74/0.64}
        \fill[accent] (\dx,\dy) circle (0.1);
      \node[above, font=\scriptsize\bfseries, color=primary] at (0,1.5)
        {Alta precisión};
      \node[below, font=\scriptsize\bfseries, color=primary] at (0,-1.5)
        {Baja exactitud (sesgo)};
    \end{scope}

    % --- Panel BL: Baja precisión, alta exactitud ---
    \begin{scope}[shift={(-3.2, -1.8)}]
      \fill[bglight!60] (0,0) circle (1.4);
      \fill[white]      (0,0) circle (0.95);
      \fill[bglight!60] (0,0) circle (0.5);
      \fill[primary, opacity=0.3] (0,0) circle (0.08);
      \foreach \dx/\dy in {0.6/-0.5, -0.7/0.4, 0.3/0.8, -0.5/-0.7, 0.8/0.2}
        \fill[accent] (\dx,\dy) circle (0.1);
      \node[above, font=\scriptsize\bfseries, color=primary] at (0,1.5)
        {Baja precisión};
      \node[below, font=\scriptsize\bfseries, color=primary] at (0,-1.5)
        {Alta exactitud};
    \end{scope}

    % --- Panel BR: Baja precisión, baja exactitud ---
    \begin{scope}[shift={(3.2, -1.8)}]
      \fill[bglight!60] (0,0) circle (1.4);
      \fill[white]      (0,0) circle (0.95);
      \fill[bglight!60] (0,0) circle (0.5);
      \fill[primary, opacity=0.3] (0,0) circle (0.08);
      \foreach \dx/\dy in {0.9/0.5, -0.8/-0.6, 0.4/-0.9, -0.6/0.8, 0.7/-0.3}
        \fill[accent] (\dx,\dy) circle (0.1);
      \node[above, font=\scriptsize\bfseries, color=primary] at (0,1.5)
        {Baja precisión};
      \node[below, font=\scriptsize\bfseries, color=primary] at (0,-1.5)
        {Baja exactitud};
    \end{scope}

    % Dividing lines
    \draw[color=bglight, line width=1pt] (0,-3.5) -- (0,3.5);
    \draw[color=bglight, line width=1pt] (-5,0)   -- (5,0);
  \end{tikzpicture}
  \end{center}

  \vspace{-4pt}
  \begin{center}
    \footnotesize\textit{Adaptado de Browner et al. (2022), Figura 4.2}
  \end{center}
\end{frame}
```

- [ ] **Step 8.2: Compile and verify (16 slides, 4-panel diana renders)**
```bash
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: 16 slides, 4-target diagram renders with dots in correct positions.
**If dots in TR panel appear outside ring:** reduce the offset values from 0.78 to ~0.5.

- [ ] **Step 8.3: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: add precision/exactitud section + 4-panel diana TikZ diagram"
```

---

## Task 9: Add Sección 5 — Confiabilidad y validez (Slides 17–20)

**Files:**
- Modify: `Slides/Lecture01_Operacionalizacion.tex`

- [ ] **Step 9.1: Add Sección 5 after Sección 4**

```latex
% ============================================================
% SECCIÓN 5: Confiabilidad y validez
% ============================================================
\section{Confiabilidad y validez}

% Slide 17
\begin{frame}{Confiabilidad en la práctica}
  \begin{caso}[¿Dos médicos, mismo diagnóstico?]
    Dos internistas examinan de forma independiente a 50 pacientes y
    clasifican cada caso como «anemia» o «no anemia».
    ¿Qué tan seguido coinciden?
  \end{caso}

  \vspace{8pt}
  \begin{columns}[T]
    \begin{column}{0.55\textwidth}
      \textbf{Confiabilidad inter-observador}\\[4pt]
      Medida con el \textbf{Kappa de Cohen ($\kappa$)}:\\[4pt]
      \begin{tabular}{ll}
        $\kappa < 0.4$ & Pobre \\
        $0.4$--$0.6$   & Moderada \\
        $0.6$--$0.8$   & Buena \\
        $> 0.8$        & Excelente \\
      \end{tabular}
    \end{column}
    \begin{column}{0.4\textwidth}
      \begin{nota}
        Kappa corrige el acuerdo por azar.\\
        El simple «\% de acuerdo» es engañoso cuando una categoría es
        muy frecuente.
      \end{nota}
    \end{column}
  \end{columns}
\end{frame}

% Slide 18
\begin{frame}{Validez}
  \begin{definicion}[Validez]
    Dimensión cualitativa de la exactitud: qué tan bien una medición
    \textbf{representa el fenómeno} que pretende medir.
  \end{definicion}

  \vspace{8pt}
  \textbf{Ejemplo (Browner):}

  \begin{columns}[T]
    \begin{column}{0.48\textwidth}
      \textbf{Creatinina sérica}\\
      \textit{Precisa y exacta}\\[4pt]
      Pero: influida también por la \textbf{masa muscular}.
      Un paciente con poca masa puede tener IRC con creatinina normal.
    \end{column}
    \begin{column}{0.48\textwidth}
      \textbf{Cistatina C}\\
      \textit{Precisa y exacta}\\[4pt]
      \textbf{Más válida} como medida de función renal: no depende
      de masa muscular.
    \end{column}
  \end{columns}

  \vspace{6pt}
  \begin{nota}
    Ambas son precisas; la diferencia está en qué tan bien representan
    la \textit{filtración glomerular real}.
  \end{nota}
\end{frame}

% Slide 19
\begin{frame}{Tipos de validez}
  \begin{tabular}{p{3.0cm} p{7.5cm}}
    \toprule
    \textbf{Tipo} & \textbf{Pregunta que responde} \\
    \midrule
    \textbf{De contenido} &
      ¿La medida cubre \textit{todos} los aspectos del fenómeno?
      \textit{(SF-36 para calidad de vida)} \\[4pt]
    \textbf{De apariencia} &
      ¿La medida parece razonable a simple vista?
      \textit{(fragilidad = debilidad + fatiga + pérdida de peso)} \\[4pt]
    \textbf{De constructo} &
      ¿La medida se comporta como predice la teoría?
      \textit{(aislamiento social separa quienes tienen pocas amistades)} \\[4pt]
    \textbf{Predictiva} &
      ¿La medida predice un desenlace futuro?
      \textit{(fragilidad predice institucionalización)} \\[4pt]
    \textbf{De criterio} &
      ¿La medida correlaciona con otra establecida?
      \textit{(nueva prueba de masa muscular vs.\ fuerza de prensión)} \\
    \bottomrule
  \end{tabular}
\end{frame}

% Slide 20
\begin{frame}{El estándar de oro (\textit{gold standard})}
  \begin{definicion}[Estándar de oro]
    Medición de referencia que se cree que representa mejor
    el \textbf{valor verdadero} de la característica.
  \end{definicion}

  \vspace{8pt}
  \begin{columns}[T]
    \begin{column}{0.48\textwidth}
      \textbf{Cuando existe:}\\[4pt]
      Se puede calcular exactitud cuantitativamente.\\[4pt]
      \textit{Ej.: biopsia para diagnóstico histológico de cáncer}
    \end{column}
    \begin{column}{0.48\textwidth}
      \textbf{Cuando no existe:}\\[4pt]
      Variables subjetivas: dolor, calidad de vida, depresión.\\[4pt]
      Se recurre a los tipos de validez del slide anterior.
    \end{column}
  \end{columns}

  \vspace{8pt}
  \begin{nota}
    Elegir el gold standard puede ser difícil y requiere consenso
    de expertos y revisión de la literatura.
  \end{nota}
\end{frame}
```

- [ ] **Step 9.2: Compile and verify (20 slides)**
```bash
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: 20 slides, tabular on slide 19 fits within frame (5 rows, narrow columns).
**If slide 19 overflows:** reduce font with `{\small ...}` around the tabular, or abbreviate examples.

- [ ] **Step 9.3: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: add confiabilidad and validez section (slides 17-20)"
```

---

## Task 10: Add Sección 6–7 — Cierre, mensajes clave, bibliografía (Slides 21–24)

**Files:**
- Modify: `Slides/Lecture01_Operacionalizacion.tex`

- [ ] **Step 10.1: Add final sections**

```latex
% ============================================================
% SECCIÓN 6: Mapa de cierre
% ============================================================
\section{Síntesis}

% Slide 21
\begin{frame}{El mapa completo (Browner, Fig.\ 4.1)}
  \begin{center}
  \begin{tikzpicture}[
    font=\small,
    box/.style={rectangle, rounded corners=3pt, draw=primary,
                fill=bglight, text width=2.4cm, align=center,
                minimum height=0.85cm, inner sep=5pt},
    accentbox/.style={rectangle, rounded corners=3pt, draw=accent,
                      fill=accent!10, text width=2.4cm, align=center,
                      minimum height=0.85cm, inner sep=5pt,
                      font=\small\bfseries},
    arrow/.style={-{Stealth[length=5pt]}, line width=1pt, color=primary}
  ]
    \node[box] (rq)  {Pregunta de\\investigación};
    \node[accentbox, right=1.6cm of rq] (meas) {Diseño de\\mediciones};
    \node[box, right=1.6cm of meas] (data) {Datos\\del estudio};
    \node[box, right=1.6cm of data] (inf)  {Inferencia\\sobre el fenómeno};

    \draw[arrow] (rq)   -- (meas);
    \draw[arrow] (meas) -- (data);
    \draw[arrow] (data) -- (inf);

    \node[below=0.5cm of meas, font=\footnotesize\itshape, color=accent,
          text width=5cm, align=center]
      {Precisión · Exactitud · Validez\\
       Escala de medición};
  \end{tikzpicture}
  \end{center}

  \vspace{4pt}
  \textit{La validez de las conclusiones del estudio depende de qué tan
  bien el diseño de mediciones representa los fenómenos de interés.}
\end{frame}

% Slide 22
\begin{frame}{¿Cómo medirías obesidad ahora?}
  \begin{caso}[Resolviendo el caso inicial]
    \textbf{Pregunta:} ¿La obesidad es un factor de riesgo para DM2
    en adultos jóvenes de Lima?
  \end{caso}

  \vspace{6pt}
  \begin{tabular}{p{3.2cm} p{6.5cm}}
    \toprule
    \textbf{Medida} & \textbf{Decisión} \\
    \midrule
    IMC (kg/m²) & Continua, alta precisión. Útil si el mecanismo es
                  acumulación de grasa total. \\[3pt]
    Perímetro abdominal & Continua, captura grasa visceral.
                         Más válida para riesgo metabólico. \\[3pt]
    \% grasa corporal & Continua, requiere equipo especial; alta exactitud
                        si se usa DEXA. \\[3pt]
    Dicotómica (obeso/no) & Pierde información. Usar solo si el diseño
                            lo requiere explícitamente. \\
    \bottomrule
  \end{tabular}

  \vspace{4pt}
  \begin{nota}
    No hay una respuesta única: la operacionalización correcta depende
    de la pregunta, los recursos y la población.
  \end{nota}
\end{frame}

% ============================================================
% SECCIÓN 7: Mensajes clave y referencias
% ============================================================
\section{Mensajes clave}

% Slide 23
\begin{frame}{Mensajes clave}
  \begin{clave}
    \begin{enumerate}
      \item \textbf{Operacionalizar} es definir exactamente cómo medir
            un concepto abstracto. La definición operacional debe ser
            explícita, reproducible y adecuada a la pregunta de investigación.
      \item Las variables \textbf{continuas} tienen mayor poder estadístico
            que las categóricas: no las dicotomices innecesariamente.
      \item \textbf{Precisión} = sin error aleatorio (reproducibilidad).
            \textbf{Exactitud} = cerca del valor verdadero (sin sesgo).
            Son conceptos relacionados pero distintos.
      \item \textbf{Validez} es qué tan bien la medición representa
            el fenómeno: busca instrumentos ya validados antes de crear uno nuevo.
      \item Toda medición tiene limitaciones. El objetivo es
            \textbf{minimizarlas}, no eliminarlas.
    \end{enumerate}
  \end{clave}
\end{frame}

% Slide 24
\begin{frame}[allowframebreaks]{Referencias}
  \printbibliography[heading=none]
\end{frame}

\end{document}
```

- [ ] **Step 10.2: Run full 3-pass compile + bibtex**
```bash
cd Slides
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
BIBINPUTS=..:$BIBINPUTS bibtex Lecture01_Operacionalizacion
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: 24 slides, references on slide 24, no `?` for citations.

- [ ] **Step 10.3: Visual check — open PDF**
```bash
open Slides/Lecture01_Operacionalizacion.pdf
```
Check each slide for: text overflow, font rendering, TikZ figure alignment, table fit.

- [ ] **Step 10.4: Commit**
```bash
git add Slides/Lecture01_Operacionalizacion.tex
git commit -m "feat: complete Beamer deck (24 slides) — operacionalizacion variables"
```

---

## Task 11: Set up Quarto project and theme

**Files:**
- Create: `Quarto/_quarto.yml`
- Modify: `Quarto/theme-template.scss`

- [ ] **Step 11.1: Create `Quarto/_quarto.yml`**

```yaml
project:
  type: website
  output-dir: ../docs

website:
  title: "ABC of Research — ADIECS"

format:
  revealjs:
    theme: [default, theme-template.scss]
    slide-number: true
    progress: true
    transition: fade
    transition-speed: fast
    highlight-style: github
    lang: es
    fig-align: center
    link-external-newwindow: true
```

- [ ] **Step 11.2: Update `Quarto/theme-template.scss` with project colors**

Add at the top of the existing `theme-template.scss` (after any existing content):

```scss
// ============================================================
// ABC of Research — ADIECS theme
// ============================================================

// Fonts
@import url('https://fonts.googleapis.com/css2?family=Fira+Sans:wght@300;400;600;700&display=swap');

// Colors
$primary: #2C3E50;
$accent: #1A7A8A;
$bglight: #ECF0F1;
$offwhite: #FAFAFA;
$textdark: #2D2D2D;
$casebg: #FEF9EE;
$amber: #D4A017;

// Apply to RevealJS
.reveal {
  font-family: 'Fira Sans', sans-serif;
  color: $textdark;
  background-color: $offwhite;
}

.reveal h1, .reveal h2, .reveal h3 {
  color: $primary;
  font-weight: 600;
}

.reveal .slide-number { color: $accent; }

// Custom divs (equivalent to Beamer environments)
.definicion {
  border-left: 4px solid $accent;
  background: $bglight;
  padding: 0.5em 0.8em;
  margin: 0.5em 0;
  font-size: 0.9em;
}

.caso {
  border: 1px solid $amber;
  border-left: 4px solid $amber;
  background: $casebg;
  padding: 0.5em 0.8em;
  margin: 0.5em 0;
  font-size: 0.9em;
}

.clave {
  background: $accent;
  color: white;
  padding: 0.5em 0.8em;
  margin: 0.5em 0;
  border-radius: 3px;
  font-size: 0.9em;
}

.nota {
  color: $textdark;
  opacity: 0.75;
  font-size: 0.78em;
  padding: 0.3em 0.5em;
}
```

- [ ] **Step 11.3: Commit**
```bash
git add Quarto/_quarto.yml Quarto/theme-template.scss
git commit -m "feat: set up Quarto project config and RevealJS theme"
```

---

## Task 12: Create Quarto lecture file

**Files:**
- Create: `Quarto/Lecture01_Operacionalizacion.qmd`

- [ ] **Step 12.1: Create the Quarto file**

Create `Quarto/Lecture01_Operacionalizacion.qmd`. The structure mirrors the Beamer file using Quarto slide syntax (`##` for slides, `:::` divs for environments):

```markdown
---
title: "Operacionalización de Variables"
subtitle: "Cómo convertir conceptos en datos medibles"
author: ""
institute: "ADIECS — Semillero ABC of Research | UNMSM — San Fernando"
date: "2026"
format:
  revealjs:
    theme: [default, theme-template.scss]
    slide-number: true
    progress: true
    transition: fade
    lang: es
bibliography: ../Bibliography_base.bib
---

## Agenda

::: columns
::: {.column width="50%"}
**1.** Caso clínico

**2.** ¿Qué es operacionalizar?
:::
::: {.column width="50%"}
**3.** Tipos de variables

**4.** Precisión, exactitud y validez
:::
:::

# El problema de medir

## ¿Cómo mides obesidad? {.caso}

::: {.caso}
Quieres estudiar si la **obesidad** es un factor de riesgo para diabetes
tipo 2 en adultos jóvenes de Lima. *¿Qué variable mides?*
:::

- Índice de masa corporal (IMC)
- Perímetro abdominal
- Porcentaje de grasa corporal
- Presencia de acantosis nigricans

## El problema

Las cuatro medidas aplicadas al **mismo paciente** dan resultados distintos.

| Medida | Valor | Clasificación |
|--------|-------|--------------|
| IMC | 28.4 kg/m² | Sobrepeso |
| Perímetro abd. | 94 cm | Riesgo aumentado |
| % grasa corp. | 34% | Obesidad |
| Acantosis | Presente | Resistencia a insulina |

**¿Cuál es la «correcta»?**

## La respuesta

::: {.definicion}
Depende de **qué** exactamente quieres medir y **para qué**. No hay una
medida «correcta» universal: hay medidas más o menos adecuadas según la
pregunta de investigación.
:::

A este proceso de definir *cómo* medir un concepto abstracto lo llamamos
**operacionalización**.

# Conceptos fundamentales

## ¿Qué es una variable?

::: {.definicion}
Atributo observable que **varía** entre individuos y que puede ser medido
o clasificado.
:::

**Ejemplos clínicos:**

- Edad, sexo, nivel de hemoglobina
- Diagnóstico de hipertensión (sí/no)
- Grado de dolor (ninguno / leve / moderado / severo)
- Número de gestaciones previas

## ¿Qué es operacionalizar?

::: {.definicion}
Especificación **exacta** de cómo se medirá un concepto abstracto:
instrumento, unidad, punto de corte, protocolo.
:::

::: {.nota}
**Ejemplo (Browner, Apéndice 4A):** Fuerza de prensión con dinamómetro.
«Coloque el dinamómetro en la mano derecha con el dial hacia la palma.
El brazo debe estar flexionado a 90° con el antebrazo paralelo al suelo.
Apriete tan fuerte como pueda mientras cuento hasta tres...»
:::

## La brecha fenómeno → medición

```{=html}
<div style="display:flex; align-items:center; justify-content:center; gap:2em; margin-top:1em;">
  <div style="border:2px solid #1A7A8A; border-radius:6px; padding:1em 1.5em; background:#ECF0F1; text-align:center;">
    <strong>Fenómeno de interés</strong><br><em>obesidad</em>
  </div>
  <div style="font-size:1.5em; color:#1A7A8A;">→</div>
  <div style="border:2px solid #1A7A8A; border-radius:6px; padding:1em 1.5em; background:#ECF0F1; text-align:center;">
    <strong>Medición en el estudio</strong><br><em>IMC, cm, %</em>
  </div>
</div>
<p style="text-align:center; font-style:italic; font-size:0.8em; color:#1A7A8A; margin-top:0.8em;">
La validez del estudio depende de esta distancia — Browner et al. (2022), Fig. 4.1
</p>
```

# Tipos de variables

## Dos grandes familias

```{=html}
<div style="display:flex; gap:3em; justify-content:center; margin-top:1em;">
  <div style="text-align:center;">
    <div style="background:#2C3E50; color:white; padding:0.5em 2em; border-radius:4px; font-weight:bold;">Variable</div>
    <div style="display:flex; gap:2em; margin-top:1em;">
      <div style="border:1px solid #2C3E50; padding:0.4em 1em; border-radius:4px; background:#ECF0F1;">Categórica</div>
      <div style="border:1px solid #2C3E50; padding:0.4em 1em; border-radius:4px; background:#ECF0F1;">Numérica</div>
    </div>
  </div>
</div>
```

::: columns
::: {.column width="50%"}
**Categórica:** Dicotómica · Nominal · Ordinal
:::
::: {.column width="50%"}
**Numérica:** Continua · Discreta
:::
:::

## Variables categóricas

::: columns
::: {.column width="33%"}
**Dicotómica**

Dos categorías

*Vivo / muerto*
*Embarazada / no*
:::
::: {.column width="33%"}
**Nominal**

Sin orden

*Tipo de sangre*
*Identidad de género*
:::
::: {.column width="33%"}
**Ordinal**

Con orden, sin intervalos cuantificables

*Dolor: ninguno / leve / moderado / severo*
:::
:::

::: {.nota}
Poder estadístico: dicotómica ≈ nominal < ordinal
:::

## Variables numéricas

::: columns
::: {.column width="50%"}
**Continua**

Infinitos valores posibles

- Hemoglobina (g/dL)
- Presión arterial (mmHg)
- IMC (kg/m²)
:::
::: {.column width="50%"}
**Discreta (conteo)**

Número finito de valores, típicamente enteros

- N.º de gestaciones
- N.º de hospitalizaciones
:::
:::

::: {.nota}
Una variable discreta con ≥6 valores posibles se comporta como continua en análisis.
:::

## Regla de oro: prefiere variables continuas

**Jerarquía de poder estadístico** (Browner, Tabla 4.1):

Continua > Discreta > Ordinal > Nominal / Dicotómica

::: {.clave}
No conviertas IMC en «obeso / no obeso» si puedes quedarte con el número.
Más información = mayor poder = menor tamaño de muestra.
:::

# Precisión y exactitud

## ¿Por qué dos médicos obtienen valores distintos?

::: {.caso}
Dos residentes toman la presión arterial al mismo paciente con el mismo
tensiómetro, tres veces cada uno. Los valores difieren. ¿Por qué?
:::

**Fuentes de error aleatorio:**

- **Observador:** velocidad de deflación del manguito, técnica
- **Instrumento:** manómetro descalibrado, temperatura
- **Participante:** variación fisiológica, ansiedad

## Precisión

::: {.definicion}
Grado en que una variable produce el **mismo valor** cuando se mide
repetidamente. Sinónimos: reproducibilidad, confiabilidad, consistencia.

Mayor precisión = menor error aleatorio = **mayor poder estadístico**.
:::

**¿Cómo se evalúa?**

- Variables continuas: desviación estándar intra-sujeto, coef. de variación
- Variables categóricas: **Kappa de Cohen**, coeficiente de correlación intraclase

## Exactitud

::: {.definicion}
Grado en que una variable se **aproxima al valor verdadero**. Depende de
minimizar el **sesgo** (error sistemático).
:::

**Fuentes de sesgo:**

- **Observador:** tendencia a redondear valores
- **Instrumento:** balanza no calibrada → pesos consistentemente bajos
- **Participante:** sesgo de recuerdo, deseabilidad social

**¿Cómo se evalúa?** Comparación con un **estándar de oro** (*gold standard*).

## Precisión vs. exactitud: las 4 dianas

```{=html}
<div style="display:grid; grid-template-columns:1fr 1fr; gap:1em; margin-top:0.5em;">
  <div style="text-align:center;">
    <svg width="120" height="120" viewBox="-1.6 -1.6 3.2 3.2">
      <circle cx="0" cy="0" r="1.4" fill="#ECF0F1"/>
      <circle cx="0" cy="0" r="0.95" fill="white"/>
      <circle cx="0" cy="0" r="0.5" fill="#ECF0F1"/>
      <circle cx="0.08" cy="0.06" r="0.1" fill="#1A7A8A"/>
      <circle cx="-0.07" cy="0.09" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.05" cy="-0.08" r="0.1" fill="#1A7A8A"/>
      <circle cx="-0.09" cy="-0.05" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.1" cy="0.03" r="0.1" fill="#1A7A8A"/>
    </svg>
    <div style="font-size:0.7em;"><strong>Alta precisión, alta exactitud</strong></div>
  </div>
  <div style="text-align:center;">
    <svg width="120" height="120" viewBox="-1.6 -1.6 3.2 3.2">
      <circle cx="0" cy="0" r="1.4" fill="#ECF0F1"/>
      <circle cx="0" cy="0" r="0.95" fill="white"/>
      <circle cx="0" cy="0" r="0.5" fill="#ECF0F1"/>
      <circle cx="0.78" cy="0.56" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.72" cy="0.62" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.80" cy="0.50" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.76" cy="0.58" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.74" cy="0.64" r="0.1" fill="#1A7A8A"/>
    </svg>
    <div style="font-size:0.7em;"><strong>Alta precisión, baja exactitud</strong> (sesgo)</div>
  </div>
  <div style="text-align:center;">
    <svg width="120" height="120" viewBox="-1.6 -1.6 3.2 3.2">
      <circle cx="0" cy="0" r="1.4" fill="#ECF0F1"/>
      <circle cx="0" cy="0" r="0.95" fill="white"/>
      <circle cx="0" cy="0" r="0.5" fill="#ECF0F1"/>
      <circle cx="0.6" cy="-0.5" r="0.1" fill="#1A7A8A"/>
      <circle cx="-0.7" cy="0.4" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.3" cy="0.8" r="0.1" fill="#1A7A8A"/>
      <circle cx="-0.5" cy="-0.7" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.8" cy="0.2" r="0.1" fill="#1A7A8A"/>
    </svg>
    <div style="font-size:0.7em;"><strong>Baja precisión, alta exactitud</strong></div>
  </div>
  <div style="text-align:center;">
    <svg width="120" height="120" viewBox="-1.6 -1.6 3.2 3.2">
      <circle cx="0" cy="0" r="1.4" fill="#ECF0F1"/>
      <circle cx="0" cy="0" r="0.95" fill="white"/>
      <circle cx="0" cy="0" r="0.5" fill="#ECF0F1"/>
      <circle cx="0.9" cy="0.5" r="0.1" fill="#1A7A8A"/>
      <circle cx="-0.8" cy="-0.6" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.4" cy="-0.9" r="0.1" fill="#1A7A8A"/>
      <circle cx="-0.6" cy="0.8" r="0.1" fill="#1A7A8A"/>
      <circle cx="0.7" cy="-0.3" r="0.1" fill="#1A7A8A"/>
    </svg>
    <div style="font-size:0.7em;"><strong>Baja precisión, baja exactitud</strong></div>
  </div>
</div>
```

# Confiabilidad y validez

## Confiabilidad en la práctica

::: {.caso}
Dos internistas examinan de forma independiente a 50 pacientes y clasifican
cada caso como «anemia» o «no anemia». ¿Qué tan seguido coinciden?
:::

**Kappa de Cohen (κ):**

| κ | Interpretación |
|---|---|
| < 0.4 | Pobre |
| 0.4–0.6 | Moderada |
| 0.6–0.8 | Buena |
| > 0.8 | Excelente |

::: {.nota}
Kappa corrige el acuerdo por azar. El simple «% de acuerdo» es engañoso.
:::

## Validez

::: {.definicion}
Dimensión cualitativa de la exactitud: qué tan bien una medición
**representa el fenómeno** que pretende medir.
:::

::: columns
::: {.column width="50%"}
**Creatinina sérica**

Precisa y exacta. Pero influida también por la **masa muscular**.
:::
::: {.column width="50%"}
**Cistatina C**

Precisa y exacta. **Más válida** para función renal: no depende de masa muscular.
:::
:::

## Tipos de validez

| Tipo | Pregunta que responde |
|------|-----------------------|
| De contenido | ¿Cubre todos los aspectos del fenómeno? |
| De apariencia | ¿Parece razonable a simple vista? |
| De constructo | ¿Se comporta como predice la teoría? |
| Predictiva | ¿Predice un desenlace futuro? |
| De criterio | ¿Correlaciona con otra medida establecida? |

## El estándar de oro (*gold standard*)

::: {.definicion}
Medición de referencia que mejor representa el **valor verdadero**
de la característica.
:::

::: columns
::: {.column width="50%"}
**Cuando existe:**

Exactitud cuantificable.

*Ej.: biopsia para cáncer*
:::
::: {.column width="50%"}
**Cuando no existe:**

Variables subjetivas: dolor, calidad de vida, depresión.

→ Se usan los tipos de validez.
:::
:::

# Síntesis

## El mapa completo

```{=html}
<div style="display:flex; align-items:center; justify-content:center; gap:1em; margin-top:1em; flex-wrap:wrap;">
  <div style="border:1px solid #2C3E50; border-radius:4px; padding:0.6em 1em; background:#ECF0F1; text-align:center; font-size:0.85em;">Pregunta de<br>investigación</div>
  <div style="color:#1A7A8A; font-size:1.3em;">→</div>
  <div style="border:2px solid #1A7A8A; border-radius:4px; padding:0.6em 1em; background:#e8f4f5; text-align:center; font-size:0.85em; font-weight:bold;">Diseño de<br>mediciones<br><span style="font-size:0.8em; color:#1A7A8A;">Precisión · Exactitud · Validez</span></div>
  <div style="color:#1A7A8A; font-size:1.3em;">→</div>
  <div style="border:1px solid #2C3E50; border-radius:4px; padding:0.6em 1em; background:#ECF0F1; text-align:center; font-size:0.85em;">Datos<br>del estudio</div>
  <div style="color:#1A7A8A; font-size:1.3em;">→</div>
  <div style="border:1px solid #2C3E50; border-radius:4px; padding:0.6em 1em; background:#ECF0F1; text-align:center; font-size:0.85em;">Inferencia<br>sobre el fenómeno</div>
</div>
```

*La validez de las conclusiones depende de qué tan bien el diseño de mediciones representa los fenómenos de interés.*

## ¿Cómo medirías obesidad ahora?

::: {.caso}
¿La obesidad es un factor de riesgo para DM2 en adultos jóvenes de Lima?
:::

| Medida | Decisión |
|--------|----------|
| IMC (kg/m²) | Continua, alta precisión. Útil para grasa total. |
| Perímetro abdominal | Continua, captura grasa visceral. Más válida para riesgo metabólico. |
| % grasa corporal | Alta exactitud con DEXA; requiere equipo. |
| Dicotómica (obeso/no) | Pierde información. Evitar si es posible. |

::: {.nota}
La operacionalización correcta depende de la pregunta, los recursos y la población.
:::

# Mensajes clave

## Mensajes clave

::: {.clave}
1. **Operacionalizar** es definir exactamente cómo medir un concepto abstracto.
2. Las variables **continuas** tienen mayor poder estadístico: no las dicotomices.
3. **Precisión** = sin error aleatorio. **Exactitud** = cerca del valor verdadero.
4. **Validez** es qué tan bien la medición representa el fenómeno.
5. Busca instrumentos ya validados antes de crear uno nuevo.
:::

## Referencias

::: {#refs}
:::
```

- [ ] **Step 12.2: Render Quarto and verify**
```bash
cd Quarto && quarto render Lecture01_Operacionalizacion.qmd
```
Expected: HTML file generated in `docs/` (or local), opens in browser without errors. Check all 4 diana SVGs render and custom divs display with correct colors.

- [ ] **Step 12.3: Commit**
```bash
git add Quarto/Lecture01_Operacionalizacion.qmd
git commit -m "feat: add Quarto RevealJS version of lecture"
```

---

## Task 13: Final quality check and deploy

**Files:**
- No new files — verification only

- [ ] **Step 13.1: Run quality score on Quarto file**
```bash
python scripts/quality_score.py Quarto/Lecture01_Operacionalizacion.qmd
```
Expected: score ≥ 80. If below 80, fix reported issues before proceeding.

- [ ] **Step 13.2: Run final 3-pass Beamer compile (clean)**
```bash
cd Slides
rm -f Lecture01_Operacionalizacion.aux Lecture01_Operacionalizacion.bbl
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
BIBINPUTS=..:$BIBINPUTS bibtex Lecture01_Operacionalizacion
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode Lecture01_Operacionalizacion.tex
```
Expected: clean exit, 24 slides, no `?` for citations, no overfull \hbox warnings (or only minor ones).

- [ ] **Step 13.3: Deploy to GitHub Pages**
```bash
./scripts/sync_to_docs.sh Lecture01
```
Expected: `docs/` updated, URL available for sharing with students.

- [ ] **Step 13.4: Final commit**
```bash
git add -A
git commit -m "feat: deploy Lecture01 operacionalizacion-variables to GitHub Pages"
```

---

## Self-Review Checklist

**Spec coverage:**

| Spec requirement | Covered in task |
|-----------------|-----------------|
| Update CLAUDE.md | Task 1 |
| metropolis theme + colors + tcolorbox environments | Task 2 |
| 24-slide Beamer deck | Tasks 3–10 |
| Caso clínico (obesidad/DM2) as hook | Task 5 |
| Appendix 4A example (dinamómetro) | Task 6 |
| TikZ fenómeno→medición diagram | Task 6 |
| Tabla de tipos de variables (Browner 4.1) | Task 7 |
| Regla de oro: continua > categórica | Task 7 |
| TikZ 4-diana figure | Task 8 |
| Tipos de validez (5 tipos) | Task 9 |
| Gold standard slide | Task 9 |
| Mapa de cierre (Browner Fig 4.1 adapted) | Task 10 |
| Resolución del caso clínico | Task 10 |
| 5 mensajes clave | Task 10 |
| Bibliography (3 entries) | Task 10 + bibtex pass |
| Quarto _quarto.yml | Task 11 |
| theme-template.scss updated | Task 11 |
| Quarto .qmd file | Task 12 |
| 4-diana SVG in Quarto | Task 12 |
| Quality score ≥ 80 | Task 13 |
| Deploy to GitHub Pages | Task 13 |

**No placeholders found.** All code blocks are complete.

**Type consistency:** TikZ colors (`accent`, `primary`, `bglight`) defined in Task 2 and used consistently in Tasks 6–10. SCSS variables match Beamer color definitions.
