# 📊 Credit Card Customer Segmentation Analysis

## Overview

This project applies **unsupervised clustering** to a Kaggle credit card dataset to uncover distinct customer segments. It includes:

-   **Exploratory Data Analysis (EDA)**
-   **Feature Engineering** (including NaN handling of ratios)
-   **KMeans Clustering** (optimal cluster selection)
-   **PCA Visualization**
-   **Business interpretation** of each segment

---

## 🔍 Dataset

-   **Source**: `CC GENERAL.csv` from Kaggle
-   **Customers**: 8,950
-   **Features** include: balances, purchase totals, cash advances, frequencies, payments, tenure, plus engineered ratios.

---

## 🧩 EDA

1. Displayed data structure, missing values, and summary statistics.
2. Plotted histograms for distributions of major monetary features.
3. Visualized correlations via a heatmap—confirmed strong interrelationships (e.g., purchases vs. payments), indicating redundancy.

🧾 _Finding_: Monetary and frequency variables are heavily right-skewed, typical of credit card usage data.

---

## 🔧 Feature Engineering

-   **Rates**:
    -   `PURCHASES_PER_MONTH = PURCHASES / TENURE`
    -   `CASH_ADVANCE_PER_MONTH = CASH_ADVANCE / TENURE`
-   **Ratios** (NaN if denominator is 0):
    -   `ONEOFF_RATIO = ONEOFF_PURCHASES / PURCHASES`
    -   `INSTALLMENT_RATIO = INSTALLMENTS_PURCHASES / PURCHASES`
    -   `PAYMENT_RATIO = PAYMENTS / PURCHASES`
    -   `CASHADV_CREDITLIMIT_RATIO = CASH_ADVANCE / CREDIT_LIMIT`

> NaNs were later filled with zeros as a neutral choice—better than forcing arbitrary values.

---

## 🎯 Scaling

-   Applied **StandardScaler** (zero mean, unit variance) to all features—no log scaling.
-   Rationale: log transform did not adequately correct skew; ratios and scaling better preserved behavioral patterns.

---

## 🔢 Clustering Approach

-   Explored **KMeans** with k in [2…10].
-   Evaluated using:
    -   **Elbow plot** (inertia)
    -   **Silhouette score**
-   Results:
    -   Elbow method showed diminishing returns after **k=4–6**
    -   Silhouette peaked at **k=6** (~0.21), though values were modest — indicating overlapping clusters
-   Chose **k = 4** for simplicity and interpretability.

---

## 📈 Visualization

-   Ran PCA (2 components) for cluster plotting.
-   The PCA scatter plot revealed overlapping clusters—clusters exist but are not fully separated in 2D space.

---

## 🧠 Cluster Profiles (Approximate centroids)

| Cluster | Profile Description                                                                                                 |
| ------- | ------------------------------------------------------------------------------------------------------------------- |
| **0**   | **Active transactors** – high balances, frequent high-value purchases (esp. one-off), payment ratio ~1              |
| **1**   | **Moderate spenders** – installment-heavy purchases, low balances, diligent payers (payments > purchases)           |
| **2**   | **Occasional cash & purchases** – low purchase frequency, moderate cash advance usage, high payment ratios          |
| **3**   | **Heavy cash advance users** – low purchase activity, high cash advance relative to limit, high credit risk signals |

---

## 💼 Business Implications

### Marketing Strategy:

-   **Cluster 0**: Target with loyalty and upsell opportunities.
-   **Cluster 1**: Offer higher credit limits, installment bonuses.
-   **Cluster 2**: Follow-up with product recommendations or reward prompts.
-   **Cluster 3**: Monitor closely, offer supportive loans, educate on financing options.

### Risk Management:

-   **Cluster 3 (Cash advance dependent)** is high risk—potential candidates for early credit intervention.
-   **Cluster 1** is low risk and stable—eligible for growth strategies.

---

## ✅ How to Run

1. Download `CC GENERAL.csv` and place with the notebook.
2. Execute all cells sequentially in a Python 3 environment with required libraries:
