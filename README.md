# NBA Game Prediction System (Winner & Over/Under)

## Overview
This project builds an end-to-end NBA game prediction pipeline using historical game data, advanced feature engineering, regime (playstyle) clustering, and regime-specific machine learning models.

The system predicts:
- **Game winner (home vs away)**
- **Over/Under outcomes for total points**

Rather than using a single global model, the approach clusters games into **distinct statistical regimes** (e.g., fast-paced, defensive, high-volatility matchups) and trains **separate models per regime** to improve contextual accuracy and interpretability.

---

## Data Source
- **NBA Official Data** via `nba_api`
- Seasons included: **2020–21 to 2025–26 (Regular Season)**
- Game-level team statistics fetched using `LeagueGameLog`

Data is saved locally as an Excel file for reproducibility.

---

## Feature Engineering
Key feature engineering steps include:

### Team & Opponent Merging
- Each game is transformed into a **team vs opponent** format
- Home and away teams are explicitly identified

### Rolling & Interaction Features
- Rolling averages (Last 5 & Last 10 games)
- Offensive, defensive, and net ratings
- Pace, shooting efficiency, and rebounding metrics
- Interaction features between home and away teams
- Volatility and fatigue adjustments (e.g., back-to-back games)

### Target Variables
- **Winner model:** Home win vs away win
- **Over/Under model:** Total points relative to line

---

## Regime Clustering
To capture different game environments, games are clustered using:

- **KMeans clustering**
- Standardized pace, efficiency, and volatility metrics
- Silhouette and Davies–Bouldin scores for validation

Each game is assigned a **REGIME_ID**, representing a distinct matchup archetype.

---

## Models

### Model 1: Winner Prediction
- **Algorithm:** Random Forest Classifier
- **Approach:** One model per regime
- **Features:** Net rating, offensive/defensive efficiency, pace, recent form
- **Output:** Probability of home team winning

### Model 2: Over/Under Prediction
- **Algorithm:** Random Forest Classifier
- **Approach:** One model per regime
- **Features:** Pace, shooting efficiency, volume stats, volatility measures
- **Output:** Probability of going over the total points line

---

## Evaluation & Analysis
- Win rate and over rate analyzed **per regime**
- Cluster-level performance summaries
- SHAP values used for **model interpretability**
- Comparison of behavioral differences across regimes

---

## Interactive Components
- `ipywidgets` used for interactive exploration
- Dynamic matchup selection
- Real-time predictions for upcoming games
- Regime-aware inference

---

## Libraries Used
- `pandas`, `numpy`
- `scikit-learn`
- `nba_api`
- `matplotlib`
- `ipywidgets`
- `shap`

---

## Key Idea
**Not all NBA games behave the same.**  
By clustering games into statistical regimes and training models within each regime, this system captures context that traditional one-model approaches miss.

---

## Notes
This project is intended for **educational and analytical purposes**, focusing on sports analytics, machine learning pipelines, and model interpretability.

---
