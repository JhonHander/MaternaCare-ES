# Compact the manuscript without cramping it

## Objective

Reduce the PDF length of the ISCMI manuscript while keeping it readable, by
fixing layout-level waste: an oversized display equation, two full-width tables
whose content does not need full width, and a redundant sentence that pushed a
float straddle across a page break.

Current correction: restore Table II's parameter rows in two columns and make
Table I and its note span the available column width. Readability and complete
rows take precedence over preserving the previous page count.

## Problem and why

The manuscript was 8 pages with five full-width tables and one figure. Two of
those tables (I and II) were mostly repetition: Table II printed the same value
in both model columns on 17 of 18 rows, and Table I restated in prose what its
own factor columns already encode. Full width bought nothing there and cost
vertical space on every page it touched.

## Scope

- Manuscript: `papers/oficial/Benchmarking General and Medical Small Language
  Models for Spanish Obstetric Question Answering: The Impact of Fine-Tuning.tex`,
  its tracked PDF, and this existing task document only.
- Layout and typography only. No experimental value, claim, citation, caption
  meaning, or section order changes.
- Table III, IV and V stay full width: they carry 8-9 columns of numbers that
  cannot be narrowed without cramping.
- T7 changes only Tables I and II. Preserve Equation 2, Figure 1, Tables III-V,
  citations, scientific prose, margins, global fonts, reference PDF and lockfiles.

## Constraints

- Table II must retain all 18 original parameter rows from `c753f5c^`, with
  exactly two columns: Parameter and Shared setting. Do not hide settings in
  the note. The base-model cell must distinguish both full source identifiers.
- Keep QLoRA in the title. Explain that shared settings apply to Gemma 4 E2B
  and MedGemma 1.5 4B, without appending QLoRA to those human names.
- Table I remains single-column; its tabular and meaningful note must both
  span `\columnwidth`, preserving C01-C12 and all factor values.
- No dangling `\ref`; no renumbering surprises.
- Compilation must stay clean: no `!` errors, no undefined references, no
  overfull hbox.
- `papers/AGENTS.md`: small reviewable edits, never invent results.

## Tasks

- [x] T1 Compact Equation 2: `\small`, `\jot` 3pt to 1pt, and `B(W)`/`P(R)`
      sharing a row. Five rows became four.
- [ ] T2 Prior implementation in `c753f5c` invalidated by the user: moving
      shared hyperparameters into the note was not accepted. Superseded by T7.
- [ ] T3 Prior implementation partially invalidated: the single-column design
      and factor note remain, but natural-width tabular/note are rejected.
      Superseded by T7 for width only.
- [x] T4 Re-tune floats and measure after each change.
- [x] T5 Audit the remaining layout and record what is left as text-level
      (content) options instead of layout ones.
- [x] T6 Commit the work unit.
- [x] T7 Correct both table layouts as one bounded work unit, rebuild the PDF,
      verify all original rows and widths, inspect rendered pages, and commit
      only the authorized source/PDF/task-document changes. Proof below.

## Historical results reported for c753f5c (not current acceptance)

| Change | Pages |
| --- | --- |
| Baseline (after Fig. 2/3 removal) | 8 |
| Equation 2 compacted | 8 |
| Table II single column | 7 |
| Table I single column, `l` columns | 7 |
| Final (redundant Table II sentence removed) | **7** |

## Historical verification reported for c753f5c (superseded for Tables I/II)

- `pdflatex → bibtex → pdflatex → pdflatex` from a clean aux: exit 0, **7 pages**,
  **0 overfull hboxes**, no `!` errors, no undefined references.
- Rendered pages inspected as images: Table I and Table II now sit one per
  column at the top of page 3, each about a third of the height the full-width
  versions consumed. Fig. 1 heads the left column of page 4 with no gap.
- Every Table II value survives: the note lists `sft_grounded`, 5,093/306,
  4-bit NF4 double quantization, rank 16, alpha 16, dropout 0.05, all linear
  modules, 2e-4, batch 1 with 8 accumulation steps (effective 8), 2 epochs /
  1,274 steps, AdamW 8-bit, cosine, 1,024 tokens, packing disabled, seed 3407,
  plus both full repository ids.
- Table I still resolves C01-C12 to model, adaptation and retrieval, and the
  note defines Base, QLoRA, No RAG, Hybrid and HyDE with `\ref` to the two
  subsections instead of hard-coded section letters.

## Other prior changes retained, outside T7

- `\label{sec:qlora}` and `\label{sec:rag-protocol}` added so Table I's note can
  cross-reference subsections without hard-coding "Section II-E"/"II-F".
- Dropped the sentence `Table~\ref{tab:qlora-config} summarizes the training
  configuration used to produce the evaluated adapters.` It duplicated the
  Table II pointer three lines above and was the clause that straddled the page
  break. `\needspace` was tried first and cost a whole extra page.
- Reworded the earlier Table II pointer to "summarizes the configuration used
  for both adapters, including the shared quantization and BF16 computation
  settings". This inherited BF16 pointer is not authorization to add a new
  Table II value; T7 leaves the unrelated prose unchanged.

