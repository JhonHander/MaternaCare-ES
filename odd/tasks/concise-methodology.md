# Concise, reproducible methodology

## Objective, problem, and rationale
Prioritize shortening the whole paper, especially Methods, without losing scientific content: repeated definitions,
tutorial material, and specialist implementation detail obscure the experimental design.
The user approved web-guided shortening and verified synchronization of the tracked PDF.
The latest direct instruction authorizes unnecessary formula deletion and selects
`feature-branch-chain`; it supersedes the obsolete appendix-versus-supplement question.
This remains the single feature document; create neither an appendix nor a supplement.

## Authorized scope and constraints
- Source: `papers/oficial/Benchmarking General and Medical Small Language Models for Spanish Obstetric Question Answering: The Impact of Fine-Tuning.tex`.
- PDF: the tracked companion with the same basename and `.pdf` extension.
- No experiments, result changes, bibliography changes, figure-asset changes, or styling changes.
- Preserve all quantitative tables, existing citations, and figure assets/typography.
- Results, Discussion, and Conclusions remain unchanged except necessary cross-reference adjustments.
- Generic LoRA figure inclusion may be removed; retain `figures/ft-vs-lora.pdf` itself.
- Delete unnecessary displayed/inline formulas and generic LoRA tutorial prose;
  retain concise explanations of study-specific choices, actual parameters, and controls.
- Existing method citations remain; citations cannot replace this study's custom settings.
- Preserve all other sessions' completed changes and existing work, including untracked
  `odd/tasks/stix-two-uniform-fonts.md` and the now-committed `odd/tasks/paper-editorial-cleanup.md`.
- Remain local: no push, PR, merge, downloads, or installations are authorized here.

## Source guidance and proposed structure
- Use the current source and retained experimental evidence, not defaults, as scientific authority.
- Previously web-researched editorial guidance: ICMJE manuscript preparation,
  https://www.icmje.org/recommendations/browse/manuscript-preparation/preparing-for-submission.html
- Nature formatting guide: https://www.nature.com/nature/for-authors/formatting-guide
- Nature ML checklist: https://www.nature.com/documents/machine-learning-checklist.pdf
- These inform concision and reproducibility; add no manuscript citations for editorial advice.
- Six Methods subsections: Design; Data/scenarios/splits; Models/QLoRA; Retrieval;
  Inference/reproducibility; Metrics/statistical analysis.
- Provisional target: 1,150–1,300 prose words, approximately 20–30% reduction;
  never force scientific-content loss to meet the target.
- Retain split integrity versus inference-time corpus access; both scenarios and their
  noncomparability; nonrandom first-10 selection; independently constructed HyDE;
  actual model/training configurations and tables; prompts/decoding; evaluator
  applicability, provenance uncertainty, and statistical uncertainty limits.
- Condense scoring, normalization, retrieval/cache detail in place, not into another artifact.
  Retain the custom clinical-score rules/weights and thresholds, normalization essentials,
  candidate-depth rule (the greater of four times final depth and 50, capped by corpus size), RRF constant
  60, final depth 5, stable-ID ties, independent HyDE/cache controls, and actual configurations.
  Delete mathematical exposition only when its scientific meaning survives in concise prose;
  retain interaction definitions and confidence-interval method/assumptions without tutorial derivations.

## Tasks, routing, and ownership
- [x] **ODD-01 — Remove unnecessary formulas and generic LoRA tutorial inclusion; condense implementation prose, retain essential settings/controls/citations, verify, and work-unit commit.**
  Route: delegated direct. Trigger: reading prepares writing and spans at least two
  nontrivial artifacts (manuscript and synchronized tracked PDF). No detail destination is created.
- [ ] **ODD-02 — Consolidate Methods into six subsections, eliminate repetition/tutorial material, retain proof, rebuild verified PDF, and work-unit commit.**
  Route: delegated direct. Trigger: reading prepares writing and spans at least two
  nontrivial artifacts (manuscript and tracked PDF, with retained-detail readback).
- Parent owns task progression, checkoff, review routing, and mandatory spot checks.
  No TODO grants review authority; this bookkeeping step launches no review actors.

