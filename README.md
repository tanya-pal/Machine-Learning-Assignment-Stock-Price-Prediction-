# Stock Price Prediction using Machine Learning 

# Overview
This project builds a Python-based machine learning model to forecast next-day stock behavior using two provided datasets:
- Data.csv – Independent variable
- StockPrice.csv – Dependent variable representing stock prices
The objective is to model how day-over-day changes in the Data dataset influence next-day stock price movements, strictly within the constraints defined in the assignment.

# Overall Approach & Assumptions

- Core Assumptions

The next day’s stock price is primarily influenced by changes in the Data variable from the previous day.
All external market factors (macroeconomic, news, etc.) are intentionally ignored.
Only relationships between the provided datasets are modeled.

- Modeling Strategy

Instead of predicting absolute stock prices (which are highly noisy), the task is reformulated to predict the direction of next-day stock movement (up/down).

# Data Preprocessing

- Data Loading
Datasets are loaded directly from the GitHub repository using raw URLs to ensure reproducibility without manual uploads.

- Date Alignment
Both datasets are merged using the Date column.
Data is sorted chronologically to preserve time-series order and prevent data leakage.

- Handling Missing Values
Missing values introduced by differencing and rolling operations are removed to ensure clean feature vectors.

# Feature Engineering

Feature engineering is designed to explicitly model day-over-day influence, as required.

- Engineered Features

  - Data_Change: Day-over-day change in the Data variable
  Rolling Statistics (derived only from Data_Change):
  - 3-day moving average
  - 5-day moving average
  - 3-day rolling standard deviation (volatility)
  These features capture short-term trends and variability while strictly using only the provided dataset.

- Target Variable

  - NextDayDirection:
  - 1 → Stock price increases the next day
  - 0 → Stock price decreases the next day
  This binary formulation reduces noise and improves learning stability.

# Model Selection

  The Random Forest Classifier was chosen because:
  - It captures non-linear relationships
  - It is robust to noisy and limited data
  - It does not rely on strong distributional assumptions
  - It balances model expressiveness and overfitting control
  Given the constrained feature space, Random Forest provides reliable performance without excessive tuning.

# Training Methodology

  - Train–Test Split:
  A time-based split (80% training, 20% testing) is used instead of random shuffling to mimic real-world forecasting conditions.

  - Feature Scaling:
  StandardScaler is applied to normalize feature ranges and improve model stability.

  - Hyperparameters:

   - Number of trees: 300
   - Maximum depth: 5
   These values were selected to avoid overfitting while maintaining predictive power.

#  Model Evaluation

Performance Metrics
- Accuracy: ~53%
- Baseline Accuracy: 50% (random guessing)
The model consistently outperforms the random baseline, demonstrating that the engineered features capture meaningful predictive signal.

# Observed Behavior
- High recall for upward price movements
- Lower recall for downward movements
This asymmetric behavior indicates that the provided Data variable is more informative for predicting upward trends, which is a realistic outcome in constrained financial modeling.

# Key Insights & Observations

- Absolute stock price prediction performed poorly due to high noise.
- Reformulating the task as a directional prediction problem significantly improved stability and performance.
- Attempts to add additional lag-based features or class balancing resulted in degraded accuracy, indicating limited signal strength in the data.
- The final model represents a realistic upper bound under the assignment’s strict constraints.

# Limitations

- Only one independent variable is available.
- No external market or technical indicators are used.
- Short-term stock movements are inherently stochastic.
- As a result, very high predictive accuracy is neither expected nor realistic.

# Conclusion

This project demonstrates a complete and well-justified machine learning workflow that strictly adheres to the assignment requirements.
The final model successfully captures the directional influence of day-over-day changes in the provided Data variable on next-day stock price movements, achieving a modest but meaningful improvement over a random baseline.
While predictive accuracy is intentionally limited by scope constraints, the modeling decisions, feature engineering, and evaluation reflect sound machine learning and financial modeling practices.
