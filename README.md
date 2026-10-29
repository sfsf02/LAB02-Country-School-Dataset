# Lab Assignment: Anomaly Detection and Cluster Analysis

**Course:** Computing Intelligence and Applications
**Registration Number:** 224008709

## 📌 lab Overview

This lab applies unsupervised machine learning techniques to the **Country Schools** dataset. The dataset tracks the progress of the Digital Literacy Programme across different counties, specifically monitoring the installation of Learner Digital Devices (LDDs) and Teacher Digital Devices (TDDs).

The primary objectives of this lab are:

1. **Data Preprocessing:** Clean and standardize the data for mathematical modeling.

2. **Anomaly Detection:** Identify regions with highly unusual installation patterns.

3. **Cluster Analysis:** Segment the counties into distinct groups based on their installation progress and school volume.

## 📊 Dataset

* **File:** `Country Schools.csv`

* **Key Features:**

  * `TOTALSCHOOLS`: Total number of schools in the county.

  * `TotalSchoolsInstalled`: Number of schools where devices are fully installed.

  * `SchoolsPending`: Number of schools awaiting installation.

  * `PercentageInstalled`: The installation completion rate.

  * `InstalledLDDs`: Total Learner Digital Devices installed.

  * `InstalledTDDs`: Total Teacher Digital Devices installed.

## 🛠️ Methodology & Implementation

### 1. Data Preprocessing

Before applying machine learning algorithms, the raw dataset was cleaned and transformed:

* **Handling Missing Values:** Rows containing null values (empty rows at the end of the dataset) were removed using `.dropna()`.

* **Data Type Conversion:** The `PercentageInstalled` column was transformed from a string object (containing `%` signs) into numerical floats.

* **Feature Reduction:** Identifiers that do not represent property measurements (`SNO` for county name, and `FID` for row ID) were dropped to prevent algorithm confusion.

* **Standardization:** A `StandardScaler` was applied to ensure all numerical features were on the same mathematical scale, preventing large metrics (like LDD counts) from overpowering percentage metrics during distance calculations.

### 2. Anomaly Detection (Isolation Forest)

An **Isolation Forest** model was utilized to detect data points that deviate significantly from the norm.

* **Findings:** The model successfully flagged 5 anomalies. The most notable was the "TOTAL" row, which contained the aggregate sum of all counties and acted as a massive mathematical outlier. Other anomalies included counties with unusually low installation rates (e.g., Turkana) or massively high school counts combined with near-perfect installation rates.

### 3. Cluster Analysis (K-Means)

A **K-Means clustering** algorithm ($k=3$) was deployed to segment the regions into 3 distinct groups:

* **Cluster 0 (High Performers):** Counties with a high percentage of completed installations and low pending counts.

* **Cluster 1 (The Outlier):** A cluster containing only the 'TOTAL' aggregate row, isolated due to its extreme distance from normal county metrics.

* **Cluster 2 (High Priority/Lagging):** Counties with a high number of pending schools and low percentage installation rates, indicating areas that require prioritized resource allocation.

## 🚀 How to Run the Code

1. Ensure you have Python installed along with the following libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, and `scikit-learn`.

2. Place the `Country Schools.csv` dataset in the same directory as the notebook.

3. Run the notebook cells sequentially from top to bottom.

*Created for the Computing Intelligence and Applications module.*