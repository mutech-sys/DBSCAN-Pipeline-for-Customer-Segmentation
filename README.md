# DBSCAN-Pipeline-for-Customer-Segmentation

## What the notebook does, step by step

1. **Load the data**
   Downloads the `Mall_Customers.csv` dataset directly from GitHub and loads it into a table using pandas (a Python library for working with tables of data).

2. **Explore the data (EDA)**
   Checks the data for missing values, looks at the gender split, and plots (draws charts of) age, income, and spending score to understand the customers.

3. **Clean the data**
   Removes columns that aren't useful for clustering (`CustomerID` and `Gender`), checks for duplicate rows, and checks for outliers (values very different from the rest).

4. **Scale the data**
   Uses `StandardScaler` to put age, income, and spending score on the same scale (so no single column unfairly dominates the clustering just because its numbers are bigger).

5. **Reduce dimensions with PCA**
   Uses PCA (Principal Component Analysis — a technique that compresses many columns into fewer, while keeping most of the important information) to squeeze the data down to 2 dimensions, just so it can be plotted and visually understood.

6. **Try three clustering algorithms**
   - **K-Means**: Groups customers into a set number of clusters (`K`). The notebook uses the "elbow method" (a chart) to pick the best value of K, which turns out to be 5.
   - **Hierarchical Clustering**: Builds a tree of groupings (shown as a "dendrogram" chart) and cuts it into 5 clusters for a fair comparison with K-Means.
   - **DBSCAN**: Groups points based on density (how close points are to each other) and can mark some points as "noise" (points that don't fit any group).

7. **Score each algorithm**
   Uses the **silhouette score** (a number from -1 to 1 that measures how well-separated the clusters are — higher is better) to judge each algorithm.

8. **Compare and pick the winner**
   Puts all three algorithms' scores into one summary table and automatically picks the one with the best silhouette score. In this run, **DBSCAN** won.

9. **Save the results**
   Saves the customer data with their assigned cluster labels into a new file: `clustered_customers.csv`.

10. **Predict for new customers**
    Takes a few made-up new customers, scales their data the same way, and assigns each one to the closest matching cluster using the winning algorithm.

## Output

- **Charts**: age/income/spending distributions, PCA plot, elbow chart, dendrogram, K-distance graph, and final cluster comparison plots.
- **`clustered_customers.csv`**: the original customer data plus a `Cluster_Label` column showing which group each customer belongs to.
- **Console summary**: a table comparing K-Means, Hierarchical, and DBSCAN, plus the winning algorithm.

## Notes

- The dataset (`Mall_Customers.csv`) has 200 customers with columns: `CustomerID`, `Gender`, `Age`, `Annual_Income_k` (in thousands), and `Spending_Score` (a score from 1–100 based on shopping behavior).
- DBSCAN can label some customers as "noise" (`Cluster_Label = -1`), meaning they didn't clearly fit into any group.
