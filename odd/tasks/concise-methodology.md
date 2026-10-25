# Concise, reproducible methodology

## Objective, problem, and rationale
Run the user-authorized reversible two-figure layout trial within unfinished ODD-02: replace displayed
formulas with complete concise prose, restore the conceptual full-fine-tuning/LoRA comparison, and
rearrange the configuration table and retrieval overview for clear IEEE-style reading order.
Keep exactly six pages, six Methods subsections, legible captions/graphics and no overlaps.
Keep `feature-branch-chain` and this single feature document; no appendix, supplement, new task,
or product-choice roundtrip. Prior math-restoration acceptance describes a preserved earlier snapshot.

## Authorized scope and constraints
- Source: `papers/oficial/Benchmarking General and Medical Small Language Models for Spanish Obstetric Question Answering: The Impact of Fine-Tuning.tex`.
- PDF: the tracked companion with the same basename and `.pdf` extension.
- No experiments, result changes, bibliography changes, figure-asset changes, or styling changes.
- Preserve all quantitative tables, existing citations, and figure assets/typography.
- Results, Discussion, and Conclusions remain unchanged except necessary cross-reference adjustments.
- Include unchanged `figures/ft-vs-lora.pdf` as Fig. 1, ideally at the bottom of physical page 2;
  clarify QLoRA's frozen quantized base and that full fine-tuning was not an experimental arm.
- Move Table II to the old Fig. 1 position (page 3, left-column top); move the retrieval overview
  to Fig. 2 in the right column of page 3. Preserve all table payloads and both asset files.
- Replace displayed clinical-score/candidate-depth/interaction/CI formulas with complete prose,
  not full inline-formula substitutes. Keep useful explanations and six subsections/zero subsubsections.
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
- Local `papers/oficial/IEEE-Formatting.docx`, paragraph 79: top/bottom column placement, figure captions
  below, table titles above, cite before insertion; large items may span both columns. Paragraphs 35/95:
  preserve typography/layout; 8-point Times New Roman figure labels recommended. Existing assets use
  embedded non-Times fonts; preserve bytes and disclose that inherited typeface limitation, not redraw them.
- Six Methods subsections: Design; Data/scenarios/splits; Models/QLoRA; Retrieval;
  Inference/reproducibility; Metrics/statistical analysis.
- Provisional target: approximately 1,100–1,300 prose words remains advisory; exactly six pages
  with clearly improved last-page use is the priority. Never force filler or scientific-content loss.
- Retain split integrity versus inference-time corpus access; both scenarios and their
  noncomparability; nonrandom first-10 selection; independently constructed HyDE;
  actual model/training configurations and tables; prompts/decoding; evaluator
  applicability, provenance uncertainty, and statistical uncertainty limits.
- Condense scoring, normalization, retrieval/cache detail in place, not into another artifact.
  Retain the custom clinical-score rules/weights and thresholds, normalization essentials,
  candidate-depth rule (the greater of four times final depth and 50, capped by corpus size), RRF constant
  60, final depth 5, stable-ID ties, independent HyDE/cache controls, and actual configurations.
  Preserve study-specific definitions and assumptions in prose rather than displayed mathematics.
  Superseded 2026-10-25 by explicit user instruction: the retrieval overview caption is the short line
  `Retrieval alternatives: No RAG, Hybrid, and independent HyDE.`; the removed explanatory clauses
  remain in the Study Design and Retrieval prose, not in the caption.

## Tasks, routing, and ownership
- [x] **ODD-01 — Remove unnecessary formulas and generic LoRA tutorial inclusion; condense implementation prose, retain essential settings/controls/citations, verify, and work-unit commit.**
  Route: delegated direct. Trigger: reading prepares writing and spans at least two
  nontrivial artifacts (manuscript and synchronized tracked PDF). No detail destination is created.
- [ ] **ODD-02 — Trial two figures instead of displayed formulas; position Fig. 1/page 2 bottom, Table II/page 3 left top, Fig. 2/page 3 right; keep six sections/pages, verify and retain proof for an own-scope commit.**
  Route: delegated direct. Trigger: reading prepares writing and spans at least two
  nontrivial artifacts (manuscript and tracked PDF, with retained-detail readback).
