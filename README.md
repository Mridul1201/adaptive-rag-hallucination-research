# Adaptive Retrieval-Augmented Generation for Reducing Hallucinations in Large Language Models

An experimental research project investigating retrieval, answer generation, and deterministic answer extraction on a structured historical Indian Premier League (IPL) cricket question-answering benchmark.

> **Research status:** Completed.

## Explore the Project

- [Open the Research Paper](./Structured_IPL_RAG_Revised_Personal_Report_.pdf)
- [Open the research notebook](adaptive_rag_github_ready/notebooks/IPL_Adaptive_RAG_Research_Cleaned.ipynb)
- [Browse the main results tables](adaptive_rag_github_ready/results/tables/)
- [View statistical tests](adaptive_rag_github_ready/results/statistical_tests/)
- [Explore error analysis](adaptive_rag_github_ready/results/diagnostics/)

## Research Overview

Retrieval-Augmented Generation (RAG) combines information retrieval with language generation to help language models answer questions using external evidence. This project compares retrieval and answer-extraction strategies on questions constructed from historical IPL match data.

The aim is to examine how retrieval quality and answer-generation methods affect factual answer accuracy in a structured question-answering setting.

## Research Questions

- How does retrieval affect answer accuracy compared with generation without retrieval?
- How do fixed BM25 retrieval and metadata-assisted retrieval compare?
- How does deterministic answer extraction from retrieved evidence compare with generative answering?
- What types of errors occur when language models answer structured factual questions?

## Experimental Setup

The current evaluation uses **180 questions** sampled from a held-out test partition. The questions cover three categories:

- Individual batter runs
- Innings totals
- Match winners

Five approaches are compared:

1. Language-model generation without retrieval
2. Fixed BM25 retrieval with language-model generation
3. Metadata-assisted retrieval with language-model generation
4. Fixed BM25 retrieval with deterministic answer extraction
5. Metadata-assisted retrieval with deterministic answer extraction

The metadata-assisted approach uses task-specific rules. It should not be interpreted as a learned adaptive-retrieval model.

## Preliminary Results

In the current 180-question evaluation, exact-match accuracy was:

| Method | Correct | Accuracy |
|---|---:|---:|
| No retrieval + FLAN-T5-small | 3/180 | 1.67% |
| Fixed BM25 RAG + FLAN-T5-small | 100/180 | 55.56% |
| Metadata-assisted RAG + FLAN-T5-small | 101/180 | 56.11% |
| Fixed BM25 + deterministic extraction | 179/180 | 99.44% |
| Metadata-assisted retrieval + deterministic extraction | 180/180 | 100.00% |

These are preliminary results on a template-generated benchmark built from structured cricket data. They do not establish general hallucination reduction across domains. 

## Repository Contents

- [`notebooks/`](adaptive_rag_github_ready/notebooks/) — research notebook and experimental workflow.
- [`results/tables/`](adaptive_rag_github_ready/results/tables/) — method-comparison and question-type tables.
- [`results/statistical_tests/`](adaptive_rag_github_ready/results/statistical_tests/) — confidence intervals and paired statistical tests.
- [`results/diagnostics/`](adaptive_rag_github_ready/results/diagnostics/) — retrieval summaries and error analyses.
- [`results/evaluation_data/`](adaptive_rag_github_ready/results/evaluation_data/) — evaluation configuration and question files.
- [`results/development_pilot/`](adaptive_rag_github_ready/results/development_pilot/) — separate pilot artifacts.
- [`requirements.txt`](adaptive_rag_github_ready/requirements.txt) — Python dependencies.



## Limitations

- Questions are template-generated from structured IPL data rather than a broad, naturally occurring question distribution.
- The evaluation contains 180 questions and covers three question categories.
- Metadata-assisted retrieval is rule-based and task-specific.
- Deterministic extraction relies on the structure and format of the retrieved evidence.
- High exact-match accuracy on this benchmark should not be generalized to open-domain question answering without additional evaluation.

## Data Source

The project uses historical IPL match data from [Cricsheet](https://cricsheet.org/). 

## Research Status

The experimental evaluation and personal research report have been completed. The repository includes the research paper, implementation details, evaluation results, statistical analysis, and supporting artifacts. Further experiments and extensions are outlined under Future Work.

## Future Work

Paraphrased Questions: Test the system with naturally phrased and varied questions to evaluate generalisation.

Unanswerable Questions: Evaluate whether the system can identify insufficient evidence and avoid generating unsupported answers.

Improved Models: Experiment with larger language models and better prompting strategies.

Hybrid Approach: Combine deterministic extraction with language-model generation for more flexible question answering.

Advanced Retrieval: Explore dense and hybrid retrieval methods alongside BM25.

Hallucination Verification: Identify, develop, and experimentally validate reliable verification methods that check generated answers against retrieved evidence and reduce hallucinations.

Robust Evaluation: Test across multiple random seeds and larger, more diverse datasets to assess consistency.

These directions aim to improve retrieval quality, answer reliability, and the system's ability to minimise hallucinations.
