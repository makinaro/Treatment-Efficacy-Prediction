# Machine Problem: Treatment Efficacy Prediction Engine

## 1. Project Overview

**Objective:**
Develop a machine learning regression system that predicts a patient's **Improvement Score** (0-10) based on their demographic profile, medical condition, and prescribed treatment plan.

**The Problem:**
Doctors currently prescribe medication based on general guidelines. However, patient responses vary wildly. By predicting the "Improvement Score" *before* treatment begins, this tool aims to help physicians choose the most effective treatment plan (Drug + Dosage + Duration) for a specific individual, effectively creating a "Personalized Medicine" recommender.

---

## 2. Technical Stack & Tools

* **Language:** Python 3.8+
* **Environment:** Jupyter Notebooks (for experimentation) or VS Code (for final scripts).
* **Core Libraries:**
* **Data Manipulation:** `pandas`, `numpy`
* **Visualization:** `matplotlib`, `seaborn`
* **Machine Learning:** `scikit-learn` (Primary), `xgboost` (Advanced/Optional)


* **Version Control:** GitHub

---

## 3. Data Dictionary

**Input Features (Independent Variables):**

1. **Demographics:** `Age` (Numeric), `Gender` (Categorical: Male/Female).
2. **Clinical Info:** `Condition` (Categorical: e.g., Hypertension, Diabetes).
3. **Treatment Plan:**
* `Drug_Name` (Categorical: e.g., Metformin, Ibuprofen).
* `Dosage_mg` (Numeric).
* `Treatment_Duration_days` (Numeric).



**Target Variable (Dependent Variable):**

* `Improvement_Score` (Numeric, Float): A score from 1-10 indicating how much the patient recovered.

---

## 4. Implementation Roadmap (Step-by-Step)

### Phase 1: Exploratory Data Analysis (EDA)

*Goal: Understand the "shape" of your data.*

1. **Univariate Analysis:** Plot histograms of `Improvement_Score`. Is it a Bell Curve (Normal Distribution) or skewed?
2. **Bivariate Analysis:**
* Does `Age` correlate with `Improvement_Score`? (Scatter plot).
* Do certain `Drugs` consistently perform better for certain `Conditions`? (Box plots).


3. **Correlation Matrix:** Use a Heatmap to see if `Dosage` and `Duration` are correlated.

### Phase 2: Data Preprocessing & Feature Engineering

*Goal: Prepare data for the model. (Crucial step for accuracy).*

1. **Encoding:** Convert `Gender`, `Condition`, and `Drug_Name` into numbers using **One-Hot Encoding** (`pd.get_dummies`).
2. **Scaling:** Normalize `Dosage_mg` and `Age` using **MinMax Scaler** or **Standard Scaler** so large numbers don't confuse the model.
3. **Feature Engineering (The "Secret Sauce"):**
* Create a new feature: `Total_Drug_Exposure = Dosage_mg * Treatment_Duration_days`.
* Create an interaction feature: `Age_Group` (e.g., Young, Middle, Senior).



### Phase 3: Model Development

*Goal: Beat the baseline.*

1. **Baseline Model:** Train a simple **Linear Regression**. Calculate the R2 Score. (Note: It will likely be low/poor. This is your baseline to beat).
2. **Advanced Model 1:** Train a **Decision Tree Regressor**. This handles non-linear data better (e.g., maybe high dosage is good for young people but bad for old people).
3. **Advanced Model 2 (Champion):** Train a **Random Forest Regressor** or **Gradient Boosting Regressor**. These combine many trees to reduce errors.

### Phase 4: Evaluation & Interpretation

*Goal: Prove your model works.*

1. **Metrics:** Report **MAE** (Mean Absolute Error) and **RMSE** (Root Mean Squared Error).
* *Interpretation:* "Our model's predictions are, on average, within +/- 0.8 points of the real score."


2. **Feature Importance:** Extract which factors mattered most. Was it the *Drug Name* or the *Duration*? (Random Forest has a built-in `.feature_importances_` attribute).

---

## 5. Success Criteria (Definition of Done)

1. **Technical Goal:** Achieve a **Mean Absolute Error (MAE) < 1.0**. (Meaning your prediction is usually less than 1 point away from the truth).
2. **Business Goal:** Identify at least one "Ineffective Treatment" pattern (e.g., "Drug A never works for Seniors").
3. **Deliverable:** A cleaned Jupyter Notebook with markdown explanations and a final `requirements.txt` file.

+
---
Sources:
https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf
https://www.geeksforgeeks.org/machine-learning/ml-one-hot-encoding/