- Parent owns task progression, checkoff, review routing, and mandatory spot checks.
  No TODO grants review authority; this bookkeeping step launches no review actors.

## Acceptance and exact per-unit verification
- Preserve every protected scientific distinction above; verify tables/configuration,
  citations, concise custom-method descriptions, exact cross-references, and protected-section diffs.
- Trial acceptance: exactly six pages, two legible single-column figures, no displayed formulas,
  no overlap/clipping, and requested physical placements verified by rendered pages and text boxes.
  Preserve table payloads; allow only local float flags/source movement/control, no typography hacks.
  One coherent draft plus at most two scoped placement adjustments before final source freeze.
  Protected baseline is the current verified `61118bfc` snapshot, including external Limitations;
  preserve a reversible TeX/PDF copy before edits and inspect every final page.
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
- RDD remains on by default; global and clone-local unset. No mode toggle or review by this writer.
  Parent-reported ODD-01 native workflow: initial assessment was unassessable because of
  unrelated untracked work. Selectorless STATUS returned `immutable_review_transport_unsupported`,
  `mutation_outcome: not_started`, `retry_safe: false`; no authority, transaction, START, or approval.
  Parent then assessed explicit scope excluding unrelated untracked work with inventory hash
  `sha256:82912b1aa401ce8b93c74177a78455da82679a1cf87a11d21fd0fa6d5833f256`.
  Accepted `gentle-ai.review-assessment/v1`: risk medium (`executable_change` on PDF),
  355 lines, 3 paths, `review_due: false`, `under_budget`. No captured v3 consent/decline exists.
  Native review remains unavailable, not approved; do not synthesize consent or a receipt.
  Delegated gate follows ordinary verification: writer self-verification and parent spotcheck,
  no mandatory separate verifier for this medium, non-small-model path. Parent trial assessment is recorded below.
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
- ODD-01 is committed; ODD-02 implementation/verification only is authorized, not staging or commit.
  Parent accepted the earlier math-restoration snapshot; the user now authorizes the two-figure trial.
  Trial implementation/verification and parent placement acceptance are observed; no stage or commit authorized.
  Native review remains unavailable, not approved.
  Final work-unit commit is pending concurrent edit ownership, not a new content-choice question.
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
  larger subsection structure remained. Both units build on this baseline without reverting cleanup.
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
  The reconciled ODD-01 assessment boundary is `607e3e9`; ODD-02 starts at `c2eadae`.
  Later documentation-only commits must be classified/reported without overwriting them;
  a later concurrent source edit requires stopping.

## Proof, progress, rollback, and next action
- `skill_resolution: paths-injected`: loaded academic-research-suite `SKILL.md`, its
  `ars/academic-paper/SKILL.md` revision entrypoint, and work-unit-commits `SKILL.md`
  from the injected paths. The academic-paper `WORKFLOW.md` path was absent; the available
  `SKILL.md` was used. No full-paper pipeline, child, assessment, or review by this writer.

### ODD-01 accepted unit
- Parent accepted complete structural readback and reran whitespace/PDF metadata checks.
  Formula-to-prose conversion and LoRA inclusion removal preserved all scientific controls.
- Isolated proof: `/tmp/opencode/concise-methodology-unit1-VzPTBV`; original baseline copies:
  `/tmp/opencode/concise-methodology-unit1-gu1MHv`. Required commands below all exited 0;
  six rendered pages inspected. Final log: 5 underfull, no actionable errors or warnings.
  An initial overbroad grep wrapper matched package info (exit 2); corrected filter passed.
- Protected comparisons against `607e3e9`: all non-Methods source, four tables, 22 citation
  occurrences/20 keys, bibliography and six figure assets unchanged; 15 Methods headings retained.
- Source SHA-256: `158b3390a24bce6cfe836be0fbc3ce749baa86dfd409a1a1d92f841c14d72cdd`.
  PDF SHA-256: `a1240615df95f966af390f80f6d56db843167c2fb9124791a7fd195972021855`.
  Whole PDF 7 to 6 Letter pages; 173,739 bytes. Methods prose 1,562 to 1,470 (-5.89%).

