# Adaptive RAG for Historical IPL Question Answering

This repository contains evaluation artifacts for an experimental comparison of retrieval and answer-extraction methods on template-generated questions about historical Indian Premier League (IPL) matches.

> **Research status:** Experimental project / manuscript in preparation. These artifacts do not constitute a published paper.

## Notebook

The cleaned Google Colab/Jupyter notebook is available at [`notebooks/IPL_Adaptive_RAG_Research_Cleaned.ipynb`](notebooks/IPL_Adaptive_RAG_Research_Cleaned.ipynb).

Open it in Google Colab by uploading the notebook or using Colab's GitHub import feature. The notebook includes data acquisition and preparation, question construction, retrieval/extraction methods, and evaluation workflow. Before treating results as independently reproduced, run it from a fresh runtime and confirm that all cells complete successfully. Some data download and package versions may change over time.

## Evaluation snapshot

The frozen evaluation contains 180 questions sampled from a held-out test partition:
- 60 batter-run questions
- 60 innings-total questions
- 60 match-winner questions

The sample excludes the earlier 60-question development pilot. It is not an independent external benchmark.

## Methods compared

1. No retrieval + `google/flan-t5-small`
2. Fixed BM25 retrieval + `google/flan-t5-small`
3. Metadata-assisted retrieval + `google/flan-t5-small`
4. Fixed BM25 + deterministic rule-based extraction
5. Metadata-assisted retrieval + deterministic rule-based extraction

The metadata-assisted logic is task-specific and rule-based. The extraction methods use structured passage templates; they should not be interpreted as general-purpose natural-language reasoning systems.

## Main observed results

| Method | Correct | Questions | Accuracy |
|---|---:|---:|---:|
| No retrieval + FLAN-T5-small | 3 | 180 | 1.67% |
| Fixed BM25 RAG + FLAN-T5-small | 100 | 180 | 55.56% |
| Metadata-assisted RAG + FLAN-T5-small | 101 | 180 | 56.11% |
| Fixed BM25 + deterministic extraction | 179 | 180 | 99.44% |
| Metadata-assisted retrieval + deterministic extraction | 180 | 180 | 100.00% |

These are observed results on this benchmark. They do not establish perfect generalization or universal hallucination reduction. The one-question differences between fixed and metadata-assisted variants were not statistically significant in the paired tests.

## Repository layout

- `results/tables/` — primary summary tables and main-results table
- `results/statistical_tests/` — confidence intervals and paired McNemar tests
- `results/diagnostics/` — retrieval, generation, extraction, and error diagnostics
- `results/evaluation_data/` — frozen evaluation questions, IDs, and configuration
- `results/development_pilot/` — earlier pilot artifacts, kept separate from the final 180-question evaluation

## Important limitations

- Questions are template-generated from structured historical match records.
- Rule extraction is tailored to the passage templates.
- Evaluation covers one domain and one frozen sample.
- Retrieval quality, answer accuracy, and evidence support are different measures.
- A correct answer alone does not establish that the answer was grounded in retrieved evidence.
- Additional evaluation on independent datasets and less structured questions is needed before making broad claims about hallucination reduction.

## Reproducibility status

This package contains evaluation artifacts, not the complete source notebook, full dataset, or all code needed to recreate every experiment. The Colab notebook and dependency/environment details should be added before describing the repository as fully reproducible.

## Data and licensing

Check the source dataset's terms and attribution requirements before redistributing data or derived records. Do not include credentials, API keys, or other secrets.
