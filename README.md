# World Cup 2026 — Match Predictor

> Using machine learning to predict match outcomes and simulate the 2026 FIFA World Cup tournament.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Progress-f39c12?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-27ae60?style=flat-square)

---

## Project Goal

Build an end-to-end ML pipeline that:
1. **Predicts match outcomes** (win / draw / loss) between any two international teams
2. **Simulates the full 2026 World Cup bracket** using Monte Carlo methods
3. **Makes live predictions** as the tournament unfolds in June 2026
4. **Documents the full process** — wins, losses, and lessons learned


---

## Project Structure

```
worldcup-2026-predictor/
│
├── data/
│   ├── raw/                    # Original, unmodified source files
│   └── processed/              # Cleaned and feature-engineered datasets
│
├── notebooks/
│   ├── 01_data_collection.ipynb
│
│
├── src/
│   ├── data_loader.py          # Data ingestion utilities
│   ├── features.py             # Feature engineering functions
│   ├── model.py                # Model training and evaluation
│   └── simulate.py             # Tournament simulation engine
│
├── results/
│   ├── plots/                  # Charts and visualisations
│   └── predictions/            # Saved model outputs
│
├── requirements.txt
└── README.md
```

---

## Data Sources

| Source | Description | Used For |
|---|---|---|
| [Kaggle — International Football Results](https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017) | 45,000+ match results since 1872 | Training data, form, H2H |
| [FIFA Rankings](https://www.fifa.com/fifa-world-ranking) | Official team rankings over time | Ranking features |
| [Elo Ratings](https://www.eloratings.net) | Elo-based team strength ratings | Baseline + features |
| [Transfermarkt](https://www.transfermarkt.com) | Squad value, player ages | Squad-level features |

---

## 🔬 Methodology

### Problem Framing
Each match is treated as a classification problem with three outcomes:
- **Home win** (or first-named team win at neutral venues)
- **Draw**
- **Away win**

Probabilities for all three outcomes are predicted, not just the most likely class.

### Feature Engineering
Key features used in modeling:

| Feature | Description |
|---|---|
| `ranking_diff` | FIFA ranking difference between teams |
| `elo_diff` | Elo rating difference |
| `home_form` | Win rate over last 10 matches |
| `away_form` | Win rate over last 10 matches |
| `h2h_win_rate` | Head-to-head record (last 10 meetings) |
| `avg_goals_scored` | Rolling average goals scored (last 10) |
| `avg_goals_conceded` | Rolling average goals conceded (last 10) |
| `neutral_venue` | Boolean flag for neutral venue |
| `tournament_weight` | Weighting by competition importance |

### Models to be Used:
- Logistic Regression (baseline)
- Random Forest
- XGBoost *(primary model)*
- Neural Network (experimental)

### Tournament Simulation
The bracket is simulated 10,000 times using match probabilities. Each run samples outcomes stochastically — meaning a 30% underdog wins roughly 30% of the time across runs. Final output is a probability distribution over all possible winners.

### Evaluation
- **Log loss** — primary metric (rewards calibrated probabilities)
- **Brier score** — measures probabilistic accuracy
- **Accuracy** — secondary, for interpretability
- **Backtesting** — validated against 2018 and 2022 World Cups

---

## Getting Started

### Prerequisites
```bash
python >= 3.10
```

### Installation
```bash
git clone https://github.com/diegoberum/worldcup-2026-predictor.git
cd worldcup-2026-predictor
pip install -r requirements.txt
```

### Run EDA
```bash
jupyter notebook notebooks/02_eda.ipynb
```

### Run Tournament Simulation
```bash
python src/simulate.py
```

---

## Results

> *Results will be updated as the project progresses.*

| Model | Log Loss | Brier Score | Accuracy |
|---|---|---|---|
| Naive baseline (rank-based) | — | — | - |
| Logistic Regression | — | — | — |
| XGBoost | — | — | — |

### 2026 World Cup Predictions
> *To be published once the draw is confirmed and the tournament begins.*

---

## Project Roadmap

- [x] Download and load historical match data
- [x] Exploratory data analysis
- [ ] Merge FIFA / Elo rankings
- [ ] Feature engineering pipeline
- [ ] Baseline logistic regression model
- [ ] XGBoost model + hyperparameter tuning
- [ ] Backtest on 2018 and 2022 World Cups
- [ ] Tournament simulation (Monte Carlo)
- [ ] Live predictions — Group Stage (June 2026)
- [ ] Live predictions — Knockouts (July 2026)
- [ ] Post-tournament analysis

---

## Caveats

- Football is inherently unpredictable. This model outputs **probabilities**, not certainties.
- Squad injuries and suspensions close to the tournament can invalidate pre-tournament predictions.
- Betting odds are a hard benchmark — they aggregate massive amounts of information and are difficult to beat consistently.
- All predictions are for educational and portfolio purposes only.

---

## Contributing

Feedback and suggestions welcome. Open an issue or reach out on LinkedIn.

---

## License

MIT License — see [LICENSE](LICENSE) for details.
