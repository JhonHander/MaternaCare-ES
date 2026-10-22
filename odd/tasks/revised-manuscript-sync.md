# Sync manuscript with ISCMI revised PDF

## Objective

Make `papers/oficial/Benchmarking General and Medical Small Language Models for
Spanish Obstetric Question Answering: The Impact of Fine-Tuning.tex` carry the
same information as the reviewer-returned `papers/oficial/ISCMI_VA116_revised
(2).pdf`, which was supplied without its LaTeX source.

## Problem and why

The professor returned a "corrected" PDF but no `.tex`. The local manuscript is
older than that PDF, so the two disagree. Without a sync, any further editing
would silently drop the reviewer's additions.

## Scope

- Source of truth: text extracted from the revised PDF (`pdftotext -layout`).
- Target: the existing `.tex` only. No rewriting, no new claims, no new
  citations, no changes to results or reference list.
- Out of scope: fixing the reviewer's remaining defects (separate request), any
  bibliography change, any figure change.

## Constraints

- `papers/AGENTS.md`: never invent results or citations, preserve LaTeX
  compilation, prefer small reviewable edits.
- Numbers must be copied verbatim from the revised PDF, including the CIs.
- Table numbering must stay sequential (I, II, III, IV, V) and every in-text
  table reference must resolve through `\ref`.

## Tasks

- [x] T1 Extract the revised PDF text and compute a word-level diff against the
      current PDF build to enumerate the true content delta.
- [x] T2 Add the approximate-marginal-95%-CI method paragraph to the Analysis
      Plan, with `$\bar{x} \pm t_{0.975,n-1} s/\sqrt{n}$`.
- [x] T3 Add Results subsection "Uncertainty of Answer Correctness" plus
      Table IV (Answer Correctness mean [95% CI], both panels).
- [x] T4 Add Results subsection "Illustrative Grounded-Answer Audit" plus
      Table V (E1-E3 auxiliary audit, English summaries).
- [x] T5 Add the Discussion paragraph stating the auxiliary cases establish
      neither overfitting nor a causal explanation.
- [x] T6 Rewrite "Limitations and Future Work" to the revised wording about
      marginal intervals, clustering, selection bias and evaluator variability.
- [x] T7 Verify compilation: 8 pages, 0 overfull boxes, all 20 citations and
      all table cross-references resolved.
- [x] T8 Commit the work unit.

## Verification evidence

- `pdflatex`/`bibtex`/`pdflatex`/`pdflatex` in a scratch copy: exit 0, no `!`
  errors, no undefined references, 0 overfull hboxes.
- Word-level diff between the new build and the revised PDF: residual
  differences are confined to the two-column reference interleaving; body text
  matches.
- Page count 8, matching the revised PDF (was 9 before raising
  `\setcounter{dbltopnumber}` to 2 so Tables IV and V share the page top).

## Route and rationale

Direct inline single-file edit. The delta was established before any write, so
no mapping or writer delegation applied.

## Accepted changes beyond a literal transcription

- `master_eval.csv` and `sft_grounded` wrapped in `\code`, matching the
  manuscript's existing convention for technical identifiers.
- Table V columns set with `>{\raggedright\arraybackslash}p{...}`; the revised
  PDF shows that column ragged-right, and justified narrow columns stretch the
  `E1:` label.
- `dbltopnumber` raised from 1 to 2, with a comment, to avoid a near-empty
  ninth page holding only Table V.

## Next steps

- Review the reviewer's remaining defects in the revised text (separate task).
- Decide whether the conclusions' "six of eight" phrasing matches Table III.