## Acceptance and exact per-unit verification
- Preserve every protected scientific distinction above; verify tables/configuration,
  citations, concise custom-method descriptions, exact cross-references, and protected-section diffs.
- In an isolated fresh `/tmp/opencode/` directory, stage the source as `paper.tex`,
  copy `references.bib`, and symlink `figures` to the existing source figures directory.
- Run `pdflatex -interaction=nonstopmode -halt-on-error paper.tex`; `bibtex paper`;
  then run `pdflatex -interaction=nonstopmode -halt-on-error paper.tex` twice more.
- Run `pdfinfo paper.pdf`; `pdftotext -layout paper.pdf paper.txt`; `pdffonts paper.pdf`.
- Inspect the log for errors, undefined references/citations, overfull boxes,
  missing glyphs, and rerun requests; record exact outcomes, including underfull diagnostics.
- Run `pdftoppm -r 130 -png paper.pdf page`, inspect rendered pages, and run `git diff --check`.
- Copy only the checked PDF to the tracked destination after all checks; parent spot check
  is mandatory. Record exact commands/results and confirm source/PDF synchronization per unit.
- Historical base: 7 Letter pages, 7 underfull diagnostics, no errors/overfull/undefined;
  baseline page count freshly confirmed during ODD-01; baseline log diagnostics remain historical.
  ODD-01 build evidence below is editorial verification, not a new scientific result.

## Configuration and review boundaries
- TDD: no explicit activation found; effective mode unknown/not established, not globally off.
  RED/GREEN is inapplicable to passive editorial work; normal documentation checks remain required.
- Functional Python runner: `python -m unittest discover -s tests -v`; not planned for
  passive LaTeX-only changes absent executable impact. Runtime harness: N/A, no executable boundary.
- Read-only `gentle-ai review mode status`: RDD on, decided by default;
  global and clone-local unset. Preserve mode; no toggles. Native assessment is required:
  do not assume passive classification or an assessment/review outcome at tracking time.
- Historical branch: `fix/figures-longer`; initial review boundary:
  `81dca25a4cdce260f46c4fc3c35b92c900646be1`.
- Initial manuscript blob: `5d92eb8dd1b5586552103d97e7c0b63eeb771b05`.
  Read-only intake instead observed accepted cleanup HEAD
  `439a7e4bdd4fb4f25a6e5e576c8742b0b10d0556`, still on `fix/figures-longer`,
  source blob `f0ff1aa0b38f69a184b4327532258f3484b4aede`, and no tracked/index diff.
  Recheck branch, HEAD, source identity, and worktree before each write; stop on concurrent source change.

## Forecast, resolved decisions, and delivery
- Forecast: 410–585 authored changed lines (additions + deletions), including this document;
  generated PDF excluded. Approximately 400 lines is advisory only: no code-golf or artificial splitting.
- Delivery policy: `ask-on-risk`; the user has resolved its chain choice as
  `feature-branch-chain`. Use ODD-01 and ODD-02 as cohesive future work-unit/chain slices,
  each with its own verification and Conventional Commit; branch first under parent coordination.
  Recount actual authored additions/deletions per unit before determining delivery boundaries.
- Review remains pending; the parent authorized one ODD-01 work-unit commit on the feature branch.
- Detail placement is resolved: delete unnecessary formulas and condense essential prose in place;
  no appendix, supplement, or further placement question. No human-choice blocker remains.

## Read-only concurrency and overlap evidence
- The prior cleanup is now committed as `439a7e4` (36 source additions, 64 deletions),
  contrary to the dirty-source handoff. Working/index source diffs are empty at intake.
- Its scoped historical diff already removes redundant Table I/II notes, repeated scenario
  inputs and rankings, the unsupported BF16 table promise, and unsupported evaluator settings.
  Preserve its explicit evaluator-provenance uncertainty and metrics/identity distinction.
- It also edits the contribution, Discussion, and Limitations; Results and Conclusions
  are untouched in that diff. These are accepted baseline edits, not this feature's changes.
- At intake, formula blocks, generic LoRA figure inclusion, implementation prose, and the
  larger subsection structure remained. ODD-01 builds on this baseline; ODD-02 remains pending.
