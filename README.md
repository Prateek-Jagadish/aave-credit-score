# 💳 Aave Wallet Credit Scoring (0–1000)

This project builds a machine learning model that assigns a **credit score between 0 and 1000** to each wallet address using raw transaction data from the Aave V2 protocol.

The score reflects the **responsibility and trustworthiness** of a user based on their historical DeFi activity.

---

## 📁 Dataset

The dataset is a large JSON file containing ~100,000 DeFi transactions. Each record includes:
- `wallet`: User wallet address
- `action`: One of `deposit`, `borrow`, `repay`, `redeemunderlying`, or `liquidationcall`
- `timestamp`: UNIX time

---

## ⚙️ Methodology

### 1. 🔧 Feature Engineering

For each wallet, we calculated:
- Total number of each action (deposit, borrow, repay, etc.)
- `repay_rate = repay / (borrow + 1)`
- `deposit_borrow_ratio = deposit / (borrow + 1)`
- Total transaction count
- Whether the wallet was **liquidated** (`1` if yes, `0` if no)

### 2. 🧮 Credit Scoring Logic

We created a simple and explainable scoring model:
- Scaled important behavior metrics between 0 and 1
- Penalized wallets that were liquidated
- Combined scaled features using weights:
  - 40% → `repay_rate`
  - 40% → `deposit_borrow_ratio`
  - 20% → `transaction count`
  - -50% → if liquidated
- Normalized the final raw score to a range of **0–1000**

---

## 💾 Output

- `wallet_credit_scores.csv`: Wallet addresses with their calculated credit score (https://drive.google.com/file/d/1-NpkDt-CaU9lZvWWAe-WArSUJGIRw88N/view?usp=sharing)

Example:
userWallet                                    credit_score
0x0000000002032370b971dabd36d72f3e5a7bf1ee    521
0x000000000096026fb41fc39f9875d164bd82e2dc    476
0x0000000000e189dd664b9ab08a33c4839953852c    471



---

## 📈 Score Summary

- Majority of wallets scored between **400–500**
- Very few scored in high range (800+)
- Liquidated wallets and wallets with no repayments scored very low

---

## 🙌 Author

Project by **Prateek Hiremath**  
