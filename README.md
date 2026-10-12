# Power Network Disruption Prediction

## Overview
This project investigates whether the local topological position of a substation in a power grid helps predict future power interruptions. Using a synthetic dataset of a grid-like network of substations, the analysis compares the prefictive performance of a baseline Logistic Regression model against an enhanced model that incorporates network-derived features.

This project was completed as part of the assignment for the *Complex Systems and Applications* course.

## Tech Stack
* **Python**
* **pandas** (Data manipulation and EDA)
* **NetworkX** (Network topology construction and feature extraction)
* **scikit-learn** (Machine Learning pipeline, scaling, Logistic Regression)
* **Matplotlib** (Data visualization)

## Methodology
1. **Exploratory Data Analysis (EDA):** Analyzed the distribution of eligible substations, comparing initial attributes like `load_ratio` and `equipment_age_years` across classes.
2. **Network Construction:** Built an undirected graph representing the physical links between substations. Extracted topological features:
   * **Degree:** The number of direct physical links a substation has.
   * **Local Clustering Coefficient:** The proportion of possible links that exist among a substation's immediate neighbours, indicating local redundancy.
3. **Model Evaluation:** Trained and evaluated two Logistic Regression models using an identical train/test split:
   * **Baseline Model:** Used original features (`load_ratio`, `equipment_age_years`).
   * **Network-Enhanced Model:** Added network features (`degree`, `local_clustering`).

## Key Results
Incorporating network features significantly improved the model's predictive power on the test set:
* **F1 Score:** Increased from `0.444` to `0.750`
* **ROC AUC:** Improved from `0.828` to `0.949`

The confusion matrices revealed that the original model struggled with **false negatives** (missing 8 actual interruptions). The network-enhanced model successfully reduced these critical misses down to 3, despite a very slight increase in false alarms (false positives).

## Ethical Considerations
Applying predictive models to critical infrastructure like power grids involves significant ethical tradeoffs. Relying blindly on predictions to prioritize repairs can be risky:
* **False Negatives:** Missing an imminent interruption can leave communities without power, potentially endangering vulnerable populations (e.g., hospitals, elderly care).
* **False Positives (Alarms):** Over-predicting failures can waste limited maintenance resources and personnel time.

Therefore, such models should serve as decision-support tools rather than fully automated dispatchers. Human-in-the-loop oversight by engineers and domain experts is crucial to ensure safe, equitable, and efficient resource distribution.
