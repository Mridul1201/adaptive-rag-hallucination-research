# Adaptive Retrieval-Augmented Generation for Reducing Hallucinations in Large Language Models

An experimental research project investigating retrieval, answer generation, and deterministic answer extraction on a structured historical Indian Premier League (IPL) cricket question-answering benchmark.

> **Research status:** Experimental project in progress. The manuscript is not yet finalized or published.

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

These are preliminary results on a template-generated benchmark built from structured cricket data. They do not establish general hallucination reduction across domains. Further reproducibility and evidence-grounding checks are needed.

## Repository Contents

- `notebooks/` — research notebook and experimental workflow.
- `results/tables/` — method-comparison and question-type tables.
- `results/statistical_tests/` — confidence intervals and paired statistical tests.
- `results/diagnostics/` — retrieval summaries and error analyses.
- `results/evaluation_data/` — evaluation configuration and question files.
- `results/development_pilot/` — separate pilot artifacts.
- `requirements.txt` — Python dependencies.

## Reproducibility

The notebook is provided for inspection and further experimentation. A successful end-to-end execution from a fresh Google Colab runtime has not yet been independently verified. Dataset availability, package versions, and execution requirements may affect reproduction.

## Limitations

- Questions are template-generated from structured IPL data rather than a broad, naturally occurring question distribution.
- The evaluation contains 180 questions and covers only three question categories.
- Metadata-assisted retrieval is rule-based and task-specific.
- Deterministic extraction relies on the structure and format of the retrieved evidence.
- High exact-match accuracy on this benchmark should not be generalized to open-domain question answering without additional evaluation.

## Data Source

The project uses historical IPL match data from [Cricsheet](https://cricsheet.org/). Please consult the source's current terms and attribution requirements before redistributing data.

## Research Status

This repository documents an ongoing experimental project. The manuscript, reproducibility checks, and further evaluation may be updated as the research develops.
