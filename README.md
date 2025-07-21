# feature-engineering-project
---

## 📄 Project Description

This project focuses on developing a **machine learning model** to predict product prices based on various listing features from the **Mercari dataset**, a popular secondhand marketplace. The goal is to build a lightweight, interpretable baseline model that supports pricing decisions and enhances user experience through data-driven recommendations.

By engineering meaningful features from product metadata—such as item descriptions, category hierarchy, shipping details, and brand information—a **Linear Regression model** was trained to estimate item prices. The project emphasizes **feature engineering**, **data preprocessing**, and **model interpretability** while handling memory and performance constraints using a 10,000-row sample for development.

Key techniques include:

* Cleaning and transforming textual and categorical data
* Log transformation of target variable for skew handling
* Feature selection using Chi-Square and Mutual Information
* One-hot encoding and numeric scaling
* Model evaluation using MSE and R²

This project serves as a strong baseline for more advanced models (e.g., XGBoost, deep learning) and showcases best practices in feature engineering for structured data problems.

---
## 🧩 Proposed Solution to the Business Problem

### 📌 Business Objective

The business objective was to **predict product prices** using listing features from the Mercari dataset. Key variables included product descriptions, item condition, category hierarchy, shipping details, and brand metadata.

An accurate price prediction model helps:

* Enhance **user experience** with better pricing recommendations
* Support **dynamic pricing strategies**
* Improve **inventory and sales forecasting**

---

## ✅ Proposed Solution

A **Linear Regression model** was developed using a **10,000-row sample** from the Mercari dataset to ensure memory efficiency and processing speed.

### 1. 📋 Data Preprocessing

* Cleaned and filtered data (confirmed no duplicates).
* Filled missing values:

  * `"Unknown"` for categorical fields
  * Median values for numeric fields
* Standardized string formats (e.g., lowercased, stripped whitespace).
* Cleaned text in `item_description`.
* Engineered new features such as:

  * `desc_len` (description length)
  * `log_price_norm` (log-transformed price for skew correction)
* Split `category_name` into 3 levels: `cat_1`, `cat_2`, `cat_3`.

---

### 2. 🛠️ Feature Engineering & Selection

* Applied **equal-frequency binning** to `price` and `desc_len`.
* One-hot encoded categorical features including binned categories and category splits.
* Performed feature selection using:

  * **Chi-Square (χ²)** test for categorical variables
  * **Mutual Information (MI)** for categorical and numeric features

⚠️ Due to memory constraints, MI was calculated on a **10,000-row subset** only.

---

### 3. 🔁 Data Transformation

* Standardized numeric features using `StandardScaler`.
* Combined scaled numeric and encoded categorical features into a model-ready dataset.

---

### 4. 🤖 Modeling

* Built a **Linear Regression** model using selected top features:

  * `shipping`, `brand_name_le`, `desc_len`, `item_condition_id`, `log_price_norm`
* Split data: **80% training / 20% testing**
* Evaluated using:

  * **Mean Squared Error (MSE)**
  * **R² Score**
* Visualized predictions using scatter plots with ideal prediction line (`y = x`).

---

### 5. 📈 Evaluation & Prediction

* Developed a **baseline regression model** with acceptable error rates and interpretability.
* Ran individual sample predictions to demonstrate usability for real-time pricing.

---

## 🧠 Learnings and Reflections

### 🚧 Challenges Faced

1. **High Dimensionality & Memory Constraints**

   * One-hot encoding increased memory usage significantly.
   * Scaling sparse matrices turned them dense, leading to MemoryErrors.
   * Solution: Use a sample of 10,000 rows for heavy computations like MI.

2. **Mutual Information Crash**

   * Full dataset caused overflow issues in MI due to internal float64 conversions.
   * Solution: Restricted MI analysis to a manageable subset.

3. **Data Cleaning Complexity**

   * Required careful type casting and transformation to avoid encoding/scaling errors.
   * Managed inconsistent values in `price`, `shipping`, and `category_name`.

4. **Skewed Target Variable**

   * Raw `price` was heavily right-skewed.
   * Applied **log transformation** to stabilize distribution and improve model fit.

---

### 🔍 Key Observations

* **Shipping**, **item condition**, and **brand\_name** significantly influenced price.
* **Log-transformed prices** helped improve regression metrics.
* **Chi-Square** was efficient for categorical filtering; **Mutual Information** helped uncover non-linear associations.
* **Visualizations** (boxplots, scatter plots, heatmaps) helped understand feature impact.

---

### 🎯 Key Decisions

* Sampled 10,000 rows to reduce memory issues while maintaining feature diversity.
* Standardized features **after** selection to maintain model accuracy.
* Removed high-cardinality or irrelevant fields (e.g., `train_id`, raw `item_description`).
* Chose **Linear Regression** for its speed and transparency, with potential to extend to complex models later.

---

### ✅ Final Outcome

A **lightweight, interpretable Linear Regression model** was successfully developed. It supports:

* Data-driven price recommendations for sellers
* Detection of unusual or outlier prices
* Automation of pricing for new listings

---

## 🚀 Next Steps

This model lays the groundwork for future upgrades, including:

* Advanced models like **Random Forest** or **XGBoost**
* NLP techniques for deeper text analysis
* Scaling to the full dataset using **distributed computing** or **cloud platforms**

---


