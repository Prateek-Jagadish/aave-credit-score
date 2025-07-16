# 📊 Credit Score Analysis

This file contains analysis of the wallet credit scores generated from the Aave V2 transaction dataset.

---

## 📈 Score Distribution (0–1000)

| Score Range | Number of Wallets |
|-------------|-------------------|
| 0–100       | 99                |
| 100–200     | 0                 |
| 200–300     | 0                 |
| 300–400     | 0                 |
| 400–500     | 3285              |
| 500–600     | 83                |
| 600–700     | 26                |
| 700–800     | 0                 |
| 800–900     | 1                 |
| 900–1000    | 1                 |

---

## 🟢 High-Scoring Wallets (800–1000)

- Rare but very responsible users
- Frequent deposits and repayments
- Very high deposit/borrow ratios
- No liquidation events
- Likely long-term real users, not bots

---

## 🟡 Mid-Scoring Wallets (400–600)

- Majority of users fall in this category
- Participated in lending/borrowing
- May have skipped repayments or have low activity
- Average or fair behavior

---

## 🔴 Low-Scoring Wallets (0–100)

- No repayment activity
- Some only performed deposits or redemptions
- No borrowing, or borrowing without repayment
- May include bots, inactive, or exploitative wallets

---

## 📊 Distribution Plot

A histogram was generated to visualize the score distribution using `seaborn` and `matplotlib` in the notebook.

```python
sns.histplot(features_df['credit_score'], bins=10, kde=True)

