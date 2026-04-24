# ABIO Stock Prediction Series II

## 📌 Overview

This project is the second iteration of predicting stock prices for **ABIO (ARCA Biopharma Inc.)** using historical OHLCV (Open, High, Low, Close, Volume) data.  
The current implementation focuses on **linear regression models** (Linear, Ridge, Lasso) with hyperparameter tuning and cross-validation.

> ⚠️ **Note**: This is an educational project. Stock price prediction is extremely challenging, and these models are not suitable for real trading without significant improvements.

---

## 📁 Dataset

**Source**: Yahoo Finance (or similar)  
**Ticker**: ABIO  
**Date Range**: 2015-01-01 to 2020-04-01  
**Rows**: 1,321 trading days  
**Features**:
- Open
- High
- Low
- Close (target)
- Volume

---

## 🧠 Models Used

| Model        | Library          | Tuning                     |
|--------------|------------------|----------------------------|
| Linear Regression | scikit-learn   | Cross-validation (CV=5)    |
| Ridge Regression  | scikit-learn   | GridSearchCV on alpha      |
| Lasso Regression  | scikit-learn   | GridSearchCV on alpha      |

**Evaluation Metric**: Negative Mean Squared Error (neg MSE) + R² score.

---

## 📊 Results Example

- **Best Ridge Alpha**: `1e-15`  
- **Best Lasso Alpha**: `1e-15`  
- **R² Score (Lasso on test set)**: ~0.998

> *High R² values may indicate data leakage (see limitations below).*

---

## 🚧 Current Limitations & Known Issues

| Issue | Description |
|-------|-------------|
| Data Leakage | Using `High`, `Low`, and `Open` from the same day to predict `Close` gives unrealistic performance. |
| Shuffled Split | `train_test_split` randomly shuffles time-ordered data, leading to look-ahead bias. |
| No Feature Scaling | Volume and price have very different scales, affecting regularization models. |
| No Time Series Split | Should use `TimeSeriesSplit` instead of K-Fold. |
| No Lag Features | Past closing prices aren't used as features. |

---

## 🔧 How to Run

1. Clone the repository:
```bash
git clone https://github.com/yourusername/abio-stock-prediction.git
cd abio-stock-prediction
