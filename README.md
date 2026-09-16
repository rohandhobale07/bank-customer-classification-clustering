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

Trained and benchmarked 4 classification models on a 70/30 split (607 train / 261 test), using **balanced class weights** to account for a heavily skewed target distribution:

| Model | Accuracy |
|---|---|
| KNN | 98.85% |
| Logistic Regression | 89.66% |
| **Decision Tree** | **99.62%** |
| Random Forest | 99.62% |

⚠️ **Class imbalance caveat:** the dataset is heavily skewed toward one loan-status class (648 of 868 records). Even after applying balanced class weights, every model still scored 0.00 recall on the rarest class — which had only 1 example in the entire test set (and ~2–3 in the whole 868-record dataset). This is a genuine data limitation, not a failed fix: balanced weighting reweights the training loss, but it can't manufacture signal from a class with almost no examples to learn from. The 99%+ accuracy numbers are real, but they reflect performance on the 3 well-represented classes, not the rare 4th one.

🔢 Clustering

Segmented accounts using loan amount and balance as features.

- Used the **Elbow Method** (WCSS across k=1–14) to guide initial cluster count selection
- Compared 4 linkage methods for Agglomerative Clustering (single, average, complete, ward) against K-Means
- **Validated cluster count with silhouette score across k=2–14** — and the results overturned the elbow-method choice: k=7 scored highest (0.4497), not k=2 (0.4336), which the elbow curve alone had suggested
- Selected **k=7** as the final, silhouette-validated cluster count

| k | Silhouette Score |
|---|---|
| 2 | 0.4336 |
| 6 | 0.4426 |
| **7** | **0.4497** |
| 13 | 0.4463 |
| 14 | 0.4491 |

(k=14 scored nearly as high as k=7, but 7 was chosen as the more interpretable, business-usable number of segments rather than defaulting to the single highest score.)

💡 Key Business Insights

- Loan status can be predicted with high accuracy from just 3 simple features (amount, duration, payments) using a Decision Tree or Random Forest
- Balanced class weighting is not a cure-all — a class with almost no examples remains unlearnable regardless of reweighting, which matters more for real-world deployment than the headline accuracy number
- Relying on the elbow method alone would have picked an under-validated cluster count (k=2); numeric silhouette validation surfaced a meaningfully better segmentation (k=7)

⭐ Project Highlights

🗄️ Relational Tables Joined: 7 (account, card, client, disp, district, loan, transaction)

🤖 Classification: 4 models compared with balanced class weights, best = Decision Tree / Random Forest at 99.62% accuracy

⚠️ Caveat: Rarest loan-status class (support=1) remained unlearnable even after class-weight correction — a data limitation, not a modeling failure

🔢 Clustering: K-Means + 4-linkage-method Agglomerative Clustering comparison, **k=7 selected via silhouette score** 
