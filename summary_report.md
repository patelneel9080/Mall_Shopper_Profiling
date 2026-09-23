# Mall Shopper Profiling — Summary Report

## Business Problem

The objective of this project is to identify natural shopper segments from mall
customer data so that retail operations teams can design more targeted store
layouts, promotions and loyalty strategies. The dataset contains 200 customers
with demographic and spending information including age, gender, annual income
and spending score.

## Exploratory Data Analysis

The dataset contains 200 rows and five original columns. No missing values or
duplicate rows were found. Female customers represent 112 observations while
male customers represent 88 observations. The Annual Income versus Spending
Score scatter plot shows several visually distinct groups, suggesting that
clustering is appropriate for identifying shopper profiles.

## Feature Engineering

Gender was encoded as Female=0 and Male=1 while the original Gender column was
retained. Additional categorical features were created using IncomeGroup,
AgeGroup and SpendingCategory.

Two clustering experiments were performed. The first used AnnualIncome and
SpendingScore because these variables provide the clearest visual segmentation.
The second used Age, AnnualIncome, SpendingScore and Gender_enc to test whether
additional demographic information improved the clustering structure.

The 2D feature set produced a K-Means silhouette score of approximately 0.555,
while the richer feature set produced a lower silhouette score of approximately
0.314.

## Algorithm Comparison

K-Means was evaluated for k values from 2 through 10. The elbow and silhouette
analysis supported five clusters. The final K-Means model achieved a silhouette
score of approximately 0.555.

Agglomerative Hierarchical Clustering was evaluated using Ward, Complete and
Average linkage. Ward linkage produced a silhouette score of approximately
0.554.

DBSCAN was tuned using a 4th-nearest-neighbour distance plot and the required
hyperparameter grid. The selected configuration was eps=0.4 and
min_samples=10. It produced four clusters and 25.5% noise. On non-noise
observations, it achieved approximately 0.597 Silhouette, 0.473 Davies-Bouldin
and 263.61 Calinski-Harabasz.

## Shopper Segments

The identified profiles include:

- Big Spenders — higher-income customers with high spending scores.
- Young Aspirers — younger customers with relatively lower income but high
  spending.
- Mainstream Shoppers — customers with medium income and spending behaviour.
- Careful Spenders — higher-income customers with relatively low spending.
- Noise/Transitional Shoppers — customers that do not strongly belong to a
  dense DBSCAN group.

## Future Work

The next stage should collect richer behavioural information such as purchase
categories, transaction values, mall visit frequency, loyalty-app activity,
coupon redemption, store visits and preferred shopping times.

The segmentation could then be integrated into a real-time persona tagging API
for the mall application and used to provide more personalised offers and
customer experiences.
