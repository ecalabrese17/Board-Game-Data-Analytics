# **Data Mining: Fundamentals**

This repository contains the code and resources for this project. 
It was developed for the Data Mining Course 
at the University of Pisa (A.Y. 2025/2026).

**[Read the full Project Report (PDF)](ProjectReport_DM1.pdf)**

## Authors
* Tommaso Agostini 
* Elisa Calabrese 

## About the Project
This project involves a comprehensive data mining analysis of a board game dataset. The study covers the entire data mining pipeline, from data preparation and feature engineering to the application of unsupervised and supervised machine learning techniques. The objective is to uncover underlying structural patterns, predict game characteristics, and extract meaningful association rules within the board game community.

## Dataset
The original dataset comprises 21,926 board games rated by an online community, featuring 46 attributes. After rigorous cleaning and preprocessing, the final dataset was refined to 19,729 records and 25 attributes.
* **Exclusions**: Texts (descriptions, image paths), highly sparse features, logically inconsistent records (e.g., minimum players > maximum players), and ancient games (published before 1950) were removed.
* **Imputation**: Missing values were handled using a category-aware median imputation strategy to preserve genre-specific characteristics.
* **Transformations**: Highly skewed variables were normalized using a log1p transformation, and popularity metrics were aggregated into a single robust indicator.

## Methodology & Models

### 1. Clustering
Various clustering algorithms were applied to explore the structural relationships of the dataset. The data exhibited a continuous density gradient (a "continent") rather than isolated islands.
* **Algorithms used**: K-Means, Hierarchical Clustering (Ward, Complete, Single, Average), DBSCAN, and OPTICS.
* **Key Findings**: K-Means (k=5) and Ward's Hierarchical Clustering (k=3) provided robust functional partitions. OPTICS outperformed DBSCAN by successfully identifying density "valleys" across the continuous distribution without over-generalizing.

### 2. Classification
Binary and multiclass classification tasks were performed using K-Nearest Neighbors (K-NN), Categorical Naive Bayes, and Decision Trees.
* **Binary Classification**: Aimed at predicting if a game is long (>= 60 minutes). K-NN emerged as the top performer (Accuracy 81%, AUC 0.89).
* **Multiclass Classification**: Aimed at predicting the ordinal Rating (1: Low, 2: Medium, 3: High). K-NN again achieved the best F1-score (67%), successfully handling the heavy overlap between contiguous rating categories better than tree-based or probabilistic models.

### 3. Regression
Regression models were trained to predict game complexity (GameWeight) and popularity (Avg_popularity_log).
* **Algorithms used**: Linear, Ridge, Lasso, Decision Tree, and K-NN Regressors.
* **Key Findings**: Non-linear models (Decision Tree and K-NN) consistently outperformed linear approaches. In multiple regression for GameWeight, K-NN achieved the highest R-squared (0.568), demonstrating that interactions between playtime, expansions, and complexity are distinctly non-linear.

### 4. Pattern Mining
The Apriori algorithm was utilized to extract frequent itemsets and association rules from discretized features.
* **Configuration**: Minimum support of 5% and minimum confidence of 70%.
* **Key Findings**: The extracted rules successfully identified strong niche dependencies. For instance, high-lift rules (> 5.0) accurately characterized the "Wargames" genre as being tightly associated with very long playtimes, high complexity, and low player counts (Solo/Duo). When used as a manual classifier, the top rule achieved a precision of 75%.
