# NBA Playoffs 2026 — Prediction Dashboard

A daily-updating prediction dashboard for the 2026 NBA Playoffs. Powered by a private predictive model that ingests game data, trains scikit-learn models, runs Monte Carlo series simulations, and pulls market consensus odds. Published to GitHub Pages automatically every morning.

**Live:** https://kloppsticks.github.io/nba-playoffs-dashboard-2026/

This repo holds only the rendered dashboard output (`index.html` + `data.json`). The model code, training data, and simulation engine live in a separate private repository and are not published here. Predictions are rebuilt locally and pushed here whenever fresh model output is available.

---

## Dashboard Tabs

| Tab | Content |
|-----|---------|
| **Today** | Today's games — predicted winner, spread, total, market consensus line, Model Edge badge |
| **Bracket** | Full bracket with series win probabilities; interactive dropdowns for Round 2+ |
| **Game Detail** | Full analysis for a selected game: model vs. market, series correction, stat comparison |
| **Results** | ATS/O-U record, CLV tracking, game-by-game log, residual trend charts |
| **Series Detail** | Monte Carlo breakdown: win probabilities, length distribution, per-game predictions |
| **Backtest** | Gate verdict and per-season metrics on 2023-24 and 2024-25 held-out playoffs |
| **Model Info** | Version, feature importances, active injury overrides, active series corrections |

---

## How It Works

The dashboard is a static HTML shell (`index.html`) that loads prediction data at runtime via `fetch('data.json')`. Both files must be served from the same directory — GitHub Pages handles this automatically.

**Note:** Opening `index.html` directly from your filesystem (`file://`) will not work — browsers block the `fetch()` call for local files. Use the live GitHub Pages URL, or serve locally with `python -m http.server 8000` from this directory.

The model behind the dashboard:
- Ingests 5 seasons of NBA game data from `stats.nba.com`
- Engineers a 24-feature differential vector per matchup
- Trains three scikit-learn models (winner classifier + spread/total regressors) with playoff-weighted training
- Runs 10,000 Monte Carlo simulations per series under the 2-2-1-1-1 home-court schedule
- Applies a Bayesian residual correction layer for in-progress series
- Pulls market consensus lines from DraftKings, FanDuel, BetMGM, and Caesars (median)

Backtest accuracy: **64.5%** on 166 held-out playoff games (2023-24 + 2024-25), vs. 58.4% higher-seed baseline.

---

## Limitations

- Linear models only (LogisticRegression + LinearRegression)
- Injury input is manual — no live feed
- Series simulation treats games as independent (no momentum)
- Backtest sample is ~166 games — error bars are wide
- Predictions are for educational and personal-research purposes only. Not financial or gambling advice.
