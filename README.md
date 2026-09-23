# 🛍️ Mall Shopper Profiling — Unsupervised Learning

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![Scikit--Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-F7931E?logo=scikit-learn)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![Status](https://img.shields.io/badge/Project-Completed-success)

---

## 📌 Project Overview

**Mall Shopper Profiling** is an Unsupervised Machine Learning project focused on
segmenting mall customers into meaningful shopper groups based on demographic,
income and spending behaviour.

The project applies three clustering algorithms:

- K-Means Clustering
- Agglomerative Hierarchical Clustering
- DBSCAN Clustering

The identified clusters are analysed and converted into practical retail
shopper personas that can help mall management with targeted promotions,
customer engagement, loyalty programs and retail planning.

---

## 🎯 Business Problem

A large shopping mall wants to understand the different types of customers
visiting its stores.

The retail operations team wants to answer questions such as:

- Which customers are high-income and high-spending?
- Which customers are young but have high spending behaviour?
- Which customers are more budget-conscious?
- Which customers have high income but relatively low spending?
- Can customers be grouped into meaningful shopper personas?
- Which clustering algorithm provides useful customer segmentation?

The objective is to use clustering techniques to discover natural customer
segments without using a predefined target variable.

---

## 📊 Dataset

The project uses the **Mall Customer Segmentation Dataset**.

### Dataset Source

Kaggle:

https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python

### Dataset Size

- **Rows:** 200
- **Original Features:** 5

### Original Features

| Feature | Description |
|---|---|
| CustomerID | Unique customer identifier |
| Gender | Customer gender |
| Age | Customer age |
| Annual Income (k$) | Annual income in thousands of dollars |
| Spending Score (1-100) | Spending behaviour score |

---

## 🔍 Dataset Inspection

The dataset was checked before applying clustering algorithms.

The following checks were performed:

- Dataset shape
- Column names
- Data types
- Missing values
- Duplicate records
- Gender distribution
- Numerical features
- Categorical features
- Correlation between numerical variables

### Dataset Quality

```text
Rows              : 200
Columns           : 5
Missing Values    : 0
Duplicate Rows    : 0
Female Customers  : 112
Male Customers    : 88
```

---

# 📈 Exploratory Data Analysis

The following EDA techniques were performed:

### Univariate Analysis

- Age histogram
- Annual Income histogram
- Spending Score histogram
- Age boxplot
- Annual Income boxplot
- Spending Score boxplot
- Gender countplot

### Bivariate Analysis

- Annual Income vs Spending Score
- Age vs Spending Score by Gender
- Age vs Annual Income by Gender
- Numerical correlation matrix
- Correlation heatmap

The **Annual Income vs Spending Score** plot provides the main visual basis
for customer segmentation.

---

# 🛠️ Feature Engineering

Several additional features were created before clustering.

## Gender Encoding

```text
Female → 0
Male   → 1
```

The original Gender column was retained for visualisation and interpretation.

## IncomeGroup

Annual income was divided into three equal-frequency groups using `pd.qcut()`:

```text
Low
Medium
High
```

## AgeGroup

Age was divided into:

```text
Young
Adult
Middle-Aged
Senior
```

## SpendingCategory

Spending Score was divided into:

```text
Low
Medium
High
```

---

# ⚙️ Clustering Feature Sets

## Experiment A — 2D Clustering

```text
AnnualIncome
SpendingScore
```

These two features provide the clearest visual separation of shopper groups.

## Experiment B — Additional Feature Experiment

```text
Age
AnnualIncome
SpendingScore
Gender_enc
```

The assignment refers to this as the 5D experiment, although the listed
feature set contains four variables.

---

# 📏 Feature Scaling

Since clustering algorithms are distance-sensitive, the numerical features
were standardized using:

```python
StandardScaler()
```

Separate scalers were used for the two feature experiments.

---

# 🔵 K-Means Clustering

K-Means was evaluated for:

```text
k = 2, 3, 4, 5, 6, 7, 8, 9, 10
```

Both the Elbow Method and Silhouette Score were used.

Final configuration:

```text
n_clusters = 5
init = k-means++
n_init = 20
max_iter = 500
random_state = 42
```

The 2D model achieved a Silhouette Score of approximately:

```text
0.555
```

The richer feature experiment produced approximately:

```text
0.314
```

---

# 🌳 Agglomerative Hierarchical Clustering

The following linkage methods were evaluated:

- Ward
- Complete
- Average

A Ward dendrogram was used to investigate the natural cluster structure.

The analysis produced approximately:

```text
5 clusters
```

Ward linkage produced a Silhouette Score of approximately:

```text
0.554
```

---

# 🔴 DBSCAN Clustering

DBSCAN was tuned using a 4th-nearest-neighbour distance plot.

### Epsilon

```text
0.2
0.4
0.6
0.8
1.0
1.2
```

### Min Samples

```text
3
4
5
7
10
```

Final configuration:

```text
eps = 0.4
min_samples = 10
metric = euclidean
```

### Result

```text
Clusters        : 4
Noise Points    : 51
Noise Percentage: 25.5%
```

On non-noise observations:

```text
Silhouette Score       ≈ 0.597
Davies-Bouldin Index   ≈ 0.473
Calinski-Harabasz      ≈ 263.61
```

---

# 📊 Algorithm Comparison

| Algorithm | Clusters | Silhouette | Davies-Bouldin | Calinski-Harabasz | Noise |
|---|---:|---:|---:|---:|---:|
| K-Means | 5 | ~0.555 | ~0.572 | ~248.65 | 0% |
| Agglomerative | 5 | ~0.554 | ~0.578 | ~244.41 | 0% |
| DBSCAN | 4 | ~0.597 | ~0.473 | ~263.61 | 25.5% |

### Metric Meaning

**Silhouette Score:** Higher values indicate better separation.

**Davies-Bouldin Index:** Lower values indicate better compactness and
separation.

**Calinski-Harabasz Index:** Higher values indicate stronger cluster
separation relative to within-cluster dispersion.

**Noise Percentage:** Applicable to DBSCAN because DBSCAN can identify noise.

---

# 👥 Shopper Personas

## 💎 Big Spenders

Higher-income customers with high spending scores.

**Retail Strategy:** Premium brands, luxury pop-ups and premium loyalty
benefits.

## 🌟 Young Aspirers

Younger customers with relatively lower income but high spending scores.

**Retail Strategy:** Youth-oriented offers, fashion promotions and limited-time
discounts.

## 🛍️ Mainstream Shoppers

Customers with medium income and spending behaviour.

**Retail Strategy:** Everyday shopping offers, cross-category promotions and
loyalty rewards.

## 💰 Careful Spenders

Customers with relatively high income but lower spending scores.

**Retail Strategy:** Personalised recommendations, exclusive previews and
targeted loyalty incentives.

## 🔎 Noise / Transitional Shoppers

Customers that do not sufficiently belong to one dense DBSCAN segment.

**Retail Strategy:** Collect additional behavioural information before assigning
a fixed persona.

---

# 📊 Visualisations Included

- Age Distribution
- Annual Income Distribution
- Spending Score Distribution
- Boxplots
- Gender Countplot
- Annual Income vs Spending Score
- Age vs Spending Score
- Age vs Annual Income
- Correlation Heatmap
- K-Means Elbow Curve
- K-Means Silhouette Curve
- K-Means Cluster Visualisation
- K-Means Centroids
- PCA Visualisation
- Hierarchical Dendrogram
- Truncated Dendrogram
- DBSCAN k-NN Distance Plot
- DBSCAN Hyperparameter Heatmap
- DBSCAN Cluster Visualisations

---

# 💾 Saved Models

```text
mall_scaler.pkl
mall_segmentation_model.pkl
```

The saved scaler and clustering model can be used for future shopper
classification.

---

# 🚀 New Shopper Classification

The project includes:

```python
classify_shopper()
```

The function accepts:

```text
Age
AnnualIncome
SpendingScore
Gender
```

and returns:

```text
Cluster Label
Persona Name
```

The final clustering model uses:

```text
AnnualIncome
SpendingScore
```

---

# 📁 Repository Structure

```text
Mall_Shopper_Profiling/
│
├── MallShopperSegmentation.ipynb
├── Mall_Customers.csv
├── mall_scaler.pkl
├── mall_segmentation_model.pkl
├── summary_report.md
└── README.md
```

---

# ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/patelneel9080/Mall_Shopper_Profiling.git
```

Move into the project directory:

```bash
cd Mall_Shopper_Profiling
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# ▶️ How to Run

## Google Colab

1. Open Google Colab.
2. Upload `MallShopperSegmentation.ipynb`.
3. Upload `Mall_Customers.csv`.
4. Run the notebook from top to bottom.

## Jupyter Notebook

```bash
jupyter notebook
```

Then open:

```text
MallShopperSegmentation.ipynb
```

and run all cells sequentially.

---

# 📦 requirements.txt

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
scipy
plotly
joblib
```

---

# 📄 Project Report

The detailed project report is available in:

```text
summary_report.md
```

It contains the business problem, EDA findings, feature engineering,
clustering results, shopper personas and future work.

---


# 👨‍💻 Author

**Neel Patel**

---
