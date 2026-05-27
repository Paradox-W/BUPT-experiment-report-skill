---
name: exp-report-latex-skill
description: Create or revise Chinese university experiment reports in LaTeX, especially BUPT-style reports with a replicated cover page, aligned cover fields, full-page border frames, CJK typography, tables, theoretical/observed data sections, and XeLaTeX PDF compilation. Use when Codex is asked to make, polish, or fix an experiment/lab report .tex/.pdf, copy a report cover from a screenshot, align cover metadata fields, or add borders to all pages.
---

# Experiment Report LaTeX

Use this skill for Chinese experiment reports that need a formal cover, page border, and compiled PDF.

## Workflow

1. Inspect the current `.tex` file or source materials before editing.
2. Use `assets/templates/bupt-exp-report-template.tex` as the preferred starting point for BUPT-style reports, or copy only the cover/border macros into an existing report.
3. Put identity metadata on the cover only unless the user asks for a repeated information block.
4. Build cover fields with fixed-width table columns, not ad hoc `\hspace` chains. Keep label starts and underline starts aligned.
5. Draw the page border with `tikz` + `eso-pic` in shipout background so every page has the same frame.
6. For cover pages using `hyperref`, disable page anchors around `titlepage` and re-enable them after the cover to avoid duplicate page anchor warnings.
7. Compile with XeLaTeX, preferably:

```bash
latexmk -xelatex -interaction=nonstopmode report.tex
```

8. Render at least page 1 and the first content page to PNG for visual QA when making layout changes:

```bash
gs -q -dSAFER -dBATCH -dNOPAUSE -sDEVICE=pngalpha -r120 \
  -dFirstPage=1 -dLastPage=1 -sOutputFile=cover.png report.pdf
```

9. Verify no cover text overlaps, no duplicate metadata block exists, and the page border does not collide with headers, footers, or content.
10. Clean auxiliary files with `latexmk -c report.tex`; keep only the `.tex` and `.pdf` unless previews were explicitly requested.

## Cover Rules

- Use a large centered school name and report title: `北 京 邮 电 大 学` and `实 验 报 告`.
- Keep the cover form block visually centered and wide enough for Chinese course and experiment names.
- Use two-column rows for short fields: `学院/班级`, `姓名/学号`, `教师/成绩`.
- Use one fixed label width and one fixed value width for both columns.
- Avoid putting `学院、班级、姓名` on one row unless the available width has been tested visually.
- Use `\underline{\makebox[<width>][l]{...}}` for stable lines. Avoid leader rules inside short fields; they often create uneven or stray-looking segments.

## Page Border Rules

Use a single shipout background hook:

```latex
\AddToShipoutPictureBG{%
  \begin{tikzpicture}[remember picture,overlay]
    \draw[line width=0.8pt]
      ($(current page.north west)+(1.25cm,-1.25cm)$)
      rectangle
      ($(current page.south east)+(-1.25cm,1.25cm)$);
  \end{tikzpicture}%
}
```

If using `fancyhdr`, remove the header rule unless the user explicitly wants a header:

```latex
\fancyhf{}
\cfoot{\thepage/\pageref{LastPage}}
\renewcommand{\headrulewidth}{0pt}
```

## Visual QA Checklist

- The cover has no second "基本信息" block after it unless requested.
- The fields `班级`, `学号`, and `成绩` align vertically in their column.
- Values and underline starts align within each column.
- The outer frame appears on the cover and on content pages.
- Page numbers sit inside the frame and do not touch it.
- The first content page starts with the actual report body, usually `实验目的`.
