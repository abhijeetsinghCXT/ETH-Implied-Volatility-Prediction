ETH 10‑Second Ahead Implied Volatility Prediction

Overview

This project forecasts Ethereum's implied volatility (IV) 10 seconds ahead using high‑frequency order book data, engineered features, and cross‑asset signals from BTC, DOGE, DOT, LINK, SHIB, and SOL.
It is submitted as part of the GoQuant recruitment process, fulfilling the competition’s functional requirements.

Data & Features

Sources:

1. Train and Test order book data for ETH (with label as target in train)
2. Matching timestamps for BTC, DOGE, DOT, LINK, SHIB, SOL

Engineered Features

ETH Features:

mid_price = (ask_price1 + bid_price1) / 2
spread = ask_price1 − bid_price1
order_imbalance = (bid_volume1 − ask_volume1) / (bid_volume1 + ask_volume1)
Rolling mean & std over 10‑second window (shifted to prevent leakage)
Lagged mid_price & spread


Cross‑Asset Features:

Same rolling mean/std and mid_price from BTC/DOGE/DOT/LINK/SHIB/SOL merged on timestamp

Modelling:

. Algorithm: LightGBM regression
. Validation: 80/20 chronological split
. Metric: RMSPE
. RMSPE = sqrt(mean(((pred - actual) / actual)^2))

Early stopping after 50 rounds without improvement

Results:

Validation RMSPE: 0.481535

Top 10 Important Features:
roll_std_10
roll_mean_10
mid_price_lag1
bid_volume1
ask_volume1
order_imbalance
bid_volume2
ask_volume2
ask_volume3
bid_volume3

Plots:

Predicted vs Actual (Validation) — shows close tracking of predicted IV with actual movements
Feature Importance — highlights ETH spread, ETH rolling volatility, and BTC/SOL cross‑asset features as strong predictors

Submission:
Predictions generated for all test timestamps in submission.csv:

Author
Abhijeet Singh

Kaggle Username: abhijeetssinghh
