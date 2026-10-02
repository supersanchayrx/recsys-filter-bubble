# Do Recommendations Narrow Taste?

A filter-bubble analysis on Yandex Music's Yambda dataset, where every listen is flagged as either found by the user or served by a recommendation.

> **Status: in progress.** The roadmap below tracks what is done. Results are added here as each part lands.

## The question

Recommendation systems are often accused of trapping people in "filter bubbles" by showing them more of what they already like. Most public data can't separate recommended consumption from self-chosen consumption. Yambda can: every event carries an `is_organic` flag. This project uses it to ask:

1. Does a user's taste diversity shrink or grow over time, and does that depend on how much they rely on recommendations?
2. Are tracks discovered through recommendations replayed and liked as often as tracks users found themselves?
3. Which users depend most on recommendations: new or established, light or heavy listeners?

## Data

**Yambda** (Yandex, 2025): 4.79B listens, likes and dislikes from 1M users over 10 months, with audio embeddings and artist and album metadata. Published on [Hugging Face](https://huggingface.co/datasets/yandex/yambda) in 50M, 500M and 5B event sizes ([paper](https://arxiv.org/abs/2505.22238)). Work starts on the 50M version and scales up.

## Approach

- Load events into **DuckDB** and build per-user monthly panels with SQL window functions
- Measure taste diversity per user and month: artist and genre entropy, and mean pairwise distance between audio embeddings
- Compare users with high and low recommendation share, matched on activity level and tenure
- Compare replay and like rates for recommended vs organic discoveries
- **Caveat:** this is observational data. Recommendation exposure is not random, so results are associations with careful controls, not causal claims.

## Roadmap

- [x] Scope the project and choose the dataset
- [ ] Load Yambda-50M into DuckDB and profile it
- [ ] Per-user monthly panels and diversity metrics
- [ ] Recommendation share vs diversity over time
- [ ] Replay and like rates: recommended vs organic
- [ ] Matched comparison and robustness checks
- [ ] Scale to Yambda-500M
- [ ] Write-up

## Planned structure

```
sql/           DuckDB queries for panels and metrics
src/           loading, metrics and matching code
notebooks/     analysis
data/          downloaded datasets (git-ignored)
```

## Setup

```bash
python -m venv .venv
pip install -r requirements.txt
```
