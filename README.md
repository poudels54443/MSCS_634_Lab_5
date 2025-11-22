# MSCS 634 – Lab 5: Clustering Techniques Using DBSCAN and Hierarchical Clustering
# Name: Safal Poudel
# Course: Advanced Big Data and Data Mining (MSCS-634-B01) - Second Bi-term
# Instructor: Prof. Satish Penmatsa


## Overview
This lab applies unsupervised clustering techniques to the Wine dataset from `sklearn.datasets`.  
The goal is to compare **Agglomerative Hierarchical Clustering** and **DBSCAN** in terms of cluster structure, evaluation metrics, and visual interpretability after standardizing the features and projecting them to 2D with PCA for visualization.


## How to Run
1. Create and activate a Python environment (optional but recommended).
2. Install the required packages (if not already installed):
   ```bash
   pip install numpy pandas scikit-learn matplotlib scipy jupyter
   ```
3. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
4. Open `MSCS_634_Lab_5_Clustering.ipynb` and run all cells in order.

## Key Insights
- **Agglomerative Hierarchical Clustering** with `n_clusters=3` produced clusters that aligned reasonably well with the three true wine classes. The Silhouette score was around 0.28, and both Homogeneity and Completeness scores were close to 0.79, indicating that the unsupervised clusters map fairly well onto the known labels.
- The **dendrogram** offers a visual summary of how clusters merge at increasing linkage distances. It helps justify reasonable choices for `n_clusters` (for example, comparing 2, 3, and 4 clusters and seeing where large merges happen).
- With the initial parameter grid (`eps` in the range 0.5–0.7 and `min_samples` of 5 or 10), **DBSCAN** did not find any dense clusters in the standardized space. All points were labeled as noise, so common clustering metrics (Silhouette, Homogeneity, Completeness) were not informative in this configuration.
- The DBSCAN results emphasize how sensitive the algorithm is to **parameter selection**. To obtain useful clusters on this dataset, it would be necessary to explore larger `eps` values, different `min_samples`, or alternative feature spaces (for example, running DBSCAN directly on the PCA-transformed data with tuned parameters).

## Challenges and Decisions
- Parameter tuning for DBSCAN was the main challenge. The initial parameter combinations demonstrated a failure mode where all observations became noise, which was still useful for illustrating DBSCAN’s behavior when density thresholds are too strict.
- To keep the dendrogram readable, a random subset of samples was used instead of plotting all observations.
- PCA with two components was used for visualization to make 2D scatter plots of the clusters. This sacrificed some variance but greatly improved interpretability of the cluster shapes and separations.
