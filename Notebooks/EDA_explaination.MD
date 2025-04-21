# Exploratory Data Analysis (EDA) Projects

This repository contains two Jupyter Notebooks aimed at understanding relationships between demographic features and voting patterns, with a focus on probability distributions and statistical insights.

## Notebooks Overview

### `EDA_Probabilities.ipynb`

**Purpose:**  
Focuses on analyzing and visualizing probability based features including variables like `P(democrat|C)`.

**What is it doing:**
- Loads data and filters columns with probabilities.
- Validates that all probabilities fall within [0, 1].
- Generates descriptive statistics for numeric fields.
- Computes matrices to explore feature interdependencies.

**Visualizations:**
- **Histograms + Kernel Density Estimations :** Shows how the probability values are distributed.
- **Boxplots:** Identify outliers and spread for each probability feature.
- **Correlation Heatmaps:** Shows relationships between different probability features.
- **Split Heatmaps:** Break down large matrices into smaller readable ones, especially for features highly correlated with `P(democrat|C)`.

---

### `EDA_dataset.ipynb`

**Purpose:**  
Explores a dataset containing demographic and voting information to identify patterns and statistically significant differences between Democrat and Republican leaning counties.

**Key Actions:**
- Cleans the data to handle outliers in some features including income.
- Normalizes numerical features using standard scaling.
- Performs t tests to detect statistically significant differences between voter groups.
- Applies KMeans clustering to discover county groupings based on voting and demographics.

**Visualizations:**
- **Histograms:** Show distributions of Democrat and Republican vote counts.
- **Boxplots (Income):** Spot income outliers and distribution.
- **Scatter Plots:** Show correlations between income and votes.
- **Correlation Heatmap:** Highlights relationships between demographic and voting variables.
- **T-test Bar + P-value Line Plot:** Displays statistical differences between groups.
- **State-wise Boxplots:** Compare votes across states.
- **Elbow + Silhouette Plots:** Help choose the number of clusters for KMeans.
