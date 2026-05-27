# BUPT Experiment Report LaTeX Skill

[中文](#中文) | [English](#english)

## 中文

`BUPT-experiment-report-skill` 是一个面向 Codex 的实验报告 LaTeX 技能，用于快速生成或修订北京邮电大学风格的中文实验报告。它将本仓库中的技能说明、封面排版规范和可复用 LaTeX 模板组织成一个可安装的 Codex Skill。

### 功能特性

- 生成仿北邮实验报告封面的 LaTeX 文档。
- 提供全页外框，封面页和正文页保持一致。
- 使用固定列宽表单字段，避免班级、学号、成绩等字段错位或文字重叠。
- 支持 XeLaTeX 中文排版、页码、表格、长表格和实验数据分析章节。
- 包含可直接复用的模板：`assets/templates/bupt-exp-report-template.tex`。
- 在 `SKILL.md` 中内置视觉检查流程，要求渲染封面和正文页预览后再交付。

### 目录结构

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── assets/
    └── templates/
        └── bupt-exp-report-template.tex
```

### 安装方式

将仓库克隆到 Codex 技能目录：

```bash
git clone https://github.com/Paradox-W/BUPT-experiment-report-skill.git \
  ~/.codex/skills/exp-report-latex-skill
```

如果你已经有同名技能目录，可以先备份或删除旧版本，再重新克隆。

### 使用方式

在 Codex 中显式调用：

```text
[$exp-report-latex-skill] 帮我用北邮实验报告格式生成一份 LaTeX 实验报告，并编译成 PDF。
```

也可以将模板复制到项目中手动修改：

```bash
cp ~/.codex/skills/exp-report-latex-skill/assets/templates/bupt-exp-report-template.tex ./report.tex
latexmk -xelatex -interaction=nonstopmode report.tex
```

### 质量检查建议

生成或修改报告后，建议至少检查：

- 封面是否只有一个信息块。
- `班级`、`学号`、`成绩` 是否在同一列起点对齐。
- 所有页面是否都有外框。
- 页码是否位于外框内部且没有碰线。
- 第一页正文是否直接进入实验内容，而不是重复个人信息。

## English

`BUPT-experiment-report-skill` is a Codex skill for creating and revising Chinese LaTeX experiment reports in a Beijing University of Posts and Telecommunications style. It packages a reusable workflow, a professionally aligned cover layout, and a ready-to-use LaTeX template for formal lab reports.

### Features

- Generates a BUPT-style experiment report cover in LaTeX.
- Adds a consistent full-page border to both the cover and body pages.
- Uses fixed-width cover fields to prevent metadata overlap and alignment drift.
- Supports XeLaTeX CJK typography, page numbering, tables, long tables, and experiment analysis sections.
- Includes a reusable template: `assets/templates/bupt-exp-report-template.tex`.
- Provides a visual QA workflow in `SKILL.md`, including cover and content-page preview checks.

### Repository Layout

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── assets/
    └── templates/
        └── bupt-exp-report-template.tex
```

### Installation

Clone this repository into your Codex skills directory:

```bash
git clone https://github.com/Paradox-W/BUPT-experiment-report-skill.git \
  ~/.codex/skills/exp-report-latex-skill
```

If a skill with the same folder name already exists, back it up or remove it before cloning.

### Usage

Invoke the skill explicitly in Codex:

```text
[$exp-report-latex-skill] Create a BUPT-style LaTeX experiment report and compile it to PDF.
```

You can also copy the template into any LaTeX project:

```bash
cp ~/.codex/skills/exp-report-latex-skill/assets/templates/bupt-exp-report-template.tex ./report.tex
latexmk -xelatex -interaction=nonstopmode report.tex
```

### Quality Checklist

After generating or revising a report, verify that:

- The cover has only one metadata block.
- `Class`, `Student ID`, and `Grade` fields are vertically aligned.
- Every page has the outer border frame.
- Page numbers sit inside the frame without touching it.
- The first content page starts with the report body instead of repeated metadata.

## License

This project follows the license included in the repository.
