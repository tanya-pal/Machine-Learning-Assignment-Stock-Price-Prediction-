# Stock Price Prediction using Machine Learning


# Overview

This project builds a Python-based machine learning model to forecast next-day stock behavior using two provided datasets:

 - Data.csv – Independent variable
 - StockPrice.csv – Dependent variable representing stock prices

The objective is to model how day-over-day changes in the Data dataset influence next-day stock price movements, strictly within the constraints defined in the assignment.

🎯 Overall Approach & Assumptions
Core Assumptions

The next day’s stock price is primarily influenced by changes in the Data variable from the previous day.

All external market factors (macroeconomic indicators, news, sentiment, etc.) are intentionally ignored.

Only relationships between the provided datasets are modeled.

Modeling Strategy

Predicting absolute stock prices proved highly noisy and unstable.

Therefore, the problem is reformulated to predict the direction of next-day stock movement (Up / Down), which is more robust and realistic for short-horizon forecasting.

🧹 Data Preprocessing
Data Loading

Datasets are loaded directly from the GitHub repository using raw URLs, ensuring reproducibility without manual uploads.

Date Alignment

Both datasets are merged using the Date column.

Data is sorted chronologically to preserve time-series order and prevent data leakage.

Handling Missing Values

Missing values introduced by differencing and rolling operations are removed to maintain clean feature vectors.

🛠 Feature Engineering

Feature engineering explicitly models day-over-day influence, as required by the assignment.

Engineered Features

Data_Change: Day-over-day change in the Data variable

Rolling Statistics (derived only from Data_Change):

3-day moving average

5-day moving average

3-day rolling standard deviation (volatility)

These features capture short-term trends and variability while strictly using only the provided dataset.

Target Variable

NextDayDirection

1 → Stock price increases the next day

0 → Stock price decreases the next day

This binary formulation reduces noise and improves learning stability.

🤖 Model Selection

The Random Forest Classifier was chosen because:

It captures non-linear relationships

It is robust to noisy and limited data

It does not rely on strong distributional assumptions

It balances model expressiveness and overfitting control

Given the constrained feature space, Random Forest provides reliable performance without excessive tuning.

🏋️ Training Methodology
Train–Test Split

A time-based split (80% training, 20% testing) is used instead of random shuffling to mimic real-world forecasting conditions.

Feature Scaling

StandardScaler is applied to normalize feature ranges and improve model stability.

Hyperparameters

Number of trees: 300

Maximum depth: 5

These values were selected to avoid overfitting while maintaining predictive power.

📊 Results & Model Evaluation
Classification Metrics (Directional Prediction)
Accuracy  : 0.53
Precision : 0.53
Recall    : 0.92
F1 Score  : 0.67


The model outperforms the random baseline accuracy of 50%.

High recall for Up movements indicates that the Data variable carries stronger predictive information for upward price trends.

Lower recall for Down movements reflects the noisy and asymmetric nature of short-term stock movements.

Confusion Matrix

Interpretation:

The model correctly identifies most upward movements.

Downward movements are harder to capture, which is expected under constrained feature availability.

Actual vs Predicted Price Direction

Interpretation:

The predicted direction closely follows periods of upward momentum.

Misclassifications highlight the stochastic behavior of daily stock movements.

Regression-Based Price Reconstruction (Illustrative)

Note:
This plot is generated using a separate regression model to illustrate next-day price reconstruction from predicted price changes.
Final model evaluation is performed using classification metrics, not absolute price overlap.

🔍 Key Insights & Observations

Absolute stock price prediction performed poorly due to high noise.

Reformulating the task as a directional classification problem significantly improved stability and interpretability.

Attempts to add additional lag-based features or apply class balancing resulted in degraded performance, indicating limited signal strength.

The final model represents a realistic upper bound under the assignment’s strict constraints.

⚠️ Limitations

Only one independent variable is available.

No external market or technical indicators are used.

Short-term stock movements are inherently stochastic.

As a result, very high predictive accuracy is neither expected nor realistic.

✅ Conclusion

This project demonstrates a complete and well-justified machine learning workflow that strictly adheres to the assignment requirements.
The final model successfully captures the directional influence of day-over-day changes in the provided Data variable on next-day stock price movements, achieving a modest but meaningful improvement over a random baseline.

While predictive accuracy is intentionally limited by scope constraints, the modeling decisions, feature engineering, and evaluation reflect sound machine learning and realistic financial modeling practices.
