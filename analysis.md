# Score Distribution and Wallet Behavior Analysis

## 📊 Score Range Breakdown

The predicted wallet scores are grouped and analyzed in bins:

| Score Range | Wallet Count | Insights |
|-------------|--------------|----------|
| 0–100       | 125          | Very risky behavior, frequent borrow/liquidation, little or no deposit |
| 100–200     | 342          | Risky users, imbalance in usage, higher borrow-to-deposit ratios |
| 200–400     | 820          | Mixed behavior, possible new users or bots |
| 400–600     | 1,274        | Moderate activity, no clear red flags |
| 600–800     | 3,092        | Good users with consistent deposits/repays |
| 800–1000    | 4,347        | Highly reliable wallets, regular deposit/repay, low or no liquidation |

(Counts are examples — use actual `value_counts` output from notebook)

---

## 📈 Distribution Plot

A histogram of predicted scores is included below:

![score-distribution](score_distribution.png) *(or generated via matplotlib in notebook)*

---

## 💡 Observations

- A significant number of wallets score above 600, suggesting active and healthy DeFi usage.
- Wallets in the 0–200 range often show patterns of:
  - Frequent borrowing with little repayment
  - Liquidation events
  - Short lifespan in transaction history
- Top scoring wallets tend to:
  - Have many `deposit` and `repay` events
  - Rarely interact with `liquidationcall`
  - Show consistent behavior over time

---

## ✅ Conclusion

This analysis can guide risk management strategies and wallet-level insights in DeFi protocols. The scoring model can be extended by:
- Incorporating time-series trends
- Cross-protocol activity
- Combining with on-chain reputation signals
