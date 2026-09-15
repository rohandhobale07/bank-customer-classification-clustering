                        🏦📊 Bank Customer Classification & Clustering Analysis 📊🏦

A dual-technique project combining SQL-based data extraction with both classification and clustering to support bank customer decision-making.

📌 Project Overview

This project analyzes relational bank customer data using SQL, Python, and Scikit-Learn — combining classification to predict a customer-related outcome and clustering to segment the customer base.

The project uses relational data spanning 7 tables: accounts, cards, clients, dispositions, districts, loans, and transactions.

The analysis focuses on SQL-based extraction and joining, followed by two separate machine learning approaches applied to the same underlying customer base.

🎯 Project Objectives

- Join and extract relevant fields across 7 relational tables using SQL
- Build a classification model to predict **loan repayment status** (4 outcome categories)
- Segment customers using K-Means clustering
- Compare and profile the resulting customer groups

🛠️ Technologies Used

🗄️ SQL
- Relational joins and data extraction (`mydb.sql`)

🐍 Python
- Data analysis and modeling

📊 Pandas & NumPy
- Data cleaning and preparation

🤖 Scikit-Learn
- Classification and K-Means clustering

📈 Matplotlib & Seaborn
- Visualization

📗 Microsoft Excel
- Supplementary clustering workbook (K_Means.xlsx)

📓 Jupyter Notebook
- Two separate notebooks: Classification and Clustering

📁 Dataset

Relational bank dataset across 7 tables:

- 🏦 Account
- 💳 Card
- 👤 Client
- 🔗 Disposition (disp)
- 🗺️ District
- 💰 Loan
- 💸 Transaction

🗄️ SQL Extraction

Wrote SQL queries (`mydb.sql`) to join and extract relevant fields across all 7 relational tables into an analysis-ready dataset.

🤖 Classification

Predicted loan status (4 categories, encoded 0–3) from 868 loan records using 3 features: loan amount, duration, and payments (scaled with MinMaxScaler).

Trained and benchmarked 4 classification models on a 70/30 split (607 train / 261 test):

| Model | Accuracy |
|---|---|
| KNN | 98.85% |
| Logistic Regression | 90.80% |
| **Decision Tree** | **99.62%** |
| Random Forest | 98.85% |

⚠️ **Class imbalance caveat:** the dataset is heavily skewed toward one loan-status class (648 of 868 records). The rarest class had only 1 example in the test set, and every model scored 0.00 precision/recall on it despite high overall accuracy — the headline numbers are real but inflated by the dominant class.

🔢 Clustering

Segmented accounts using loan amount and balance as features.

- Used the **Elbow Method** (WCSS across k=1–14) to guide cluster count selection
- Compared 4 linkage methods for Agglomerative Clustering (single, average, complete, ward) against K-Means
- Selected **k=2** as the final cluster count

💡 Key Business Insights

- Loan status can be predicted with high accuracy from just 3 simple features (amount, duration, payments) using a Decision Tree
- Real-world classification performance can look excellent on paper (99.6% accuracy) while completely failing on rare classes — a reminder to check per-class metrics, not just overall accuracy
- Accounts separate into 2 meaningful clusters based on loan amount and balance, providing a simple segmentation for risk or service tiering

⭐ Project Highlights

🗄️ Relational Tables Joined: 7 (account, card, client, disp, district, loan, transaction)

🤖 Classification: 4 models compared, best = Decision Tree at 99.62% accuracy

⚠️ Caveat: Severe class imbalance — rarest loan-status class had 0% recall despite high overall accuracy

🔢 Clustering: K-Means + 4-linkage-method Agglomerative Clustering comparison, k=2 selected via Elbow Method

