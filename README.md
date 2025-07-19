# Aave V2 DeFi Wallet Credit Scoring

## 🧠 Problem Statement

Given 100K transaction-level DeFi interactions from the Aave V2 protocol, the goal is to assign a **credit score (0–1000)** to each unique wallet address. The score must reflect the reliability and responsibility of each wallet's behavior based on historical actions.

## 📊 Data Description

- **Source**: Aave V2 protocol logs
- **Size**: 100,000 records (~87 MB JSON)
- **Key columns**:
  - `userWallet`: Wallet address (ID)
  - `action`: Type of transaction (e.g., `deposit`, `borrow`, `repay`)
  - `actionData`: Contains numeric fields like `amount`
  - `timestamp`: Epoch time of transaction

## ⚙️ Feature Engineering

We engineered the following wallet-level features:

- **Transaction Counts**: Number of each action type (`deposit`, `borrow`, `repay`, etc.)
- **Amount Statistics**: `sum`, `mean`, `max` of the `amount` values extracted from `actionData`
- **Ratios & Flags**:
  - `borrow/deposit` ratio
  - `liquidationcall` frequency

## 🎯 Scoring Logic

To simulate the score (as actual scores were not provided), we designed a heuristic:

```python
score = 600 + 0.2 * mean_amount - 100 * borrow/deposit ratio - 0.1 * liquidationcount
```

The score is then clipped between `0` and `1000`. This logic can be updated with true supervised labels if available.

## 🤖 Model

- **Algorithm**: Random Forest Regressor (sklearn)
- **Input**: Engineered features from above
- **Target**: Simulated score
- **Validation**: R² score printed for test set

## 📦 Project Structure

```
.
├── user-wallet-transactions.json
├── main.ipynb               # Jupyter notebook with full pipeline
├── wallet_scores.csv        # Final output
├── README.md                # This file
└── analysis.md              # Score analysis
```

## ✅ How to Run

1. Load the JSON file into a pandas DataFrame
2. Run the notebook to:
   - Generate features
   - Train model
   - Score all wallets
3. Review `wallet_scores.csv` and `analysis.md`
