# Compact the manuscript without cramping it

## Objective

Reduce the PDF length of the ISCMI manuscript while keeping it readable, by
fixing layout-level waste: an oversized display equation, two full-width tables
whose content does not need full width, and a redundant sentence that pushed a
float straddle across a page break.

## Problem and why

The manuscript was 8 pages with five full-width tables and one figure. Two of
those tables (I and II) were mostly repetition: Table II printed the same value
in both model columns on 17 of 18 rows, and Table I restated in prose what its
own factor columns already encode. Full width bought nothing there and cost
vertical space on every page it touched.

## Scope

- Single file: `papers/oficial/Benchmarking General and Medical Small Language
  Models for Spanish Obstetric Question Answering: The Impact of Fine-Tuning.tex`.
- Layout and typography only. No experimental value, claim, citation, caption
  meaning, or section order changes.
- Table III, IV and V stay full width: they carry 8-9 columns of numbers that
  cannot be narrowed without cramping.

## Constraints

- Every numeric value and identifier from Table II must survive verbatim,
  either in a column or in the table note.
- No dangling `\ref`; no renumbering surprises.
- Compilation must stay clean: no `!` errors, no undefined references, no
  overfull hbox.
- `papers/AGENTS.md`: small reviewable edits, never invent results.

## Tasks

- [x] T1 Compact Equation 2: `\small`, `\jot` 3pt to 1pt, and `B(W)`/`P(R)`
      sharing a row. Five rows became four.
- [x] T2 Convert Table II to a single-column table headed `Gemma 4 E2B` /
      `MedGemma 1.5 4B`, with every shared hyperparameter moved into the note.
- [x] T3 Convert Table I to a single-column table, dropping the redundant
      `Condition definition` column and defining the factor levels in the note.
- [x] T4 Re-tune floats and measure after each change.
- [x] T5 Audit the remaining layout and record what is left as text-level
      (content) options instead of layout ones.
- [x] T6 Commit the work unit.

## Results

| Change | Pages |
| --- | --- |
| Baseline (after Fig. 2/3 removal) | 8 |
| Equation 2 compacted | 8 |
| Table II single column | 7 |
| Table I single column, `l` columns | 7 |
| Final (redundant Table II sentence removed) | **7** |

## Verification evidence

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

## Accepted changes beyond the literal request

- `\label{sec:qlora}` and `\label{sec:rag-protocol}` added so Table I's note can
  cross-reference subsections without hard-coding "Section II-E"/"II-F".
- Dropped the sentence `Table~\ref{tab:qlora-config} summarizes the training
  configuration used to produce the evaluated adapters.` It duplicated the
  Table II pointer three lines above and was the clause that straddled the page
  break. `\needspace` was tried first and cost a whole extra page.
- Reworded the earlier Table II pointer to "summarizes the configuration used
  for both adapters, including the shared quantization and BF16 computation
  settings", which is what the table now actually does.

## Remaining audit findings (not applied)

- Page 7 is filled with the reference list, so 6 pages is not reachable by
  layout alone.
- The real remaining length is textual: the abstract restates every top result,
  the Discussion restates the Results numbers, and the Conclusions restate them
  again. Trimming that is a content decision, not a layout one; roughly 0.5-0.8
  page is available there.

## Route

Direct inline, single file. The delta was fully understood before the first
write, so no mapping or writer delegation applied.
