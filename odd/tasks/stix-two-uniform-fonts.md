# Canceled: uniform STIX Two font migration

## Decision and objective

**User canceled this uncommitted feature and explicitly requested restoring the
IEEEtran default font setup and the pre-migration PDF. T1 and T2 are canceled,
not completed. No staging, work-unit commit, or tracking commit is authorized.**

The manuscript already used `\documentclass[conference]{IEEEtran}`. Restore only
the font migration, not unrelated manuscript changes or historical HEAD contents.
IEEEtran is now the selected formatting authority; do not apply earlier literal
DOCX geometry corrections or claim the default fonts are Microsoft Times New Roman.

## Canceled task checklist

- [ ] **T1 — CANCELED:** vendor STIX Two and migrate text/code/math families.
  An uncommitted implementation and seven-page proof existed; the user withdrew
  the feature before its work-unit commit. Roll back that implementation only.
- [ ] **T2 — CANCELED:** relabel retained Figure 1 and prove uniform STIX fonts.
  Never started. Do not alter the original figure or its existing font resources.

## Authorized rollback boundary

- Repository `/home/jhonh/Code/MaternaCare-ES`, branch `fix/figures-longer`, HEAD
  `b2b1cfa247e24b4cd3a225ec06a3e391c157e927`; no branch/history changes.
- Manuscript basename in `papers/oficial/`:
  `Benchmarking General and Medical Small Language Models for Spanish Obstetric Question Answering: The Impact of Fine-Tuning`.
  Restore its `.tex` and `.pdf` from the original **dirty** baseline in
  `/tmp/opencode/stix-two-T1-EX4Ryf/baseline/`, not from HEAD.
- Preserve approved Table V/audit removal, Figure 2 removal (keep its asset),
  Table IV placement on physical page 6, four tables I–IV, and retained Figure 1.
  Preserve every scientific statement, author identity, citation, equation and value.
- Remove only the five new OTFs, copied `OFL.txt`, and authored README in
  `papers/oficial/fonts/stix-two/`, after matching known filenames and hashes.
  Do not touch foreign files, original figure resources, or user-installed TeX.
- No reset/checkout/clean, new feature document, source redesign, font download,
  OS install/uninstall, child agents, remote operations, review calls, RDD toggle,
  staging, commit, PR, push, or merge. This cancellation supersedes the old budget
  and delivery gate; there is no migration left to commit.

## Brief history and baseline identities

The earlier user-selected STIX Two experiment vendored official release v2.13b171
at commit `744a22a4dd626cd14d75728aef34fc8ad7c85db0` with its unmodified OFL.
The first Lua build lacked luaotfload; after the user's own installation, stage
`/tmp/opencode/stix-two-T1-54yntcdv` built seven Letter pages and passed T1 font,
content and basic visual checks. Its PDF was synchronized but never committed.
The original figure was never modified. Earlier full plans and evidence remain
in Engram observation 3189 history; this file records the superseding cancellation.

| Artifact | Original dirty baseline SHA-256 |
| --- | --- |
| TeX | `0604f633804fa13dfc59fd93ea708ee54fe166ee9e4a475ee0ae1bc4afa15bd6` |
| PDF | `0ebc6bc2a03410adf80a6f5c96ee8bd53e3aea628eed0d033be723854be03089` |
| `figures/ft-vs-lora.pdf` | `fcf8dc76b71ddceb50ac18c3774e7a5dad79b02bfba058ae43032b65d63f07f3` |

At cancellation, verified migrated TeX/PDF hashes were respectively
`f3e4f054626680f117b18de3d4b0e6ff844e1bf7e31058095a1e1d9f52a91fe4` and
`e905a8c9f61f40aab8ca5fa83e654028a97bc206da5b919ad1aec1159d778912`.

## Rollback verification and progress

Cancellation was recorded before source rollback; restoration and fresh proof passed.
TDD/application runtime harness: N/A for passive LaTeX/font rollback. Required:

1. Verify current and original hashes, restore exact original TeX/PDF, and remove
   only the verified new font bundle. Confirm no STIX/fontspec/unicode-math setup
   remains in source and the original figure is unchanged.
2. In fresh `/tmp/opencode/ieeetran-font-revert-*`, copy restored source as
   `paper.tex`, `references.bib`, and figures; run foreground
   `pdflatex -interaction=nonstopmode -halt-on-error paper.tex`, `bibtex paper`,
   and the same pdfLaTeX command twice. Record exact exits and warnings.
3. Check seven Letter pages, actual embedded font inventory, missing glyphs,
   errors, overfull boxes and undefined references/citations. Compare the entire
   restored source/body, all four tables, ordered citations, authors/equations/
   values to the original dirty baseline; verify Table IV remains on page 6.
4. Verify fresh-build correspondence independently without replacing the exact
   restored baseline PDF again; run `git diff --check`. Read back this document
   and its full Engram mirror, topic `odd/stix-two-uniform-fonts/tasks`.

### Observed results

- Stage `/tmp/opencode/ieeetran-font-revert-w550stne`: pdfLaTeX pass1, BibTeX,
  pdfLaTeX passes2–3 all exited 0 using the exact commands above. `pdfinfo`
  confirms seven Letter pages, each 612×792 bp; fresh PDF is 364,019 bytes.
- Restored tracked TeX/PDF match the original dirty hashes above exactly;
  fresh/stored text-layout dictionaries and 72-dpi rendered pixels match on all
  seven pages. The independently rebuilt PDF is not copied over the exact baseline.
- All four tables and 18 ordered citation commands, authors, equations and values
  are unchanged; Table IV is on physical page 6. Figure 1 is byte-identical.
- Only the seven verified experiment files and empty font directories were
  removed. No STIX/fontspec/unicode-math setup remains in source; no new fonts remain.
- `pdffonts`: embedded NimbusRomNo9L variants, NimbusMonL and Computer Modern
  math; original Figure 1 retains its Poppins/Noto/STIX italic resources. These
  default-stack results are not literal Microsoft Times New Roman compliance.
- No errors, missing glyphs, overfull boxes, undefined references/citations or
  rerun markers. Seven underfull diagnostics remain: six hboxes and one vbox.
- `pdftotext` and page-6 rasterization exited 0; inspected `rollback-page-6.png`:
  Table IV and surrounding text readable, no visible clipping/overlap.
- Final `git diff --check`: exit 0; branch/HEAD and all three baseline hashes
  match. Only approved dirty TeX/PDF plus this untracked cancellation record remain;
  index is empty. No staging/commit, review, download or OS change occurred.

## Preparation and next step

Loaded exact paths: `/home/jhonh/.pi/agent/skills/academic-research-suite/SKILL.md`
(paper fidelity only), `/home/jhonh/.agents/skills/cognitive-doc-design/SKILL.md`,
and `/home/jhonh/.agents/skills/work-unit-commits/SKILL.md`; root/papers guidance
and actual prior task/mirror were read. Professional English artifacts only.
Parent independently spot-checks the remaining approved baseline diff. Never resume
T1/T2, create a tracking commit, or capture those preexisting changes in a new commit.
