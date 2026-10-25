# Paper

This directory holds the ISCMI 2026 IEEE conference manuscript for MaternaCare-ES and the assets it needs. The LaTeX source is authoritative; the committed PDF is the build output produced from it. Venue paper ID: VA116.

## Contents

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Writing, naming, build, and bibliography rules for this directory. |
| `README.md` | This file. |
| `oficial/` | Manuscript directory: source, built PDF, bibliography, figures, and venue material. |
| `oficial/benchmarking-slm-spanish-obstetric-qa.tex` | Authoritative LaTeX source, `\documentclass[conference]{IEEEtran}`. |
| `oficial/benchmarking-slm-spanish-obstetric-qa.pdf` | Committed build output; 6 pages, US Letter (612 x 792 pt). |
| `oficial/references.bib` | BibTeX database resolved by `\bibliography{references}`. |
| `oficial/figures/` | Figure assets referenced by the build. |
| `oficial/figures/ft-vs-lora.pdf` | Figure 1: full fine-tuning versus LoRA. |
| `oficial/figures/rag-types-v2.pdf` | Figure 2: No RAG, Hybrid, and independent HyDE retrieval alternatives. |
| `oficial/figures/archive/` | Assets no longer referenced by the build. Retained for provenance. |
| `oficial/figures/archive/execution-runtime.png` | Archived asset, not referenced by the current build. |
| `oficial/figures/archive/inference-pipeline.pdf` | Archived asset, not referenced by the current build. |
| `oficial/figures/archive/lora-training.pdf` | Archived asset, not referenced by the current build. |
| `oficial/figures/archive/ragas-eval-workflow.pdf` | Archived asset, not referenced by the current build. |
| `oficial/figures/archive/rag-types.pdf` | Archived asset, not referenced by the current build. |
| `oficial/submission/` | Material exchanged with the venue. |
| `oficial/submission/ISCMI2026-VA116-revised.pdf` | Reviewer-returned revised PDF. Supplied without its LaTeX source. |
| `oficial/templates/` | IEEE-provided reference material. Outside the build path. |
| `oficial/templates/IEEE-conference-template.docx` | IEEE Word conference template, kept for reference only. |

## Source of truth

`oficial/benchmarking-slm-spanish-obstetric-qa.tex` is the maintained manuscript. `oficial/submission/ISCMI2026-VA116-revised.pdf` is the venue revision the source was synchronized with; it is a record of what was returned, not an editable artifact. Do not treat the PDFs as a source to edit back into LaTeX.

## Build

Run from `papers/oficial/`:

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error benchmarking-slm-spanish-obstetric-qa.tex
```

Without `latexmk`, run the manual sequence:

```bash
pdflatex benchmarking-slm-spanish-obstetric-qa.tex
bibtex benchmarking-slm-spanish-obstetric-qa
pdflatex benchmarking-slm-spanish-obstetric-qa.tex
pdflatex benchmarking-slm-spanish-obstetric-qa.tex
```

The build requires a TeX Live installation that provides `IEEEtran.cls` and `IEEEtran.bst`. They are not vendored in this repository, and `.gitignore` excludes `papers/**/IEEEtran.cls` and `papers/**/IEEEtran.bst`.

The committed PDF is the output of this command: 6 pages on US Letter, no undefined references or citations, and no overfull hboxes. Rebuild and replace `oficial/benchmarking-slm-spanish-obstetric-qa.pdf` whenever the source changes.

## Figures

| File | Figure | Content |
|------|--------|---------|
| `oficial/figures/ft-vs-lora.pdf` | Figure 1 | Full fine-tuning versus LoRA. |
| `oficial/figures/rag-types-v2.pdf` | Figure 2 | No RAG, Hybrid, and independent HyDE retrieval alternatives. |

Files under `oficial/figures/archive/` are not referenced by the current build. Keep them there for provenance rather than deleting them.

## Naming convention

This is a repository convention derived from IEEE submission-system constraints, not an IEEE-mandated standard.

1. ASCII only: `a-z`, `A-Z`, `0-9`, `-`, `_`. No spaces, colons, parentheses, accents, or duplicate-download suffixes.
2. Manuscript source and built PDF share one basename, so `latexmk` writes the PDF next to the source.
3. The manuscript slug derives from the paper title, not from the repository or project name: lowercase kebab-case, abbreviated where the title is long, with no venue and no year. `benchmarking-slm-spanish-obstetric-qa.{tex,pdf}` stands for "Benchmarking General and Medical Small Language Models for Spanish Obstetric Question Answering". Venue identity belongs to `submission/`, so resubmitting elsewhere does not force a rename.
4. Venue artifacts keep the official uppercase venue acronym and paper ID: `ISCMI2026-VA116-revised.pdf`.
5. Figure assets use lowercase kebab-case descriptive names: `ft-vs-lora.pdf`, `rag-types-v2.pdf`.
6. Build artifacts are never committed.

Writing and bibliography rules are in [`AGENTS.md`](AGENTS.md).

## Version control

Tracked: the `.tex`, the built `.pdf`, `references.bib`, the figures, and the venue material under `submission/` and `templates/`.

Gitignored: `*.aux`, `*.bbl`, `*.blg`, `*.out`, `*.toc`, `*.fls`, `*.fdb_latexmk`, `*.synctex.gz`, `*.log`. These build artifacts are never committed.

## Third-party material

`oficial/templates/IEEE-conference-template.docx` is IEEE-provided material, not authored here. `oficial/submission/ISCMI2026-VA116-revised.pdf` is a venue revision returned to the authors.

MIT covers only the original repository code and documentation. See `NOTICE` and `LICENSE` at the repository root for the redistribution scope of models, datasets, source documents, and other third-party material.
