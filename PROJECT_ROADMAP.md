# Project Roadmap: Telco Customer Churn Prediction
**Objective:** Predict customer churn using the Telco dataset with a focus on high recall and model explainability.
**Target Audience:** ICSSR Internship Evaluation
**Reference:** Upgrading a 5-year-old baseline with modern tabular ML techniques.

---

## Phase 1: Data Wrangling & Cleaning (The Foundation)
*Goal: Create a clean, error-free dataset for analysis.*

1.  **Load Data:** Import `WA_Fn-UseC_-Telco-Customer-Churn.csv`.
2.  **Fix `TotalCharges`:**
    * Identify blank strings (`" "`) which cause this column to be read as an object.
    * Action: Force convert to numeric (`errors='coerce'`) and fill resulting NaNs with 0.
3.  **Data Type Conversion:**
    * Ensure `SeniorCitizen` is categorical (or keep as int flag).
    * Verify `Tenure` is integer.
4.  **Sanity Check:**
    * Check for duplicates.
    * Drop `customerID` (non-predictive unique identifier).

## Phase 2: Exploratory Data Analysis (EDA)
*Goal: Understand the "Why" before the "How".*

1.  **Univariate Analysis:**
    * Plot the **Target Variable (`Churn`)** distribution (Check for imbalance).
    * Analyze numerical distributions (`MonthlyCharges`, `Tenure`) using Histograms/KDE.
2.  **Bivariate Analysis (Churn vs. X):**
    * **Categorical:** Use Stacked Bar Charts for `Contract` vs `Churn`, `PaymentMethod` vs `Churn`.
        * *Hypothesis to test:* Do Month-to-month users churn more?
    * **Numerical:** Use Boxplots for `Tenure` vs `Churn`.
        * *Hypothesis to test:* Do newer customers churn more?
3.  **Correlation Matrix:**
    * Check for multicollinearity (e.g., is `TotalCharges` highly correlated with `Tenure` * `MonthlyCharges`?).

## Phase 3: Feature Engineering (The "Secret Sauce")
*Goal: Create new signals that improve model performance.*

1.  **Tenure Cohorts:**
    * Bin `Tenure` into groups: "New" (0-12 mo), "Loyal" (12-48 mo), "Very Loyal" (>48 mo).
2.  **Service Density:**
    * Create a feature counting total services: `Num_Services = Phone + Internet + Streaming + ...`
3.  **Encoding:**
    * **Avoid Label Encoding** for non-ordinal features (like Payment Method).
    * Use **One-Hot Encoding** (for Linear Models) or allow **CatBoost/XGBoost** to handle categories natively.

## Phase 4: Modeling (Baseline vs. Advanced)
*Goal: Prove improvement over a simple approach.*

1.  **Split Data:** Train (80%) / Test (20%) with `stratify=y` to maintain churn proportion.
2.  **Baseline Model (The "Control"):**
    * Train a **Logistic Regression** model.
    * Metrics: Accuracy, F1-Score, ROC-AUC.
3.  **Advanced Model (The "Challenger"):**
    * Train **XGBoost** or **CatBoost**.
    * **Handle Imbalance:** Use `scale_pos_weight` (XGBoost) or `auto_class_weights` (CatBoost) to prioritize churners.
    * **Hyperparameter Tuning:** Use **Optuna** to find best `learning_rate`, `max_depth`, etc.

## Phase 5: Evaluation & Explainability
*Goal: Not just prediction, but insight.*

1.  **Performance Metrics:**
    * **Confusion Matrix:** Focus on False Negatives (Churners we missed).
    * **ROC-AUC Curve:** Compare Baseline vs. Advanced.
2.  **Feature Importance:**
    * Plot Global Feature Importance (Gain/Cover).
3.  **SHAP Values (Crucial for Internship):**
    * Use SHAP summary plots to show *directionality* (e.g., "High Monthly Charges increases churn risk").
    * Pick one specific customer and explain why the model predicted they would churn.

## Phase 6: Conclusion & Reporting
1.  Summarize key findings (e.g., "Fiber Optic users are high risk").
2.  Propose business actions (e.g., "Offer 1-year contract discounts to Month-to-month Fiber users").