# DeFi Credit Scoring Engine

This repository presents a robust machine learning pipeline to assign **credit scores (0–1000)** to wallets interacting with the Aave V2 protocol. The scores are computed using only historical on-chain behavior to assess reliability, activity consistency, financial responsibility, and bot-like behavior.

---

## 🚀 Project Objective

To develop an explainable and automated credit scoring engine that evaluates wallet behavior based on transaction-level interactions with DeFi protocols (e.g., `deposit`, `borrow`, `repay`, `redeemunderlying`, `liquidationcall`). 

Higher scores indicate reliable users with good financial discipline. Lower scores indicate risk-prone, bot-like, or exploitative behavior.

---

## 📁 Input Data

The input is a raw JSON file containing user transactions:

- File: `user-wallet-transactions.json`
- Size: ~87MB
- Format: List of dictionaries, each representing a wallet transaction
- Fields used include: `userWallet`, `timestamp`, `action`, `actionData` (with nested `amount`, `assetPriceUSD`, etc.)

---

## 🧠 Methodology

The solution follows a modular ML pipeline with the following steps:

### 1. Feature Engineering

For each wallet, we aggregate features across:

- **Transaction Activity**
  - Total transactions, frequency, time gaps
- **Financial Metrics**
  - Volume in USD, deposits/borrows, repayment ratios
- **Behavioral Patterns**
  - Bot-like behaviors (round numbers, repetitive patterns)
- **Risk Indicators**
  - Liquidation ratios, variance in transactions
- **Asset Diversity**
  - Gini coefficient, asset concentration

### 2. Scoring Models

Five sub-scores are calculated and combined:

| Component           | Method Used              | Weight |
|---------------------|--------------------------|--------|
| Health Score        | Rule-based on repayments | 30%    |
| Behavior Score      | Time & pattern analysis  | 25%    |
| Risk Score          | Variance, liquidation    | 20%    |
| Activity Score      | Frequency, volume        | 15%    |
| Anomaly Score       | Isolation Forest         | 10%    |

The final credit score is a weighted combination of the above, scaled to 0–1000.

---

## 📦 Output

- `wallet_credit_scores.csv`: Final credit scores with breakdowns
- `wallet_features.csv`: All engineered features
- `credit_score_visualizations.png`: Comprehensive score visualization
- `analysis.md`: Detailed interpretation of score distribution

---

## 📊 Visualizations

Includes:
- Histogram of credit score distribution
- Component scores comparison
- Wallet activity trends
- Correlation heatmaps

---

## 🧪 Requirements

```bash
pip install pandas numpy matplotlib seaborn scikit-learn plotly