## Remaining audit findings (not applied)

- The prior assertion that page 7 is entirely references and six pages cannot
  be reached by layout alone is unverified and must not be treated as fact.
- The real remaining length is textual: the abstract restates every top result,
  the Discussion restates the Results numbers, and the Conclusions restate them
  again. Trimming that is a content decision, not a layout one; roughly 0.5-0.8
  page is available there.

## Route

Historical route: direct inline for `c753f5c`. Current route: delegated-direct,
one bounded executor/writer on `fix/figures-longer`; no child delegation,
network, remote work, push or PR. RDD remains on (default); the parent performs
assessment and independent checks. This executor does not invoke review.

## T7 preparation and write triggers

- Preparation: read the injected skills, `papers/AGENTS.md`, this document,
  current table source, and authoritative Table II source at `c753f5c^`.
- Before source write: update scope/acceptance here, mirror the full document
  with its repository-relative locator to Engram topic
  `odd/paper-length-reduction/tasks`, and read both back. Completed before
  source edits; initial mirror/readback: observation 3148.
- Write trigger: explicit user rejection of `c753f5c`'s Table II note-collapse
  and Table I natural width, plus authorization to rebuild the tracked PDF.
- Use existing standard LaTeX width constructs only; no whole-paper redesign.
- TDD: not applicable to passive LaTeX layout; no Python behavior changes or
  TDD configuration. Runtime harness: N/A, no application runtime boundary.
- Required proof: fresh `/tmp/opencode/table-correction-build`, source copied
  as `paper.tex`, bibliography copied, figures symlinked; foreground
  `pdflatex -interaction=nonstopmode -halt-on-error paper.tex`, `bibtex paper`,
  then the same pdflatex command twice; `pdfinfo paper.pdf`;
  `pdftotext -layout paper.pdf paper.txt`;
  `grep -nE '^!|Overfull|undefined' paper.log` (exit 1 means no matches).
- Inspect extracted Tables I/II and render their pages at 130 dpi using
  `pdftoppm -f N -l N -r 130 -png paper.pdf tables`; inspect images for full
  Table I/note width, complete readable Table II, and no column collisions.
- Copy the PDF to the tracked manuscript path only after clean proof.
  Run `git diff --check` and verify the change boundary before committing.
- Rollback boundary: only the two table blocks, rebuilt manuscript PDF, and
  this correction's tracking entries; retain all valid earlier layout work.
- Commit source/PDF as one Conventional Commit, then record its exact identity
  here in a small tracking commit. The 400-line heuristic is advisory only.

## T7 evidence

- Build directory: `/tmp/opencode/table-correction-build`; source copied as
  `paper.tex`, `references.bib` copied, figures symlinked to the repository.
- All four foreground stages exited 0 in the prescribed order: pdflatex,
  bibtex, pdflatex, pdflatex (all LaTeX runs used
  `-interaction=nonstopmode -halt-on-error paper.tex`).
- `pdfinfo paper.pdf`: **8 pages**, letter size, 366,208 bytes.
- `pdftotext -layout paper.pdf paper.txt`: exit 0. Read both complete tables:
  all 12 C01-C12 factor rows and all 18 parameter rows present, no missing
  values, replacement glyphs, or unresolved `??` references.
- `grep -nE '^!|Overfull|undefined' paper.log`: no matches, expected exit 1.
  The final build has no errors, overfull boxes or undefined references.
  Underfull box warnings remain outside the changed table blocks.
- Read-only Python structural assertions: **PASS**. All 18 original parameter
  labels match `c753f5c^`; all 17 shared values match both original value
  columns exactly; both full base-model IDs remain distinct and labeled.
  Table I's 12 rows and note are unchanged; its tabular uses `columnwidth`.
  Source outside the two table blocks is byte-for-byte unchanged from
  `c753f5c`, including Equation 2, Figure 1 and Tables III-V.
- `pdftoppm -f 3 -l 3 -r 130 -png paper.pdf tables`: exit 0. Inspected
  `/tmp/opencode/table-correction-build/tables-3.png`: Table I rules and note
  span the full left column; Table II has exactly two readable columns and
  all rows, with model identifiers wrapped inside one setting cell. No column
  collisions, missing glyphs or broken subsection references were visible.
- Copied the clean PDF to the tracked manuscript path; `git diff --check`:
  exit 0. Diff is limited to the two table blocks, manuscript PDF and this
  document. No reference PDF or lockfile changed.
- TDD/Python tests and application runtime harness: N/A (passive LaTeX only).
  No required build/layout check skipped. The optional academic-paper workflow
  entrypoint was absent from the injected skill installation; the exact
  requested SKILL.md was loaded and manuscript fidelity rules were followed.
- Source/PDF correction commit:
  `4357d06ffa2839df76c779835b9a8b380b7c75e7`
  (`fix(paper): restore parameter rows and full-column table width`).
  The following tracking-only commit records this exact identity without
  self-reference. Parent assessment and independent spot-check remain pending;
  no user acceptance or RDD review is claimed.
