# Keep only Fig. 1 in the manuscript

## Objective

Reduce the manuscript to a single figure (Fig. 1, the full fine-tuning vs LoRA
comparison) by removing the RAG-variants figure and the RAGAS-workflow figure
from the paper body, leaving no dangling `\ref` behind.

## Problem and why

The paper carried three single-column figures. Two of them (RAG variants and
the RAGAS workflow) duplicate what the surrounding prose already states and
consume column space that the results tables need. Removing them frees room for
the remaining figure to be enlarged later on this branch.

## Scope

- `\subsection{Retrieval-Augmented Generation Protocol}` lead paragraph: drop
  the sentence that announced the removed RAG-variants figure.
- `\subsection{Evaluation Framework and Metrics}` lead paragraph: drop the
  sentence that announced the removed RAGAS-workflow figure.
- Delete both `figure` environments with their comments.
- Keep `figures/ft-vs-lora.pdf` and `\label{fig:qlora}` untouched.
- Do NOT delete the image assets from `figures/`; they stay available for the
  later enlargement step.

## Constraints

- `papers/AGENTS.md`: preserve LaTeX compilation, small reviewable edits, do not
  rewrite the paper.
- No figure may be replaced by prose that states a new claim; only the
  figure-announcing sentence goes away.

## Tasks

- [x] T1 Create branch `fix/figures-longer` from `paper/revised-sync`.
- [x] T2 Remove the RAG-variants figure block (`figures/rag-types.pdf`,
      `\label{fig:rag-types}`) and its announcing sentence.
- [x] T3 Remove the RAGAS-workflow figure block
      (`figures/ragas-eval-workflow.pdf`, `\label{fig:ragas-eval-workflow}`) and
      its announcing sentence.
- [x] T4 Verify that only `fig:qlora` survives and that the two affected
      paragraphs still read coherently.
- [x] T5 Recompile and confirm no dangling reference.
- [x] T6 Commit the work unit.

## Verification evidence

- `grep -n "Fig\.\|fig:\|begin{figure}\|includegraphics"` after the edits returns
  only line 333 (`Fig.~\ref{fig:qlora}`), line 397 (`\begin{figure}[t]`), line
  399 (`figures/ft-vs-lora.pdf`), line 401 (`\label{fig:qlora}`).
- `pdflatex → bibtex → pdflatex → pdflatex`: exit 0, 8 pages, 0 overfull hboxes,
  no `!` errors, no undefined references.
- Rendered text: "...receives the question and context. Hypothetical text is
  used only for query expansion." then `1) Corpus Provenance...`; and
  "RAGAS 0.4.3 [18] is used as an external automatic evaluation layer.
  Response-quality, retrieval-quality, and operational measurement domains are
  kept separate before paired contrasts and interaction analysis." then
  `1) Retained Fine-Tuning-Output Evaluator`. No orphan figure mention.

## Route and rationale

Direct inline single-file edit; the two deletion sites were read before writing
and needed no delegation.

## Next steps

- Enlarge Fig. 1, which is what the branch name reserves room for.
