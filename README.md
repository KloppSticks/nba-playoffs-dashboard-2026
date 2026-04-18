# NBA Playoffs 2026 — Prediction Dashboard

Self-contained HTML dashboard for the 2026 NBA playoffs, auto-generated from a
private predictive model. Hosted on GitHub Pages so it renders on any device
(Mac, iPhone, anything with a modern browser).

**Live:** https://kloppsticks.github.io/nba-playoffs-dashboard-2026/

This repo only holds the rendered dashboard (`index.html`). The model code,
training data, and simulation engine live in a separate private repository
and are not published here. Predictions are rebuilt locally and pushed here
whenever fresh model output is available.

## What you'll see

- **Bracket** — all 8 Round 1 matchups with probabilities. Round 2+ slots show
  dropdowns that let you pick your own path through the bracket and see the
  model's probability for each resulting series.
- **Series Detail** — tap any matchup for Monte Carlo distributions, per-game
  predictions (spread + total), and a winner × length joint table.
- **Backtest** — model performance on the 2023-24 and 2024-25 playoffs.
- **Model Info** — training metadata and known limitations.

Everything is client-side JavaScript reading an embedded JSON blob — no network
calls, no tracking.
