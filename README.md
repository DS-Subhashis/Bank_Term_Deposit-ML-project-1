# Bank Term Deposit Prediction — ML Notebook

## 1. What This Notebook Does (Overview)

This notebook is a Machine Learning project aimed at predicting whether a bank customer will subscribe to a *Term Deposit* or not (yes/no). It is a **Binary Classification problem**, meaning the output falls into only two categories — YES or NO.

The dataset used is **bank-full_csv.xls**, containing data from 45,211 customers — including attributes like age, job, balance, loan status, contact month, etc.

The notebook is structured into 6 clear steps, following a proper ML pipeline:

1. Data Importing  
2. Exploratory Data Analysis (EDA) + Correlation Analysis  
3. Variable Selection (Backward Elimination, Forward Selection, RFE)  
4. Baseline Model — Logistic Regression  
5. Underfitting/Overfitting Check  
6. Advanced Models — Decision Tree, Random Forest, XGBoost  

---

## 2. Step-by-Step Process

### Step 1: Data Importing
- Dataset loaded using **pandas**.  
- Although the file extension is `.xls`, the data is semicolon-separated, so `bank-full.csv.xls` with `sep=';'` was used.  
- Output: 45,211 rows and 17 columns.  

### Step 2: EDA and Correlation Analysis
- Checked for missing values → none found.  
- Target distribution: highly imbalanced (ratio ~7.5:1, more “no” than “yes”).  
- Created dashboards: target distribution, age distribution, balance distribution, job-wise rate, education-wise rate, month-wise rate.  
- Correlation heatmap: “duration” was most correlated with target but dropped due to **data leakage risk**.  
- No extreme multicollinearity found.  

**Feature Engineering:**  
- Dropped “duration”.  
- Converted “pdays = -1” into a binary column “was_contacted_before”.  
- Target variable converted to 0/1 (yes=1, no=0).  
- All categorical columns label-encoded.  

### Step 3: Variable Selection
- Used three statistical methods:  
  - **Backward Elimination** (remove insignificant features based on p-value).  
  - **Forward Selection** (add features improving AIC score).  
  - **RFE (Recursive Feature Elimination)** with Logistic Regression.  
- Final feature set chosen based on common/union results.  

### Step 4: Baseline Model — Logistic Regression
- Train/test split (80/20, stratified).  
- Features scaled using **StandardScaler**.  
- Evaluated Accuracy, Precision, Recall, F1-score, ROC-AUC.  
- Confusion Matrix plotted.  
- Output: decent accuracy but lower recall due to imbalance.  

### Step 5: Underfitting/Overfitting Check
- Compared train vs test accuracy.  
- 5-Fold Cross-Validation performed.  
- Learning Curve plotted.  
- Output: Logistic Regression showed reasonable fit (neither overfit nor underfit).  

### Step 6: Advanced Models — Decision Tree, Random Forest, XGBoost
- Applied **SMOTE** to balance training data.  
- Trained Logistic Regression, Decision Tree, Random Forest, XGBoost.  
- Compared metrics: Accuracy, Precision, Recall, F1, ROC-AUC.  
- Random Forest/XGBoost achieved best ROC-AUC (~0.77–0.80).  
- Plotted Confusion Matrix, ROC Curve, and Feature Importance.  

**Bonus Section:**  
- Added functionality to manually input new customer details and instantly predict subscription likelihood with confidence percentage.  

---

## 3. Final Summary Table

| Step | What Was Done | Output |
|------|---------------|--------|
| 1. Data Import | Loaded bank-full_csv.xls | 45,211 rows, 17 columns |
| 2. EDA + Correlation | Checked missing values, distributions, heatmap | Duration dropped (leakage), no multicollinearity |
| 3. Variable Selection | Backward Elimination + Forward Selection + RFE | Final feature set selected |
| 4. Baseline Model | Logistic Regression | Decent accuracy, ROC-AUC benchmark |
| 5. Fit Check | Train/Test gap, CV, Learning curve | Reasonable fit |
| 6. Advanced Models | Decision Tree, Random Forest, XGBoost + SMOTE | Random Forest/XGBoost best ROC-AUC (~0.77–0.80) |

---

## 4. Business Insights (Simple Terms)
- Customers with higher balances are more likely to subscribe.  
- Subscription rates vary by contact month.  
- Customers with housing loans are less likely to subscribe (possibly due to lower disposable income).  
- Customers who responded positively in past campaigns are more likely to subscribe again.  

---

---

Would you like me to also polish this into a **professional project report format** (with executive summary, methodology, results, and business recommendations), or keep it as a straightforward translation?
