# Credit Card Customer Segmentation Analysis

## Overview

This project applies unsupervised clustering techniques to a credit card customer dataset. The goal is to segment customers based on their usage patterns to support data-driven decisions in marketing and credit risk management.

The analysis includes:

-   Exploratory Data Analysis (EDA)
-   Feature engineering to quantify behavioral patterns
-   KMeans clustering with cluster evaluation
-   PCA visualization to explore cluster structure
-   Interpretation of customer segments and business insights

---

## Dataset

-   **Source:** `CC GENERAL.csv`
-   **Link:** https://www.kaggle.com/datasets/arjunbhasin2013/ccdata
-   **Samples:** 8,950 customers
-   **Features:** Card balances, purchases (by type and frequency), cash advances, payments, credit limits, and tenure

---

## Exploratory Data Analysis (EDA)

-   Reviewed structure, distributions, and missing data
-   Filled missing values in `CREDIT_LIMIT` and `MINIMUM_PAYMENTS` using median imputation
-   Visualized variable distributions and a correlation matrix
-   Observed expected relationships between key features (e.g., purchases and payments)
-   Noted strong right skew in financial features — typical for transactional data

---

## Feature Engineering

Created new features to better represent customer behavior:

-   `PURCHASES_PER_MONTH` = total purchases divided by tenure
-   `CASH_ADVANCE_PER_MONTH` = cash advance amount divided by tenure
-   `ONEOFF_RATIO` = one-off purchases divided by total purchases
-   `INSTALLMENT_RATIO` = installment purchases divided by total purchases
-   `PAYMENT_RATIO` = payments divided by total purchases
-   `CASHADV_CREDITLIMIT_RATIO` = cash advance divided by credit limit

Where division by zero was possible, values were set to `NaN` and later filled with 0 during preprocessing. This approach avoids artificial inflation and keeps the data interpretable.

---

## Data Scaling

-   Used `StandardScaler` to standardize features (mean = 0, standard deviation = 1)
-   Did not apply log scaling — ratios and standard scaling provided sufficient normalization
-   Ratios added scale-invariant behavioral insight that log transformation could not improve

---

## Clustering Methodology

-   Applied KMeans clustering for values of `k` from 2 to 10
-   Evaluated clusters using:
    -   **Elbow method:** Inertia decreased rapidly up to 4–6 clusters
    -   **Silhouette score:** Peaked around 6 clusters (~0.21), indicating weak but non-random structure

Selected **4 clusters** for balance between interpretability and performance.

---

## PCA Visualization

Used Principal Component Analysis (PCA) to project the high-dimensional dataset into two components. This helped visualize how customer clusters overlap and differentiate in a reduced feature space.

Although clusters overlapped, PCA revealed some separation, supporting the notion of soft segment boundaries rather than rigid classes.

---

## Cluster Profiles

| Cluster                                     | Profile Description                                                                                                               |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **0 – Active Transactors**                  | High balances, frequent and large one-off purchases, payment ratios near 1. Regular, engaged card users.                          |
| **1 – Moderate Installment Users**          | Lower balances, mostly installment purchases, and payment amounts typically exceeding purchases. Financially conservative.        |
| **2 – Infrequent Purchasers with Cash Use** | Low purchase frequency, occasional cash advances, but high payments relative to spending. Likely light users or strategic payers. |
| **3 – Cash Advance Dependent**              | Low purchases but heavy reliance on cash advances and high credit limit utilization. Higher credit risk profile.                  |

---

## Business Implications

### Marketing Strategy

-   **Cluster 0:** Target with rewards programs and premium product upsells
-   **Cluster 1:** Offer line increases and installment promotions
-   **Cluster 2:** Use targeted offers to encourage engagement
-   **Cluster 3:** Promote financial education, alternatives to cash advances, or lower-risk credit tools

### Credit Risk Strategy

-   **Cluster 3:** Monitor closely for risk indicators and intervene early
-   **Cluster 1:** Low-risk customers suitable for retention and growth campaigns

---

## How to Run

1. Place `CC GENERAL.csv` in the working directory
2. Run the Jupyter notebook in a Python 3 environment
3. Required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`
4. Review the outputs:
    - Data distributions
    - Correlation heatmaps
    - Cluster selection plots
    - PCA scatter plots
    - Segment summaries and interpretations

---
