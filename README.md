# Rip Current Risk Prediction

Predicting daily rip current risk (Low / Moderate / High) for Orange County, California beaches using publicly available NOAA ocean data.

## Overview

Rip currents kill more Americans each year than hurricanes, tornadoes, or lightning. This project builds a machine learning classifier that predicts the official National Weather Service rip current risk rating from three free, public data sources:

- **Wave conditions** from NDBC buoy 46222 (San Pedro, ~20 mi off Huntington Beach)
- **Tide levels** from NOAA CO-OPS station 9410660 (Los Angeles)
- **Risk labels** from NWS San Diego Surf Zone Forecasts (archived via the Iowa Environmental Mesonet)

## Key Findings

- A simple Logistic Regression model achieves **58.5% accuracy** on out-of-sample data, beating the 34.1% baseline (always predicting "Moderate") by 24 points.
- **Wave energy dominates** the prediction — wave height, dominant period, and a wave energy proxy (H² × T) are the top three features.
- **Tide adds surprisingly little** once wave conditions are in the model, improving accuracy by only 0.2%. This suggests NWS forecasters' ratings are primarily driven by the incoming swell.
- The model is strongest at the extremes — it rarely confuses Low with High, which is the critical distinction for swimmer safety.

## Dataset

2,538 days (Jan 2019 – Dec 2025) with 13 engineered features. Chronological train/test split to prevent data leakage.

## Repository Contents

```
├── README.md
├── rip_current_prediction.ipynb   # Full analysis notebook (runs in Google Colab)
├── feature_importance.png
├── confusion_matrices.png
├── model_comparison.png
└── conditions_by_risk.png
```

## Run It Yourself

1. Open `rip_current_prediction.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Run all cells top to bottom (Shift+Enter)
3. The notebook fetches all data directly from NOAA and NWS — no local downloads needed

## Data Sources

| Source | Station / Product | What It Provides |
|---|---|---|
| [NOAA NDBC](https://www.ndbc.noaa.gov/) | Station 46222 | Hourly wave height, period, direction, water temp |
| [NOAA CO-OPS](https://tidesandcurrents.noaa.gov/) | Station 9410660 | Hourly tide levels |
| [NWS via IEM](https://mesonet.agron.iastate.edu/) | Product SRFSGX | Daily rip current risk ratings (Low/Moderate/High) |

## Built With

Python · scikit-learn · pandas · matplotlib · seaborn

## Author

**Luke Ronningen** · Huntington Beach, CA
Founder, [Aayan Sea Initiative](https://github.com/lukeronningen) · 501(c)(3) ocean safety nonprofit

## License

MIT
