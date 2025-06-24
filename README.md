# Credit Card Customer Segmentation Analysis

## Overview

This project applies unsupervised clustering to credit card usage data from Kaggle. The goal is to segment customers based on their transaction patterns to inform marketing and risk management strategies.

The work includes:

-   Exploratory Data Analysis (EDA)
-   Feature engineering of behavioral metrics
-   KMeans clustering with cluster selection analysis
-   PCA visualization of cluster separation
-   Interpretation of cluster profiles and business implications

---

## Dataset

-   **Source:** `CC GENERAL.csv`
-   **Kaggle link:** https://www.kaggle.com/datasets/arjunbhasin2013/ccdata
-   **Records:** 8,950 customers
-   **Features:** balances, purchase amounts and types, cash advances, credit limits, payments, tenure, and engineered ratios

---

## Exploratory Data Analysis (EDA)

-   Inspected data structure, missing values, and distributions
-   Found missing values in `CREDIT_LIMIT` and `MINIMUM_PAYMENTS`, filled using median
-   Identified strong right skew in monetary variables (purchases, cash advances)
-   Visualized feature correlations using a heatmap, confirming expected relationships (e.g., purchases and payments)

---

## Feature Engineering

Created new features to reflect customer behavior:

-   `PURCHASES_PER_MONTH = PURCHASES / TENURE`
-   `CASH_ADVANCE_PER_MONTH = CASH_ADVANCE / TENURE`
-   `ONEOFF_RATIO = ONEOFF_PURCHASES / PURCHASES`
-   `INSTALLMENT_RATIO = INSTALLMENTS_PURCHASES / PURCHASES`
-   `PAYMENT_RATIO = PAYMENTS / PURCHASES`
-   `CASHADV_CREDITLIMIT_RATIO = CASH_ADVANCE / CREDIT_LIMIT`

Ratios where the denominator was zero were marked as NaN. These were later filled with zero to avoid introducing distortions into the clustering.

---

## Scaling

-   All features were scaled using StandardScaler (mean 0, standard deviation 1)
-   Log scaling was intentionally not applied because it did not materially improve the distribution symmetry
-   Ratios and rates provided better normalization for clustering purposes

---

## Clustering Approach

-   Applied KMeans with cluster counts from 2 to 10
-   Evaluated with:
    -   Elbow method: diminishing inertia returns beyond 4–6 clusters
    -   Silhouette score: peaked at 6 clusters (~0.21), indicating weak but present structure

Chose **4 clusters** for balance between interpretability and model performance.

---

## PCA Visualization

Used PCA to reduce features to two dimensions for visualization. The PCA scatter plot revealed overlapping clusters, consistent with the data forming gradients of behavior rather than sharply defined groups.

---

## Cluster Profiles

| Cluster                                  | Description                                                                           |
| ---------------------------------------- | ------------------------------------------------------------------------------------- |
| **0: Active transactors**                | High balances, frequent high-value purchases (mostly one-off), payment ratio around 1 |
| **1: Moderate spenders**                 | Low balances, installment-heavy purchases, payments greater than purchases            |
| **2: Occasional spenders with cash use** | Low purchase frequency, moderate cash advances, high payments relative to purchases   |
| **3: Cash advance dependent**            | High cash advance use relative to limit, low purchases, higher credit risk signals    |

---

## Business Implications

**Marketing:**

-   Cluster 0: Target with loyalty programs, upsell premium products
-   Cluster 1: Offer higher credit limits, encourage installment purchases
-   Cluster 2: Engage with targeted offers to increase activity
-   Cluster 3: Provide financial support products, education on alternatives to cash advances

**Risk management:**

-   Cluster 3: Monitor for credit risk, consider early interventions
-   Cluster 1: Low-risk group, good candidates for growth strategies

---

## How to Run

1. Place `CC GENERAL.csv` in the same directory as the notebook
2. Run all cells in a Python 3 environment
3. Required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`
4. Review EDA outputs, cluster selection plots, PCA visualization, and cluster summaries

---

## Next Steps

-   Engineer additional behavioral features (e.g., spend consistency, seasonality)
-   Test alternative clustering algorithms like Gaussian Mixture Models (GMM)
-   Integrate external data (e.g., demographics, credit bureau scores)
-   Build time-based models to monitor customer segment transitions

---

## Files

-   `notebook.ipynb`: Full code and visualizations
-   `README.md`: Project summary and explanation
