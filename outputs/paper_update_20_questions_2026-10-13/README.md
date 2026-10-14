# Consolidated results for the 20-question evaluation

This directory contains aggregate results for the exploratory evaluation reported in the manuscript: 10 questions in each of two scenarios, evaluated under 12 model/adaptation/retrieval conditions (240 condition-item outputs). Results remain separated by scenario; the scenario-level means are not pooled.

All 1,360 applicable automatic metric values are present. The six metrics in Table III have 10 valid observations per applicable condition. Context-dependent metrics are not applicable to No RAG. No per-question answers, prompts, or retrieved source excerpts are included in these aggregate files.

## Files

- `table_iii_recomputed.csv`: condition means and valid sample counts for the six metrics reported in Table III.
- `condition_summary.csv`: condition-level means, sample standard deviations, operational measures, retrieval summaries, and metric-coverage counts.
- `descriptive_contrasts.csv`: descriptive differences between conditions; these are not inferential significance tests.
- `operational_metrics_summary.csv`: aggregate generation, output-length, GPU-energy-estimate, and peak-memory measures.
- `noise_sensitivity_summary.csv`: condition-level noise-sensitivity results.
- `maternaqa_reference_retrieval_summary.csv`: aggregate reference-chunk retrieval measures for the MaternaQA-es subset, where reference metadata is available.

The analysis is exploratory and limited to the 20-question evaluation set; it does not represent the full 328-question test partition or establish clinical validity.
