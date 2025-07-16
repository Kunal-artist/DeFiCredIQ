# DeFi Wallet Credit Scoring – Aave V2

This project assigns credit scores (0–1000) to DeFi wallets using Aave V2 transaction history. Scores reflect reliability, with higher values indicating responsible usage.

---

## 🔧 Architecture Overview

### 1. **Data Input**
- Input: Raw Aave V2 transaction-level JSON data
- Actions include: `deposit`, `borrow`, `repay`, `redeemunderlying`, `liquidationcall`

### 2. **Feature Engineering**
For each wallet:
- `total_deposit_usd`, `total_borrow_usd`, `total_repay_usd`, `total_redeem_usd`
- `repay_to_borrow_ratio`, `redeem_to_deposit_ratio`
- `total_liquidations`
- `active_days`, `num_tokens`
- `avg_transaction_gap_days`

### 3. **Scoring Logic**
A custom function computes credit scores using:
- Normalized repay/redeem ratios
- Activity measures (token diversity, active days)
- Log-scaled deposit volume
- Heavy penalty for liquidations
- Final score capped in range `[0, 1000]`

### 4. **Clustering (Unsupervised Learning)**
KMeans with `n=5` segments wallets into behavioral clusters. Each cluster's average score is compared for validation.

### 5. **Anomaly Detection**
Isolation Forest flags abnormal usage patterns. Penalized credit scores for outliers.

---

## 🛠 How to Run

1. Upload the transaction JSON file
2. Run the notebook or script
3. Outputs: `wallet_scores.csv` with:
   - `wallet`, `credit_score`, `cluster`, `anomaly`

---

## 📊 Output Preview

Plots show:
- Balanced score distribution (0–350)
- Score variation across KMeans clusters

---

## 📁 Files

- `wallet_scores.csv`: Final scores
- `analysis.md`: Wallet behavior insights
- `notebook.py`: All code (Colab-ready)

---

## 📬 Contact

Made with ❤️ by a data science enthusiast. Feedback and improvements welcome!