### ODD-01 commit receipt
- Commit: `c2eadae41df2edad2a6e7d57c90bb7b01b55c81c` (`docs(paper): condense methodological exposition`).
- Assessment base: `607e3e9d8ac6246a18f75b5e1d9687ca6155c0c2`; exactly the manuscript TeX/PDF and this document committed.
- Authored changes: 253 additions + 102 deletions = **355 lines** (source 150; new document 205); binary PDF excluded.
  Earlier `439a7e4` cleanup and unrelated `607e3e9` record commit are excluded from this feature count.
- This receipt was left unstaged after ODD-01 and is now part of ODD-02's pending document diff.

### Earlier ODD-02 snapshot: verified, superseded page-use objective
- Parent accepted scientific preservation and six-section structure at 947 Methods prose words.
  Isolated proof remains in `/tmp/opencode/concise-methodology-unit2-HVRSfI` (source `ff1ec3b3`, PDF `c1aec56a`).
  After reconciling the separately owned Limitations paragraph, combined proof remained in
  `/tmp/opencode/concise-methodology-combined-RCMGd2` (source `a4c6d60e`, PDF `9ce80903`).
  Both full builds passed; six pages inspected, 8 underfull, no actionable diagnostics. The combined
  snapshot is the protected baseline for the current revision, not an obsolete completion claim.

### Previous math-restoration snapshot: verified and parent-accepted, superseded by two-figure trial
- Parent accepted that snapshot and spotchecked metadata/whitespace/page six. Historical scoped
  assessment v1: medium (`executable_change` on PDF), 3 paths/535 lines including external 10,
  `review_due: false`, `under_budget`; ordinary fallback tier met, no native review approval/authority.
- Preserved full proof: `/tmp/opencode/concise-methodology-sixpage-w7HKmQ` (source `61118bfc`, PDF `be995b45`).
  Six Letter pages/313,774 bytes; all commands and six-page visual checks passed; 9 underfull, no actionable
  diagnostics. Methods 1,097 approximate prose words; page-six text envelope 80.90%, not ink/full coverage.
  This remains the reversible trial baseline, not current acceptance of the new layout.

### Current two-figure trial: verified and parent-accepted; own commit pending
- Parent independently inspected final pages 2/3 and accepted all requested positions, legibility/no overlap, and inherited asset-font limitation.
  Parent spotchecks passed: `git diff --check`; `pdfinfo` (6 Letter pages, 330,413 bytes); review mode on, unchanged.
  Pre-record scoped assessment v1 (exclude untracked, same inventory hash above): medium (`executable_change` on PDF), 3 paths/530 lines.
  `review_due: false`, `under_budget`; non-small writer checks plus parent readback/spotcheck complete the ordinary fallback tier.
  Known unsupported STATUS was not retried; native review remains unavailable, with no new authority, approval, or toggle.
- Read actual strict-OOXML guide and both assets before writing. Plan/full mirror matched before first
  source edit. Reversible baseline: `/tmp/opencode/ieee-two-figure-trial-8HxgIB/before.tex` and `before.pdf`.
  That folder retains extracted `ieee-guide.txt`, first draft and the one scoped float adjustment.
- The guide's paragraph 79 supports top/bottom column floats, captions below figures/titles above tables,
  and citation before insertion. Exact pages/columns come from the user's request, not a guide mandate.
  Final ordinary float queue uses Fig. 1 `[!b]`, Table II `[t]`, Fig. 2 `[t]`; no preamble, package,
  global style, font/margin, negative spacing, overlay, or hard page-break changes.
- Observed old/new anchors in PDF points from top-left (`placements.json`; caption/title words, not image edges):
  - Table II: page 2 right, (420.989, 53.506) to **page 3 left top**, (157.975, 53.506).
  - Retrieval overview: old Fig. 1 page 3 left, (48.964, 298.689), to **Fig. 2 page 3 right**, (311.978, 298.689).
  - Restored conceptual comparison: **Fig. 1 page 2 right bottom**, caption (311.978, 693.028).
    Graphic-text envelope y=432.525–680.399; caption y=693.028–718.087. Fig. 2 graphic-text envelope
    y=63.592–273.757, caption y=298.689–332.715. All requested physical placements met.
