# Recommender Benchmark

A reproducible evaluation harness for comparing pretrained sequential and generative recommendation models on user interaction histories.

## Project status

**Current:** Project scaffold and evaluation plan. No completed model comparison results are published in this repository yet.

**Next:** Select two compatible pretrained checkpoints, verify their training data and test split compatibility, then implement and validate the evaluation protocol.

## Research questions

- How do sequential and generative recommenders differ in top-k ranking quality?
- How does interaction-history length affect recommendation quality?
- How do popularity, sparse histories, and long-tail items affect model errors?
- What are the latency and memory costs of each architecture?

## Planned evaluation

- Ranking metrics: Recall@10, NDCG@10, and MRR@10.
- User segmentation: short, medium, and long interaction histories.
- Failure analysis: popularity bias, repeated items, sparse histories, and long-tail misses.
- Systems measurements: model loading time, per-user inference latency, throughput, and peak memory.

## Planned architecture

```text
Interaction dataset and split
    -> preprocessing and user-history builder
    -> model adapters
    -> candidate generation / scoring
    -> ranking metrics
    -> user-segment analysis
    -> failure-case review
    -> benchmark report
```

## Repository layout

```text
configs/              Dataset, checkpoint, and evaluation configurations
docs/                 Protocol, data provenance, and architecture notes
src/data/             Dataset loading and interaction-history construction
src/models/           Sequential and generative model adapters
src/evaluation/       Evaluation runner and candidate handling
src/metrics/          Recall@K, NDCG@K, MRR@K
src/analysis/         User segments, popularity, and failure analysis
experiments/          Run manifests and raw metrics
reports/              Benchmark summaries
tests/                Data split, ranking, and metric tests
```

## Candidate models and datasets

Potential starting points from the assignment:

- P5 pretrained checkpoints: [jeykigung/P5](https://github.com/jeykigung/P5)
- BIGRec pretrained checkpoints: [USTCbaokq on Hugging Face](https://huggingface.co/USTCbaokq)
- SASRec / gSASRec: [asash/gSASRec-pytorch](https://github.com/asash/gSASRec-pytorch)
- MovieLens: [GroupLens datasets](https://grouplens.org/datasets/movielens/)
- Amazon Reviews 2023: [McAuley-Lab/Amazon-Reviews-2023](https://huggingface.co/datasets/McAuley-Lab/Amazon-Reviews-2023)

Before implementation, verify that the selected checkpoint was trained on the exact dataset/category and that its preprocessing and test split can be reproduced. Do not compare models on incompatible splits.

## Planned milestones

1. Verify checkpoint loading and dataset compatibility.
2. Reproduce the authors' preprocessing and test split.
3. Implement a common top-k evaluation interface.
4. Compute Recall@10, NDCG@10, and MRR@10.
5. Segment results by interaction-history length and item popularity.
6. Analyze at least four incorrect recommendations.
7. Add inference latency and memory measurements.

## Scope

This project evaluates pretrained recommenders; it does not claim to train or fine-tune models. Publish quantitative results only after the evaluation pipeline is validated.