- Intake source SHA-256: `234dd37c442edc1d5118cd9cf423d69c465f6858db607a0d5e7dbbb222020d3f`.
  Intake PDF SHA-256: `b10af3bf15a0b685dc8e5f7e32e122ee89804a285a8d76e1a389cb0a41f8ea27`.
  These matched the cleanup document's final identities; no new build was claimed at intake.
- Before/after bookkeeping checks found the same HEAD, source blob, and source/PDF
  SHA-256 values; no source activity was observed during this interval, not a guarantee
  against another writer resuming. At that intake, the three named task documents were untracked.
- The parent created `docs/concise-methodology` at `439a7e4`. After the ODD-01 source edit,
  a guard detected HEAD `607e3e9d8ac6246a18f75b5e1d9687ca6155c0c2` and stopped the writer.
  Parent explicitly reconciled and authorized a bounded verification/proof continuation:
  that commit adds only the unrelated 115-line `odd/tasks/paper-editorial-cleanup.md`.
  Source blob remains `f0ff1aa0b38f69a184b4327532258f3484b4aede`; no overlapping source edit.
  Preserve that record commit; exclude its 115 lines from this feature's authored count.
  The reconciled initial review boundary for this feature is now `607e3e9`.
  Later documentation-only commits must be classified/reported without overwriting them;
  a later concurrent source edit requires stopping.

## Proof, progress, rollback, and next action
- `skill_resolution: paths-injected`: loaded academic-research-suite `SKILL.md`, its
  `ars/academic-paper/SKILL.md` revision entrypoint, and work-unit-commits `SKILL.md`
  from the injected paths. The academic-paper `WORKFLOW.md` path was absent; the available
  `SKILL.md` was used. No full-paper pipeline, child, assessment, or review was launched.
- **ODD-01 implementation/proof accepted by parent; review separately pending.**
  Parent completed structural readback and reran whitespace/PDF metadata checks (pass, 6 Letter pages).
  Parent authorized ODD-01 checkoff and one work-unit commit; ODD-02 remains unchecked and unstarted.
- ODD-01 replaces interaction, clinical-score, candidate-depth, output-rate and CI notation
  with prose, removes generic LoRA figure inclusion (not its asset), and condenses specialist
  implementation descriptions in place. All 15 Methods subsection/subsubsection headings remain.
- Protected scientific readback: clinical-term substring weights 1/2, action-term weight 1,
  cumulative word-count bonuses 2 at 120 and 350, reference-line penalty 3 at ratio 0.35,
  zero floor and normalization remain. Candidate depth remains the greater of four times
  final depth and 50, capped by corpus size; RRF 60, final depth five and stable-ID ties remain.
  Independent Spanish HyDE generation/model/cache identity and reuse controls remain.
  Matched 4-bit QLoRA settings remain in the unchanged table; sample/scenario distinctions,
  paired contrasts/interaction, Student-t marginal CI method and assumptions, unavailable
  paired tests and evaluator-provenance uncertainty remain. No new claims/settings/citations.
- Automated comparisons against `607e3e9` passed: pre-Methods prefix and Results-through-end
  suffix byte-identical; all four full table environments byte-identical; citation multiset
  unchanged (22 occurrences, 20 keys); all six tracked figure assets and bibliography match
  HEAD Git blobs. Removed figure/equation labels have no remaining references.
- Fresh build directory: `/tmp/opencode/concise-methodology-unit1-VzPTBV`.
  Source copied as `paper.tex`, bibliography copied as `references.bib`, and `figures`
  symlinked to the repository's existing figures directory. No repository auxiliary outputs.
  Preserved original baseline copies also reside in `/tmp/opencode/concise-methodology-unit1-gu1MHv`.
- Final source normalization retained existing line endings and formatting; no layout/preamble
  changes. The authorized source SHA below was unchanged throughout verification and PDF copy.