- Two figure environments/labels, zero display-math environments, six Methods subsections/zero subsubsections.
  Complete prose retains clinical weights/thresholds/normalization, candidate-depth/RRF/ties, fixed-scenario
  interaction and marginal-CI method/limits. Fig. 1 caption makes full fine-tuning conceptual, not an arm;
  QLoRA uses frozen quantized base weights. Fig. 2 retains independent-HyDE/query-versus-evidence controls.
- Final fresh directory: `/tmp/opencode/ieee-two-figure-final-ieo8KX`. Source frozen as `paper.tex`,
  bibliography copied and existing figures symlinked. Exact foreground sequence, all exit 0:
  `pdflatex -interaction=nonstopmode -halt-on-error paper.tex`; `bibtex paper`; same `pdflatex` twice;
  `pdfinfo paper.pdf`; `pdftotext -layout paper.pdf paper.txt`; `pdffonts paper.pdf`;
  `pdftoppm -r 130 -png paper.pdf page`; `git diff --check`.
- **Exactly 6 Letter pages**, 330,413 bytes, PDF 1.5. All six final PNGs read individually and inspected;
  figures, captions and table are legible, no image/image, image/caption or table/text overlap or clipping.
  Numbering/labels resolve; first text callouts precede insertion. Final log: **9 underfull**, no warnings,
  errors, undefined citations/references, overfull boxes, missing characters, or rerun requests.
  All fonts embedded/subset, including inherited Type 3 glyph fonts in the unchanged comparison asset.
  Asset labels are not strictly the guide's recommended 8-point Times New Roman; bytes preserved as requested.
- Protected against the `61118bfc` baseline: preamble/all non-Methods source including full external
  Limitations paragraph byte-identical; **four complete table environments byte-identical** despite
  Table II movement; 20 citation keys retained. Bibliography, six figure files, both canonical snapshots,
  root/paper AGENTS and IEEE DOCX match HEAD blobs. No code/data/asset edits. Prose count 1,097 to 1,110
  with the same stripping method (figures/captions/tables/math/headers excluded).
- User-authorized caption revision (2026-10-25): replaced the three-sentence explanatory note in
  Fig. 2 with the short caption `Retrieval alternatives: No RAG, Hybrid, and independent HyDE.`
  after verifying the removed explanatory clauses remain in prose (Study Design: Base vs No RAG;
  Retrieval: independent HyDE and retrieved-chunks-only evidence). Rebuilt and re-inspected in
  `/tmp/opencode/rag-cap2-AsqWjv`; source SHA-256 `b36cd56d5ada61a0acea06078f24d08a3b23c7e9c0348b336ef95d26fea6f466`;
  PDF SHA-256 `96d88f4d480a69dfdfb253fb58807533456f14b2544752000c5bbd5c91f576e7`;
  6 Letter pages, 333,880 bytes, 9 underfull, no actionable diagnostics, all fonts embedded.
  The live source also gained, concurrently and untouched here, a short evaluator-settings paragraph
  (RAGAS 0.4.3, gpt-5.4-mini, text-embedding-3-small, 2048-token limit) included in that rebuild.
  Previous accepted identities (source `1557fcd6...`, PDF `9436bd4c...`) describe the long-caption snapshot.
- Python tests/runtime harness N/A, passive TeX layout. TDD unknown, RED/GREEN inapplicable. No native
  review/assessment/toggle/START by this writer; parent visual acceptance is not native review approval.
- Own pending authored count: source 125 additions + 171 deletions = 296; document 134 + 95 = 229;
  **525 pending**, **880 cumulative** with ODD-01. Exclude external 10 lines/PDF. Full mirror: `MaternaCare-ES`, `odd/concise-methodology/tasks`.
- ODD-01 checked, ODD-02 unchecked awaiting an authorized own-scope commit after parent visual acceptance.
  HEAD remains `c2eadae`, index empty; no staging/commit. Shared external work still blocks whole-path
  committing/restoring. Rollback only to the preserved before-snapshot when live external work still
  matches it; never overwrite concurrent work. Untracked `stix` task document preserved.
