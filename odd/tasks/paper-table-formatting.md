# Clarify and format retained tables without changing the figure

## Objective and current gate

Format Tables I–IV and their notes, headings and direct introductory references
for readable, locally applied 8-point table typography. **Parent read back this
file/full mirror 3212, reconciled the approved Conclusions, and authorized sole-writer
T1 continuation with native IEEEtran table typography. Source/PDF proof passed;
the work-unit commit is recorded below; parent assessment remains pending.**

## Scope and protected content

- Only the official long-basename manuscript `.tex`, its verified `.pdf`, and
  this new feature record may change after continuation. Preserve IEEEtran
  conference/default fonts; no downloads, font packages/assets, global fonts,
  geometry, title/author changes, bibliography edits, or scientific-claim repairs.
- **No figure work:** retain the asset, inclusion block, caption, announcing
  sentence, fonts and size byte-for-byte. Do not intentionally move the figure;
  incidental page reflow is not authorization to edit it or its surrounding prose.
- Preserve prior Table V/audit and Figure 2 removals, keeping the removed figure
  asset. Keep four tables I–IV, one retained Figure 1, and exactly seven Letter
  pages. Table III starts on page 5; Table IV must remain on physical page 6.
- Leave canceled `odd/tasks/stix-two-uniform-fonts.md` untouched and uncommitted;
  do not revive any STIX/figure-font decision. No unrelated acronym/first-use or
  “six of eight” repairs. Preserve every numeric cell, equation and author identity.
- Use reasonable table-only wrapping/column spacing and normal-or-larger
  `arraystretch`; no resizing, smaller fonts, negative vertical space or margins
  to force pagination. General notes are not keyed 6-point footnotes.

## Baseline and preparation

Repository `/home/jhonh/Code/MaternaCare-ES`, branch `fix/figures-longer`, HEAD
`b2b1cfa247e24b4cd3a225ec06a3e391c157e927`. Manuscript basename in `papers/oficial/`:
`Benchmarking General and Medical Small Language Models for Spanish Obstetric Question Answering: The Impact of Fine-Tuning`.

| Verified baseline | SHA-256 |
| --- | --- |
| Dirty TeX | `0604f633804fa13dfc59fd93ea708ee54fe166ee9e4a475ee0ae1bc4afa15bd6` |
| Dirty PDF | `0ebc6bc2a03410adf80a6f5c96ee8bd53e3aea628eed0d033be723854be03089` |
| `figures/ft-vs-lora.pdf` | `fcf8dc76b71ddceb50ac18c3774e7a5dad79b02bfba058ae43032b65d63f07f3` |
| `IEEE-Formatting.docx` | `5aa9476585f50612b6f8298ecd6944c0b4f76ab78c467d6cfbb75607c749d436` |

Root/papers guidance and exact requested academic-research-suite, cognitive-doc-design
and work-unit-commits SKILL.md paths were read. Prior supplied DOCX XML typography
findings are preparation context, not a new full audit. Read current table blocks,
protected Figure 1 block/announcement, Results lead and unchanged interval method.
Recheck drift before implementation and capture the dirty baseline, not HEAD.
Comparison baseline: original dirty source above plus the exact currently approved
three-paragraph Conclusions (Engram 3222), captured byte-for-byte before edits.

## Stable task and acceptance

- [x] **T1 — Correct all retained table typography/clarity and close one checked
  work unit.** Route: **delegated-direct**, one bounded writer, no child agents.
  Preparation plus nontrivial TeX/PDF changes trigger this record/full mirror.

Acceptance: ordinary local **native IEEEtran `\footnotesize`**, nominal 8 TeX pt
(approximately 7.970 bp), for table copy, bold heads and general notes. Retain
native small-cap captions, default font families and legitimate smaller math
superscripts; no literal Word 8-bp or Microsoft Times New Roman claim. Remove
the custom tablemath/mathversion/size helper, expansion override and uppercase
caption wrappers. Preserve body/figure styles and original caption strings.
Table I and its note span the full
column. Table II keeps exactly two columns, Parameter/Shared setting, and all
18 rows; change only “LR scheduler” to “Learning-rate scheduler” and add the
unit “tokens” to 1,024. Preserve its shared-setting note and both full model IDs.

Table III metric heads are exactly Answer Correctness, Answer Relevancy, Semantic
Similarity, Faithfulness, Context Precision and Context Recall; wrap bold heads.
Bold the existing Panel B Faithfulness **0.966** without changing its number;
retain all other bold maxima/ties. Replace its note with exactly:

> Note. Means are calculated from 10 responses per condition and scenario for each applicable metric. Dashes indicate metrics not applicable without retrieval. Bold values identify each metric’s maximum within a scenario.

A LaTeX-safe ASCII apostrophe is acceptable without meaning changes. Table IV's
note expands CI to “confidence interval” and states n = 10 questions, retaining
approximate marginal Student-t, independent-question and nonpaired caveats.
Do not alter the interval-method paragraph (baseline lines 533–540). Add short
direct references to Tables III/IV in the Results lead, before their physical
floats, retaining later Table IV uncertainty prose. No other prose changes.

## Required proof (final acceptance pending)

1. Fresh `/tmp/opencode/table-formatting-*`: stage short `paper.tex`, bibliography
   and figures; foreground `pdflatex -interaction=nonstopmode -halt-on-error paper.tex`,
   `bibtex paper`, then the same pdfLaTeX command twice; repeat only for genuine
   convergence. Record exact exits, warnings and immutable snapshot identities.
