# Fraud Detection with Machine Learning

## Project Overview
This project builds an end-to-end fraud detection system for financial transactions.  
It focuses on **data understanding, feature preparation, model training, and evaluation** with special attention to **highly imbalanced datasets**.

---

## Task 1 – Data Analysis & Preprocessing
**Status: Completed**

- Datasets:
  - `Fraud_Data.csv` → target: `class`
  - `creditcard.csv` → target: `Class`
- Data cleaning and preprocessing for both datasets
- Exploratory Data Analysis (EDA) for each dataset:
  - Fraud vs non-fraud behavior
  - Feature distributions and relationships
  - Class imbalance analysis
- Prepared modeling-ready features and validated dataset quality

---

## Task 2 – Model Building & Training
**Status: Completed**

### Data Preparation
- Stratified train–test split to preserve class distribution for both datasets
- Features separated from target variable
- Class imbalance handled correctly during training

### Models Trained
- **Baseline Model:** Logistic Regression  
  - Used for interpretability and performance comparison
- **Ensemble Model:** XGBoost  
  - Tuned with basic hyperparameters (`n_estimators`, `max_depth`)
  - Selected as the final model

### Evaluation Metrics
- Confusion Matrix
- F1-Score
- AUC-PR (Primary metric due to class imbalance)

### Cross-Validation
- Stratified 5-Fold Cross-Validation for both datasets
- Stable performance across folds
- **Fraud_Data.csv:**
  - Mean AUC-PR ≈ **0.98**
  - Mean F1-Score ≈ **0.97**
- **creditcard.csv:**
  - Mean AUC-PR ≈ **0.79**
  - Mean F1-Score ≈ **0.90**

---

## Task 3 – Model Explainability & Business Insights
**Status: Completed**

### SHAP Interpretation
- **Comparison:** Compared SHAP values with built-in XGBoost feature importance. SHAP revealed that while `sex_M` and `browser` types were used by the model, they acted as significant "trust" or "risk" anchors that simple importance metrics couldn't quantify.
- **Top 5 Drivers of Fraud:**
  1. `time_since_signup_hours` (Newer accounts = Higher Risk)
  2. `purchase_value` (Higher amounts = Higher Risk)
  3. `age` (Specific age groups correlated with fraud patterns)
  4. `browser_Opera` / `browser_Safari` (Higher relative risk)
  5. `sex_M` (Non-male accounts weighted as higher risk by the model)
- **Counterintuitive Findings:** Fraudsters successfully mimicked "safe" profiles (using Internet Explorer and SEO sources) to lower their risk scores, highlighting a model blind spot.

### Local Analysis (Force Plots)
Analyzed specific cases to understand model behavior:
- **True Positive:** Correctly flagged fraud driven by an immediate purchase after signup.
- **False Positive:** Legitimate user flagged primarily due to their browser type and age.
- **False Negative:** Fraudulent transaction missed because the model over-prioritized "trust signals" like the browser and traffic source.

### Actionable Business Recommendations
1. **Velocity-Based Holds:** Implement a 24-hour "cooling period" for high-value transactions on accounts less than 6 hours old (derived from the `time_since_signup` insight).
2. **Adaptive Authentication:** Trigger Multi-Factor Authentication (MFA) for users on high-risk browsers (Opera/Safari) to reduce false positives while maintaining security.
3. **Trust-Signal Calibration:** Reduce the negative weighting (the "trust bonus") given to browsers like Internet Explorer to prevent fraudsters from masking their activity.

---

## Current Status
- Task 1: ✅ Completed  
- Task 2: ✅ Completed  
- Task 3: ✅ Completed

---

## 3. How to Run

1. **Clone the Repository:**
    ```bash
    git clone [https://github.com/AstraMeron/Fraud-detection.git](https://github.com/AstraMeron/Fraud-detection.git)
    cd Fraud-detection
    ```

2. **Create and Activate a Virtual Environment:**
    ```bash
    python -m venv venv
    ```

    **Windows (PowerShell):**
    ```bash
    .\venv\Scripts\Activate
    ```

    **Linux / macOS:**
    ```bash
    source venv/bin/activate
    ```

3. **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4. **Prepare the Data:**
    ```text
    Place the following files inside data/raw/ :
    - Fraud_Data.csv
    - IpAddress_to_Country.csv
    - creditcard.csv
    ```

5. **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```

6. **Run Notebooks:**
    ```text
    notebooks/eda-fraud-data.ipynb
    notebooks/eda-creditcard.ipynb
    notebooks/feature-engineering.ipynb
    notebooks/modeling.ipynb
    notebooks/shap-explainability.ipynb
    ```

---

## Notes
- Processed datasets are saved in `data/processed/`.
- Saved model artifacts are in `models/`.
- Task 3 results provide the logic for moving from a reactive "block-all" strategy to a proactive "risk-based" verification strategy.