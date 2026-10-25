# Organize `papers/oficial/` for repository publication

## Objective

Leave `papers/oficial/` in a state that can be pushed as-is: ASCII-safe,
IEEE-compatible file names, a single unambiguous manuscript source/build pair,
venue material separated from authored material, no committed build residue, and
project documentation that points at the real paths.

## Problem and why

`papers/oficial/` accumulated three generations of work without a layout:

1. The manuscript basename is the full paper title, containing spaces and a
   colon (`Benchmarking ... Answering: The Impact of Fine-Tuning`). The colon is
   a reserved character on Windows and breaks shell, Makefile and URL handling;
   spaces force quoting in every command and in every editor/CI integration.
2. `MaternaCare_ES_with_QLoRA_table.*` are orphan build artifacts of a source
   file that no longer exists (committed rename `367c6d9`).
3. `figures/rag-types-v2.pdf` is referenced by the manuscript but is untracked,
   so a fresh clone cannot compile. `figures/rag-types.{aux,log}` are stray
   build residue inside the asset directory.
4. The reviewer-returned PDF keeps its browser duplicate-download name
   (`ISCMI_VA116_revised (2).pdf`).
5. Five legacy diagrams no longer referenced by the manuscript sit mixed with
   the two figures the build actually uses.
6. `papers/AGENTS.md` names `MaternaCare_ES_with_QLoRA_table.tex` as the
   manuscript, which is stale. Root `README.md` links to `papers/README.md`,
   which does not exist (deleted in `90e1d8e`), so the documentation table has a
   dead entry.

## Scope

- Names and locations under `papers/oficial/` only, plus the documentation that
  points at them (`papers/AGENTS.md`, new `papers/README.md`, root `README.md`).
- No manuscript content change: the `.tex` bytes move unchanged, and the rebuilt
  PDF must be text-identical to the current 6-page build.
- No deletion of authored material. Legacy figures are archived, not removed.
- No edit to `odd/tasks/*.md` historical records; they are evidence of past
  work and are left as written.

## Constraints

- `papers/AGENTS.md`: never invent citations or results, preserve LaTeX
  compilation, prefer small reviewable edits.
- Root `AGENTS.md`: `papers/` rules govern this area.
- IEEE does not standardize working source file names. What IEEE submission
  systems do require is ASCII-only names, and camera-ready PDFs are normally
  named by venue paper ID (e.g. `xxx.pdf` / `<ID>-<suffix>.pdf`). The convention
  adopted here is derived from that requirement and must be documented as a
  repository convention, never as an IEEE-mandated filename standard.
- `git mv` for every move so history follows the file.

## Naming convention adopted

1. ASCII only: `a-z`, `A-Z`, `0-9`, `-`, `_`. No spaces, colons, parentheses,
   accents, or duplicate-download suffixes.
2. Manuscript source and its built PDF share one basename, so `latexmk` owns the
   `.pdf` next to the `.tex`.
3. Authored slugs are lowercase kebab-case including project, venue and year:
   `maternacare-es-iscmi2026.{tex,pdf}`.
4. Venue identifiers keep their official uppercase form and paper ID:
   `ISCMI2026-VA116-revised.pdf`.
5. Figure assets are lowercase kebab-case descriptive nouns:
   `figures/ft-vs-lora.pdf`, `figures/rag-types-v2.pdf`.
6. Build artifacts (`aux`, `bbl`, `blg`, `fdb_latexmk`, `fls`, `log`, `out`) are
   never committed; `.gitignore` already covers all of them.

## Target layout

```
papers/
├── AGENTS.md
├── README.md                                   # new: artifact index + build
└── oficial/
    ├── maternacare-es-iscmi2026.tex            # manuscript source of truth
    ├── maternacare-es-iscmi2026.pdf            # build output (committed)
    ├── references.bib
    ├── figures/
    │   ├── ft-vs-lora.pdf                      # used: Fig. 1
    │   ├── rag-types-v2.pdf                    # used: Fig. 2 (was untracked)
    │   └── archive/                            # unused, kept for provenance
    │       ├── execution-runtime.png
    │       ├── inference-pipeline.pdf
    │       ├── lora-training.pdf
    │       ├── ragas-eval-workflow.pdf
    │       └── rag-types.pdf
    ├── submission/
    │   └── ISCMI2026-VA116-revised.pdf         # reviewer-returned revision
    └── templates/
        └── IEEE-conference-template.docx       # IEEE Word template (reference)
```

`templates/` is deliberately outside `submission/`, so that zipping
`submission/` for the venue cannot include the IEEE template by accident.

## Tasks

- [ ] T1 Move and rename the manuscript source and PDF to
      `maternacare-es-iscmi2026.{tex,pdf}` with `git mv`.
- [ ] T2 Move venue material into `submission/` and `templates/` with `git mv`.
- [ ] T3 Archive the five unused figures under `figures/archive/`.
- [ ] T4 Delete orphan build artifacts: `Benchmarking ...*.{aux,bbl,blg,...}`,
      `MaternaCare_ES_with_QLoRA_table.*`, `figures/rag-types.{aux,log}`, and the
      stray root-level `texput.log`.
- [ ] T5 Stage `figures/rag-types-v2.pdf` so a fresh clone compiles.
- [ ] T6 Rebuild the PDF from the renamed source; verify exit 0, 6 pages, no
      undefined references, and text identical to the pre-move build.
- [ ] T7 Write `papers/README.md` and rewrite `papers/AGENTS.md` around the real
      paths, the build command and the naming convention.
- [ ] T8 Update root `README.md` so the repository tree and documentation table
      match the new layout; confirm root `AGENTS.md` needs no change.
- [ ] T9 Commit the work unit.

## Verification plan

- `latexmk -pdf -interaction=nonstopmode -halt-on-error` from `papers/oficial/`,
  expecting exit 0 and exactly 6 pages (`pdfinfo`).
- `pdftotext` diff between the pre-move build and the rebuilt PDF: must be
  empty.
- `git status` clean of untracked paper assets; `grep -rn` for the old basenames
  must only hit `odd/tasks/` historical records.
- `python -m unittest discover -s tests -v` is not applicable: no Python code
  or fixture in this work unit changes.

## Delivery forecast

Renames plus three documentation files; well under the ~400 authored-line
planning heuristic. Single work unit, no chained PR.

## Route and rationale

File moves and the PDF rebuild are mechanical and already-understood, so they
run inline. Documentation is delegated to one writer with the fact package above
and verified by the parent against the actual tree.
