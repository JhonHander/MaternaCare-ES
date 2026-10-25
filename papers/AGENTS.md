# Paper Writing Rules

## Scope

| Artifact | Path |
|----------|------|
| Manuscript source | `papers/oficial/benchmarking-slm-spanish-obstetric-qa.tex` |
| Build output | `papers/oficial/benchmarking-slm-spanish-obstetric-qa.pdf` |
| Bibliography | `papers/oficial/references.bib` |
| Figures | `papers/oficial/figures/` |

The manuscript uses `\documentclass[conference]{IEEEtran}` for ISCMI 2026, paper ID VA116.

## Non-negotiable rules

- Never invent citations.
- Every citation must be traceable to a real DOI, arXiv page, ACL Anthology page, IEEE/ACM/Springer/Elsevier page, or official documentation.
- Never invent experimental results.
- Use placeholders when evidence is missing.
- Separate claims from evidence.
- Preserve LaTeX compilation.
- Do not rewrite the whole paper unless explicitly requested.
- Prefer small, reviewable edits.

## File layout

```
papers/
├── AGENTS.md
├── README.md
└── oficial/
    ├── benchmarking-slm-spanish-obstetric-qa.tex
    ├── benchmarking-slm-spanish-obstetric-qa.pdf
    ├── references.bib
    ├── figures/
    │   ├── ft-vs-lora.pdf
    │   ├── rag-types-v2.pdf
    │   └── archive/
    │       ├── execution-runtime.png
    │       ├── inference-pipeline.pdf
    │       ├── lora-training.pdf
    │       ├── ragas-eval-workflow.pdf
    │       └── rag-types.pdf
    ├── submission/
    │   └── ISCMI2026-VA116-revised.pdf
    └── templates/
        └── IEEE-conference-template.docx
```

- `oficial/`: manuscript source, build output, bibliography, and figures.
- `oficial/figures/`: figure assets referenced by the current build.
- `oficial/figures/archive/`: assets not referenced by the current build, retained for provenance.
- `oficial/submission/`: material exchanged with the venue; `ISCMI2026-VA116-revised.pdf` is the reviewer-returned revision, supplied without its LaTeX source.
- `oficial/templates/`: IEEE-provided Word template, reference only. Kept outside `submission/` so packaging cannot include it by accident.

## Naming convention

This is a repository convention derived from IEEE submission-system constraints, not an IEEE-mandated standard.

1. ASCII only: `a-z`, `A-Z`, `0-9`, `-`, `_`. No spaces, colons, parentheses, accents, or duplicate-download suffixes.
2. Manuscript source and built PDF share one basename, so `latexmk` writes the PDF next to the source.
3. The manuscript slug derives from the paper title, not from the repository or project name: lowercase kebab-case, abbreviated where the title is long, with no venue and no year. `benchmarking-slm-spanish-obstetric-qa.{tex,pdf}` stands for "Benchmarking General and Medical Small Language Models for Spanish Obstetric Question Answering". Venue identity belongs to `submission/`, so resubmitting elsewhere does not force a rename.
4. Venue artifacts keep the official uppercase venue acronym and paper ID: `ISCMI2026-VA116-revised.pdf`.
5. Figure assets use lowercase kebab-case descriptive names: `ft-vs-lora.pdf`, `rag-types-v2.pdf`.
6. Build artifacts are never committed.

## Build and verification

Run from `papers/oficial/`:

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error benchmarking-slm-spanish-obstetric-qa.tex
```

Manual sequence:

```bash
pdflatex benchmarking-slm-spanish-obstetric-qa.tex
bibtex benchmarking-slm-spanish-obstetric-qa
pdflatex benchmarking-slm-spanish-obstetric-qa.tex
pdflatex benchmarking-slm-spanish-obstetric-qa.tex
```

Requires a TeX Live installation providing `IEEEtran.cls` and `IEEEtran.bst`. They are not vendored here; `.gitignore` excludes `papers/**/IEEEtran.cls` and `papers/**/IEEEtran.bst`.

A build is acceptable when it exits 0, produces 6 pages, reports no undefined references or citations, and reports no overfull hboxes. A change to the `.tex` must be followed by a rebuild of the committed `benchmarking-slm-spanish-obstetric-qa.pdf`.

## Figures

| Asset | Figure | Content |
|-------|--------|---------|
| `figures/ft-vs-lora.pdf` | Figure 1 | Full fine-tuning versus LoRA. |
| `figures/rag-types-v2.pdf` | Figure 2 | No RAG, Hybrid, and independent HyDE retrieval alternatives. |

Unused assets move to `figures/archive/` instead of being deleted. Files there are not referenced by the build.

## Bibliography workflow

When adding references:
1. Verify the source using a reliable academic index or publisher page; prefer DOI-based metadata from Crossref, Semantic Scholar, OpenAlex, or arXiv.
2. Update `papers/oficial/references.bib`; do not invent missing fields.
3. Use BibTeX keys in the format `lastnameYearKeyword`.
4. Every citation used in `.tex` must exist in the bibliography, and every bibliography entry must be traceable to a reliable academic source.

The build uses `\bibliographystyle{IEEEtran}` with `\bibliography{references}`, resolving to `papers/oficial/references.bib`.

## Version control

Never commit build artifacts: `*.aux`, `*.bbl`, `*.blg`, `*.out`, `*.toc`, `*.fls`, `*.fdb_latexmk`, `*.synctex.gz`, `*.log`. Only the source, the built PDF, the bibliography, the figures, and the venue material are tracked.

External material lives in `submission/` and `templates/`. Redistribution scope is defined by `NOTICE` and `LICENSE` at the repository root.