- Required foreground commands and observed results:
  - `pdflatex -interaction=nonstopmode -halt-on-error paper.tex`: exit 0 (pass 1).
  - `bibtex paper`: exit 0, no warning; `bibtex.stdout` retained.
  - `pdflatex -interaction=nonstopmode -halt-on-error paper.tex`: exit 0 (passes 2 and 3).
    Each pass's stdout is retained as `pdflatex-pass1.stdout` through `pdflatex-pass3.stdout`.
  - `pdfinfo paper.pdf`: exit 0; 6 Letter pages (612 by 792 pt), 173,739 bytes, PDF 1.5.
  - `pdftotext -layout paper.pdf paper.txt`: exit 0; extracted text retained.
  - `pdffonts paper.pdf`: exit 0; all 12 listed fonts embedded/subset Type 1.
  - Final `paper.log`: no warnings, errors, undefined citations/references, overfull boxes,
    missing characters, or rerun requests; 5 underfull diagnostics (historical baseline 7).
    An initial overbroad grep wrapper exited 2 because it matched `rerunfilecheck` package
    informational lines, not a rerun request; a corrected actionable diagnostic filter found
    no matches (expected grep exit 1). No required build/render command failed.
  - `pdftoppm -r 130 -png paper.pdf page`: exit 0; all six `page-1.png` through `page-6.png`
    successfully read and visually inspected at full-page resolution. Tables and text are
    legible, with no observed overlaps, clipped content, missing glyphs, or blank pages.
  - `git diff --check`: exit 0 before PDF copy and after proof update; untracked-document
    whitespace check emitted no diagnostics (expected `git diff --no-index --check` exit 1).
- Same explicit approximate Methods prose count: **1,562 to 1,470 words (-5.89%)**.
  Restrict to Methods between section markers; remove unescaped-percent comments,
  table/figure/equation/align environments including captions, dollar-delimited inline math,
  section/subsection/subsubsection/cite/label/ref/eqref commands and arguments, then remaining
  command names. Retain other braced arguments including code identifiers; count ASCII
  alphanumeric words with internal hyphens/apostrophes. This is not a linguistic word count.
  `wordcount-method.txt` and `scope-proof.json` retain method/results. The provisional
  1,150–1,300 target is not met by ODD-01 alone; do not claim ODD-02 restructuring completed.
- Whole PDF: **7 to 6 pages**; baseline page count freshly observed with `pdfinfo baseline.pdf`.
  Only the verified generated `paper.pdf` was copied to the tracked companion PDF.
  Source/PDF synchronization confirmed by byte comparison and matching SHA-256 identities:
  - Source: `158b3390a24bce6cfe836be0fbc3ce749baa86dfd409a1a1d92f841c14d72cdd`.
  - PDF: `a1240615df95f966af390f80f6d56db843167c2fb9124791a7fd195972021855`.
- Functional Python suite `python -m unittest discover -s tests -v`: skipped/N/A for
  passive LaTeX-only edits with no executable impact; runtime harness N/A for the same reason.
  TDD activation remains unknown/not established; no invented off setting, RED/GREEN, or runtime claim.
- Source diff: 48 additions + 102 deletions (150 authored lines), plus this new feature document.
  Record the actual committed authored count below; exclude PDF and unrelated 115-line commit.
  Approximately 400 lines remains advisory; no artificial slicing or minification.
- After each accepted work-unit commit, record its hash and proof here and mirror the full document.
  ODD-01 commit identity will be appended after creation; its receipt cannot be in its own commit.
- Engram mirror contract: project `MaternaCare-ES`, topic `odd/concise-methodology/tasks`,
  full content plus repository-relative locator `odd/tasks/concise-methodology.md`;
  read both copies back before claiming mirror success; if unavailable, preserve local and mark pending.
- Roll back only this feature's exact edits/files and generated companion PDF; preserve prior work,
  bibliography, figure assets and `607e3e9` record commit. Exact rollback boundary: restore only
  this manuscript's ODD-01 diff and companion PDF from `607e3e9`, and remove this feature document
  if the feature is abandoned; no executable behavior is involved. Never reset unrelated work.
- Next: create the parent-authorized work-unit commit, then append its identity as an unstaged receipt.
  Parent owns subsequent native review under unchanged RDD policy; no assessment/review here.
  Authorized Conventional Commit: `docs(paper): condense methodological exposition`.
  Preserve ODD-02 for its separate authorized work unit and selected feature-branch chain.
