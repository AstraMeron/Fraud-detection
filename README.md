# Fraud Detection with Machine Learning

## Project Overview
This project builds an end-to-end fraud detection system for financial transactions.  
It focuses on **data understanding, feature preparation, model training, and evaluation** with special attention to **highly imbalanced datasets**.

---

## Task 1 – Data Analysis & Preprocessing
**Status: Completed**

- Dataset: `Fraud_Data.csv`
- Target variable: `class` (1 = fraud, 0 = non-fraud)
- Data cleaning and preprocessing
- Exploratory Data Analysis (EDA) to understand:
  - Fraud vs non-fraud behavior
  - Feature distributions and relationships
  - Class imbalance impact
- Prepared modeling-ready features and validated dataset quality

---

## Task 2 – Model Building & Training
**Status: Completed**

### Data Preparation
- Stratified train–test split to preserve class distribution
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
- Stratified 5-Fold Cross-Validation
- Stable performance across folds
- Mean AUC-PR ≈ **0.98**
- Mean F1-Score ≈ **0.97**

### Model Selection
XGBoost was selected due to:
- Significantly higher AUC-PR
- Strong recall on fraudulent transactions
- Consistent cross-validation performance

---

## Current Status
- Task 1: ✅ Completed  
- Task 2: ✅ Completed  
- Task 3: ⏳ Pending (Model Explainability with SHAP)

---
## 3. How to Run

1. **Clone the Repository:**
    ```bash
    git clone https://github.com/AstraMeron/Fraud-detection.git
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

6. **Run Notebooks Used in Interim-2:**
    ```text
    notebooks/eda-fraud-data.ipynb
    notebooks/eda-creditcard.ipynb
    notebooks/feature-engineering.ipynb
    notebooks/modeling.ipynb
    
    ```