2. `pdfinfo`: exactly seven Letter pages; `pdffonts`: default stack unchanged.
   Scan errors, missing glyphs, undefined citations/references and overfull boxes.
   Rasterize **all seven pages and actually read them**; verify native nominal
   8-TeX-pt copy/heads/notes, bold metadata and class small-cap captions, widths/fit.
3. Prove physical pre-citation order of III/IV and IV on page 6, full-column I/note,
   two-column II/all 18 rows, unchanged four-table numeric matrices after stripping
   formatting, complete scenario maxima with only the added 0.966 emphasis, exact
   III note, II/IV caveats, and all 18 ordered citation commands unchanged.
4. Compare scientific prose outside allowed table blocks/short Results references,
   math and identities against the reconciled baseline. Preserve the approved
   Conclusions snapshot exactly. Prove figure block, announcement
   and native hash unchanged; optionally compare normalized PDF figure renders.
   Run `git diff --check`; copy only a fully verified seven-page PDF. If impossible
   within scope, stop partial: no content cuts or figure hacks. Record rollback to
   this dirty TeX/PDF baseline without losing prior approvals.

## Delivery, progress and next step

Revised forecast **388–400 authored additions plus deletions**, including approved
prior removals/move/Conclusions, this record, implementation and proof tracking;
generated PDF excluded but checksum-verified. Strategy **ask-on-risk**: if forecast
or count exceeds 400, parent resolves delivery before any commit. This is advice,
not a code cap: never omit proof, minify, trim cosmetically or split artificially.
After parent continuation and proof, one Conventional Commit on this feature branch
may close T1 with checks/docs; attribute captured preexisting edits, not as new work.
Do not stage the canceled STIX record. No PR/push/merge. Committed running count: 398.

TDD/application runtime: N/A, passive LaTeX table typesetting, no Python feature.
No dataset/model tests, downloads, installs, native review calls or RDD changes.
Prior native preflight was unsupported, retry_safe=false; parent owns independent
spot-check and review/risk assessment. T1 is **complete**;
verification passed. Mirror topic: `odd/paper-table-formatting/tasks`.

## Reconciled baseline and current proof

- The parent resolved the earlier concurrent-edit stop: Engram 3222's exact
  approved Conclusions must remain unchanged and may be captured in the combined
  manuscript commit with attribution as preexisting approved work, not new prose.
- Original dirty baseline: `/tmp/opencode/table-formatting-5nin1dgu/baseline`;
  derive a comparison copy by substituting only the captured approved Conclusions.
- Before native-typography simplification, verified source SHA-256:
  `8cb4224fa993f2a12fa07c911ff000eb3ff2ad140c025ba3ba881f05bfc95b9c`.
  Current tracked PDF from the Conclusions work:
  `99401026e4c3b38bdd0d0cb20d03999a38f3e1e39d9f469abdcc3ab3af754831`.
- Earlier literal-8-bp candidates built seven pages, but that unnecessary custom
  machinery is superseded by the parent's explicit native IEEEtran refinement.
  Earlier evidence and the resolved stop remain in full mirror 3212 history.
- Figure native hash and canceled STIX record remain unchanged. All required
  native-font proof passed without new drift; only the verified PDF was synchronized.

## T1 verification evidence

- Final stage: `/tmp/opencode/table-formatting-native-lquedqrh`; comparison source
  `baseline/reconciled.tex`, exact approved snapshot `baseline/conclusions.tex`.
- Exact build commands above: pdfLaTeX pass 1, BibTeX, pdfLaTeX passes 2–3 all
  exit 0. `pdfinfo`: seven Letter pages, 363,451 bytes; III page 5, IV page 6,
  both introductory references page 4. No extra convergence pass was needed.
- `source-checks.stdout`: all row/cell matrices [12,18,24,8], notes, maxima/ties,
  captions, 18 ordered citations and all other scientific prose/math/authors PASS.
  Approved Conclusions remain byte-identical, SHA-256
  `fa0ca7b35efa571926378ec6b234b78be5c9ddc806d6eb79f54ec099a5fcea16`.
- `pdf-checks.stdout`/`measurements.json`: native copy/bold heads 7.9701 bp;
  small-cap glyphs about 6.376 bp; retained microtype gives note spans 7.89–8.0494
  bp; genuine math superscripts 5.9776 bp. Default families retained; no custom
  machinery remains. Table I rule/note span the 251.059-bp column.
- Figure block/announcement/native hash, embedded Form/BBox/placement matrix and
  150-dpi figure-plus-caption pixels match original. Canceled STIX record untouched.
- `pdftotext` and `pdftoppm -f 1 -l 7 -r 110 -png paper.pdf page`: exit 0;
  all seven `page-1.png` through `page-7.png` actually read, no visible clipping,
  overlap or illegible table heads/notes. Independent parent spot-check is pending.
- No errors, missing glyphs, undefined citations/references, overfull boxes or
  rerun markers; seven underfull diagnostics remain. `git diff --check`: exit 0.
- Frozen source SHA-256:
  `3ea7dcca5b3d1ddbf749577de8037a10d28630a3b7a1f7464c3e5836cdeb3033`.
  Verified tracked/staged PDF SHA-256:
  `b04af95870e7192543527336d06db69eba16d2832c452b7c3ff4bc2cf68a723b`.
- Rollback: restore `baseline/reconciled.tex` and rebuild its matching PDF,
  preserving the approved removals/move/Conclusions. No normalizer ran after freeze.
- Work-unit commit: `0bb01844e13d2031d238806c2c3fc59965f49c31`.
  This tracking-only update records its identity and closes T1.

Complete only T1 with the reconciled baseline; no contact with another writer,
additional feature, native review call or RDD switch change is authorized.
