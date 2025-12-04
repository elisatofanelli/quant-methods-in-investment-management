# Exploring Factor Prediction Outcomes: A Two-Stage Machine Learning Approach

## Project Overview
This project implements a dynamic investment strategy based on a Two-Stage Machine Learning Framework. The objective is to generate excess returns by systematically rotating between equity style factors (Value, Growth, Momentum, Low Volatility, Quality) based on the predicted market environment.

Instead of a static allocation, our model adapts to changing economic conditions by:
1.  **Identifying the Market Regime** 
2.  **Selecting the Optimal Factors Combination** specific to that regime.

---

## Methodology

### The Two-Stage Framework
The strategy separates the prediction task into two distinct supervised learning problems:

#### **Stage 1: Regime Detection**
* **Goal:** Predict if the next month will be a "Normal" market or a "Non-Normal" one (Correction/Bear).
* **Model:** XGBoost Classifier.
* **Rationale:** Selected for its ability to handle non-linear interactions between macroeconomic variables and its superior balance of F1-Score on imbalanced crash data compared to Random Forest and Logistic Regression.

#### **Stage 2: Factor Selection**
* **Goal:** Given the predicted regime, determine which factor has the highest probability of outperforming the market.
* **Model:** **Stacking Ensemble**.
* **Architecture:**
    * *Level 1:* Random Forest, Support Vector Machine, Gaussian Naive Bayes.
    * *Level 2:* Logistic Regression to optimize the weights of the base predictions.

### Backtesting Strategy
* **Approach:** Rolling Window Analysis.
* **Training Window:** 204 months (17 years).
* **Refit Frequency:** Monthly (models are retrained every month to incorporate new data).
* **Out-of-Sample Period:** Feb 2007 – Jan 2025.

---

## Repository Structure
```text
.
├── README.md                                # Project overview and documentation
├── factor_dataset_construction.ipynb        # Factors Returns Dataset Creation
├── clustering.ipynb                         # Market Regimes Creation
├── model_selection.ipynb                    # Model Research & Selection
└── rolling_window_backtest.ipynb            # Final Backtest & Strategy Implementation
```
