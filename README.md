# Traffic Congestion Prediction Project

This project explores the development of a machine learning model to accurately predict traffic congestion levels. The analysis emphasizes the critical importance of model diagnostics, demonstrating why a high-performing Linear Regression model was ultimately rejected in favor of a more robust Random Forest Regressor.

---

## 1. Problem Statement

The goal of this project is to build a reliable regression model that can accurately predict the level of traffic congestion based on various features, such as location, weather, time of day, and roadwork activity.

---

## 2. Analysis & Methodology

The modeling process followed a deliberate path of building, diagnosing, and iterating.

### a. Data Preprocessing

* **Feature Engineering:** Created a comprehensive `Location` feature by combining `Area Name` and `Road/Intersection Name`.
* **Categorical Encoding:** Converted binary categorical features (e.g., 'Roadwork and Construction Activity') from 'Yes'/'No' to `1`/`0`.
* **Data Type Conversion:** Ensured all data was in the correct format for modeling (e.g., converting boolean columns to `1`/`0` and ensuring text fields were strings).

### b. Baseline Model: Linear Regression

* **Initial Model:** A Linear Regression model was first trained as a baseline.
* **Deceptive Results:** The model produced a high R-squared of **~0.92**, suggesting it explained 92% of the variance.

### c. Diagnostic Failure: Why Linear Models Failed

Despite the high R² score, a deeper diagnostic analysis revealed the model was fundamentally invalid.

1.  **Non-Linearity:** The residual plot (errors vs. predicted values) showed clear, systematic patterns and heteroscedasticity (uneven variance). This proved the underlying relationship between the features and the target was **not linear**, violating a core assumption of the model.
2.  **Severe Multicollinearity:** A Variance Inflation Factor (VIF) analysis showed high correlations between essential predictive features.

To confirm these findings, a **Ridge Regression** model (designed to handle multicollinearity) was also tested. It produced nearly identical results to the simple Linear Regression, confirming that **non-linearity was the primary problem** and that no linear-based model would be suitable for this dataset.

### d. Final Model: Random Forest Regressor

The strategy was pivoted to a non-linear, tree-based ensemble model.

* **Model Choice:** A **Random Forest Regressor** was chosen.
* **Why?** This model is inherently robust to both **multicollinearity** and **non-linear relationships**, directly addressing the two critical issues identified in the linear models.

---

## 3. Results & Conclusion

The final results clearly show the superiority and validity of the non-linear approach.

* **Linear / Ridge Regression (Invalid):**
    * **R-Squared:** ~0.92
    * **Conclusion:** This high score is **misleading**. The models are unreliable as they fail core diagnostic checks and do not accurately capture the data's true patterns.

* **Random Forest Regressor (Valid & Final Model):**
    * **R-Squared:** **~0.966**
    * **Conclusion:** This model not only achieves a higher R-squared score but is also considered **valid and genuinely strong**, as its non-linear structure correctly fits the data's underlying complexity.

---

## 4. Model Validation

The Random Forest's reliability was further confirmed by testing it against synthetic, "dummy" test data. This data was created to simulate three distinct real-world scenarios:

1.  Low Congestion
2.  Moderate Congestion
3.  High Congestion

The model performed accurately and predictably across all three simulated scenarios, verifying its robustness and readiness for deployment.

---

## 5. Technologies Used

* **Python**
* **Pandas:** For data manipulation and preprocessing.
* **Scikit-learn:** For model implementation (`LinearRegression`, `RandomForestRegressor`) and metrics (`r2_score`, `mean_squared_error`).
* **Matplotlib / Seaborn:** For data visualization and model diagnostics (e.g., residual plots).
* **Google Colab:** For iterative analysis and development.
