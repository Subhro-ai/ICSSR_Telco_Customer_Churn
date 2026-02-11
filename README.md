
# 📉 Telco Customer Churn Prediction

A production-style Machine Learning pipeline to predict customer churn using the Telco Customer Churn dataset.

The goal is to identify customers likely to leave so that businesses can take preventive action and reduce revenue loss.

---

## 🚀 Project Highlights

✅ End-to-end ML pipeline (clean → features → model → evaluation)  
✅ Professional preprocessing using ColumnTransformer + Pipeline  
✅ Feature engineering based on customer behavior  
✅ Imbalance-aware training  
✅ XGBoost & CatBoost models  
✅ Threshold optimization for business recall  
✅ Cross-validation  
✅ Model explainability with SHAP  

---

## 📊 Problem Statement

Customer churn is a major issue in telecom services. Acquiring a new customer costs 5–7x more than retaining an existing one.

Objective:
Predict whether a customer will churn (Yes/No) using demographics, contracts, billing behavior, and service usage.

This is a binary classification problem with class imbalance (~27% churn).

---

## 🧠 Approach

Pipeline:

Data Cleaning  
→ EDA  
→ Feature Engineering  
→ Preprocessing Pipeline  
→ Baseline Model  
→ XGBoost/CatBoost  
→ Cross Validation  
→ Threshold Tuning  
→ Explainability (SHAP)

---

## 🗂 Dataset

Source: Kaggle – Telco Customer Churn  

Rows: ~7,000 customers

Key features:
- tenure
- MonthlyCharges
- TotalCharges
- Contract
- InternetService
- PaymentMethod
- Services
- Churn (target)

---

## 🧹 Data Cleaning

- Converted TotalCharges to numeric
- Median imputation for missing values
- Dropped customerID
- Avoided chained assignment issues (pandas 2.x safe)

---

## 🛠 Feature Engineering

Added behavioral features:

- AvgCharge (spending pattern)
- IsNewCustomer (early churn risk)
- HasContract (loyalty signal)
- NumServices (engagement level)

These significantly improved model performance.

---

## ⚙️ Preprocessing

Implemented sklearn ColumnTransformer:

Numeric → passthrough  
Categorical → OneHotEncoder  

Benefits:
- No leakage
- Reproducible
- Cross-validation friendly
- Production ready

---

## 🤖 Models Used

Baseline:
- Logistic Regression

Advanced:
- XGBoost
- CatBoost

Tree-based boosting performs best for tabular churn problems.

---

## 📏 Evaluation Metrics

Because the dataset is imbalanced:

- ROC-AUC ⭐
- F1 Score ⭐
- Recall ⭐
- Confusion Matrix

---

## 📈 Results (Typical)

| Metric | Score |
|---------|---------|
| Accuracy | 80–85% |
| ROC-AUC | 0.88–0.90 |
| F1 Score | 0.70+ |
| Recall | 0.78+ |

---

## 🔍 Explainability

SHAP used to interpret predictions:

- Month-to-month contracts → high churn
- Fiber optic → higher churn
- Short tenure → higher churn

This provides actionable business insights.

---

## 📁 Project Structure

.
├── customer_churn_prediction.ipynb  
├── README.md  
├── requirements.txt  
└── data/

---

## ▶️ How to Run

pip install -r requirements.txt  
jupyter notebook customer_churn_prediction.ipynb

---

## 📦 Requirements

pandas  
numpy  
scikit-learn  
xgboost  
catboost  
shap  
matplotlib  
seaborn  

---

## 🎯 Key Learnings

- Feature engineering > model complexity
- Tree models dominate tabular data
- Threshold tuning improves business metrics
- Explainability matters in real applications

---

## 👤 Author

Machine Learning project demonstrating production-style tabular modeling.

---

⭐ If you found this useful, please star the repo!
