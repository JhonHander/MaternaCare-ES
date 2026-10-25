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
3. The manuscript slug derives from the paper title, not from the repository or
   project name: lowercase kebab-case, abbreviated where the title is long, with
   no venue and no year:
   `benchmarking-slm-spanish-obstetric-qa.{tex,pdf}`.
   Venue identity lives in `submission/`, so a resubmission does not force a
   rename.
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
    ├── benchmarking-slm-spanish-obstetric-qa.tex            # manuscript source of truth
    ├── benchmarking-slm-spanish-obstetric-qa.pdf            # build output (committed)
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

- [x] T1 Move and rename the manuscript source and PDF to
      `benchmarking-slm-spanish-obstetric-qa.{tex,pdf}` with `git mv`.
- [x] T2 Move venue material into `submission/` and `templates/` with `git mv`.
- [x] T3 Archive the five unused figures under `figures/archive/`.
- [x] T4 Delete orphan build artifacts: `Benchmarking ...*.{aux,bbl,blg,...}`,
      `MaternaCare_ES_with_QLoRA_table.*`, `figures/rag-types.{aux,log}`, and the
      stray root-level `texput.log`.
- [x] T5 Stage `figures/rag-types-v2.pdf` so a fresh clone compiles.
- [x] T6 Rebuild the PDF from the renamed source; verify exit 0, 6 pages, no
      undefined references, and text identical to the pre-move build.
- [x] T7 Write `papers/README.md` and rewrite `papers/AGENTS.md` around the real
      paths, the build command and the naming convention.
- [x] T8 Update root `README.md` so the repository tree and documentation table
      match the new layout; confirm root `AGENTS.md` needs no change.
- [x] T9 Commit the work unit.
- [x] T10 Rename the manuscript to a title-derived slug after review feedback:
      `maternacare-es-iscmi2026.{tex,pdf}` ->
      `benchmarking-slm-spanish-obstetric-qa.{tex,pdf}` with `git mv`, then
      realign `papers/AGENTS.md`, `papers/README.md` and this document.

## Superseded decision

T1 named the manuscript after the repository (`maternacare-es`) plus venue and
year. Review feedback rejected that: the project name does not appear in the
paper title, so the basename described the repository rather than the paper, and
encoding the venue made every resubmission a rename. T10 supersedes T1's
basename; every other decision in this document still holds.

The replacement derives from the title, "Benchmarking General and Medical Small
Language Models for Spanish Obstetric Question Answering": `slm` is the
manuscript's own abbreviation for small language models, and venue identity moved
entirely to `submission/ISCMI2026-VA116-revised.pdf`.

## Verification evidence

- `git mv` used for all nine moves; `git status` reported them as renames, so
  history follows each file.
- The `.tex` content is byte-identical to the pre-move working tree: the diff
  against the pre-move `HEAD` blob is still 155 insertions / 179 deletions, the
  same delta that was already uncommitted before this work unit. Renaming
  authored nothing.
- `latexmk -pdf -interaction=nonstopmode -halt-on-error
  benchmarking-slm-spanish-obstetric-qa.tex` from `papers/oficial/`: exit 0, output
  `benchmarking-slm-spanish-obstetric-qa.pdf (6 pages, 333842 bytes)`.
- `pdfinfo`: 6 pages, 612 x 792 pts (US Letter), same size as the pre-move
  build.
- `pdftotext -layout` diff between the pre-move build and the rebuilt PDF:
  empty.
- Build log: 0 overfull hboxes, no undefined control sequences, no undefined
  references, no citation warnings.
- `git status` after the commit: no untracked or modified file under `papers/`.
  The two remaining working-tree entries (`odd/tasks/concise-methodology.md`
  modified, `odd/tasks/stix-two-uniform-fonts.md` untracked) belong to separate
  in-flight work and were deliberately left untouched and uncommitted.
- `grep -rn` for the retired basenames outside `odd/` and `.git`: no matches.
  The surviving references are inside `odd/tasks/*.md` historical records, left
  as written.
- `python -m unittest discover -s tests -v` is not applicable: no Python code,
  fixture or canonical snapshot changes in this work unit.
- T10 rename verified in an isolated copy under `/tmp/opencode/rebuild-check` so
  the committed PDF bytes were never rewritten: `latexmk` exit 0, 6 pages,
  612 x 792 pts, 0 overfull hboxes, no undefined references or citations, and
  `pdftotext -layout` identical to the committed PDF. `pdfinfo` shows no
  `maternacare` string inside the PDF, so the rename is a pure `git mv` with no
  byte change.

## Route and rationale

- Moves, artifact cleanup and the PDF rebuild ran inline: mechanical,
  already-understood, and verifiable by a single build.
- The two documentation files were delegated to one writer with a closed fact
  sheet, then read back and checked by the parent: every stated path exists, the
  eight original rules and four bibliography steps survived, and the writer
  marked the naming convention as a repository convention rather than an IEEE
  standard. The writer's only correction was dropping an unsupported
  "superseded by" claim about `figures/archive/rag-types.pdf`.
- Root `README.md` was edited inline: one tree block and one table cell, no
  research needed. Root `AGENTS.md` already deferred to `papers/AGENTS.md` and
  named no stale path, so it was left unchanged rather than churned.

## Review status

Receipt-driven development is enabled for the clone (`status` reports
`on`, decided by `default`). The work-unit commit `ee57ee7` was assessed with
`gentle-ai review assess --base-ref c2eadae --committed-only`: `risk: high`,
`review_due: true`, reason `unassessable` because the worktree holds untracked
files that require an explicit declaration.

The mandated preflight then returned a typed unavailable result, not a review:

```
code: immutable_review_transport_unsupported
message: The active runtime cannot provide immutable receipt-review transport.
phase: preflight
next_action: stop
```

No START was issued, no transaction exists for this candidate, and nothing was
started. `gentle-ai review mode disable` was not run: the review switch is
user-owned, and this run does not act on it.

## Next steps

- Decide the review switch: the current runtime cannot carry immutable receipt
  review, so `gentle-ai review mode disable --scope clone --cwd <repo>` is the
  documented way out if reviews should stop being queued here. It was not run.
- Push and open the PR when ready; delivery is not authorized by this document.
- This document was realigned to the T10 basename. Other `odd/tasks/*.md`
  records may still mention earlier manuscript basenames; those are historical
  records and were intentionally not rewritten.
