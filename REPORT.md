# NYC Motor Vehicle Collision Severity Prediction
## CS 210 Data Management Final Report

---

## 1. Problem Statement and Motivation

**Research Question:** Given collision context (time, location, vehicle types, contributing factors), can we predict if a crash will cause at least one injury or fatality?

**Target Variable:** `SEVERE = 1` if `(# persons injured + # persons killed) > 0`, else `0`

**Motivation:**
- NYC experiences over 200,000 motor vehicle collisions annually
- Predicting severity can help emergency services prioritize response
- Understanding contributing factors can inform traffic safety policy
- Emphasis on **data management** (cleaning, transformation, feature engineering) over complex modeling

> **Reference:** See `pipeline.ipynb` Cell 0 for the full research question.

---

## 2. Relation to Course Topics

This project demonstrates key data management concepts from CS 210:

| Course Topic | Implementation |
|--------------|----------------|
| **Data Cleaning** | Handling missing values, data type conversion, invalid value replacement |
| **Data Storage** | SQLite database with primary keys, multiple tables (accidents_raw, train_set, test_set) |
| **ETL Pipeline** | Reproducible notebook pipeline: Extract (CSV) → Transform (features) → Load (SQLite) |
| **Feature Engineering** | Time features, categorical consolidation, derived variables |
| **Handling Missing Data** | KNN spatial voting for borough/zip, K-means centroid for coordinates |
| **SQL Queries** | SELECT, GROUP BY, aggregation, subqueries demonstrated |

---

## 3. Data Description and Sourcing

### Source
- **Dataset:** NYPD Motor Vehicle Collisions
- **Provider:** NYC Open Data
- **Download Date:** December 3, 2025

### Dataset Statistics
| Metric | Value |
|--------|-------|
| Total Records | 2,224,642 |
| Columns | 29 |
| Date Range | July 2012 - November 2025 |
| Target Distribution | 24.4% severe (injury/fatality) |
| Class Imbalance Ratio | 3.10:1 |

### Key Columns
- **Identifiers:** COLLISION_ID, CRASH DATE, CRASH TIME
- **Location:** BOROUGH, ZIP CODE, LATITUDE, LONGITUDE
- **Outcomes:** NUMBER OF PERSONS INJURED, NUMBER OF PERSONS KILLED
- **Context:** CONTRIBUTING FACTOR VEHICLE 1-5, VEHICLE TYPE CODE 1-5

> **Reference:** See `EDA.ipynb` Cells 1-6 for data loading and summary statistics.

---

## 4. Pipeline Design Decisions

### 4.1 Time-Based Train/Test Split

**Decision:** Train on 2012-2021, Test on 2022-2024

**Rationale:** 
- Simulates real-world deployment (predicting future from past)
- Avoids data leakage from temporal patterns
- Tests model generalization to recent years

> **Reference:** See `pipeline.ipynb` Cells 21-22 for split implementation.

### 4.2 Missing Data Imputation

#### Borough/ZIP Code: KNN Spatial Voting
- **Method:** For rows with coordinates but missing borough/zip, find 50 nearest known locations and assign by majority vote
- **Why KNN?** Spatial proximity is highly predictive of administrative boundaries
- **Result:** 478,734 rows imputed (21.5%), reducing unknown boroughs from 30.6% to 9.1%

> **Reference:** See `pipeline.ipynb` Cell 8 for KNN implementation.

#### Coordinates: K-Means Centroid
- **Method:** For rows with borough but missing coordinates, assign borough centroid
- **Result:** 37,773 rows imputed

> **Reference:** See `pipeline.ipynb` Cell 11 for K-means implementation.

### 4.3 Feature Consolidation

#### Vehicle Types
- **Problem:** 1,842 unique values (inconsistent naming, typos)
- **Solution:** Map to ~10 standardized categories using `VEHICLE_TYPE_MAP`
- **Categories:** Sedan, SUV, Taxi, Truck, Van, Bus, Motorcycle, Bike, Other, Unknown

#### Contributing Factors
- **Problem:** 61 unique values with overlapping meanings
- **Solution:** Map to ~10 categories using `CONTRIBUTING_FACTOR_MAP`
- **Categories:** Distraction, Failure to Yield, Following Too Closely, Improper Maneuver, Fatigue, Traffic Violation, Speeding, Alcohol/Drugs, Inexperience, Other, Unspecified

> **Reference:** See `pipeline.ipynb` Cell 2 for mappings, Cell 19 for application.

### 4.4 Model Selection

**Models Evaluated:**
1. Logistic Regression (interpretable baseline)
2. Random Forest (handles non-linear relationships)
3. XGBoost (gradient boosting, handles imbalanced data)

**All models use:**
- `class_weight='balanced'` or equivalent for imbalance handling
- One-hot encoding for categorical features
- Passthrough for numeric features

---

## 5. Key Findings

### 5.1 Model Performance Comparison

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|-------|----------|-----------|--------|----------|---------|
| Logistic Regression | 60.4% | 51.4% | 67.2% | 58.2% | 0.673 |
| Random Forest | 60.8% | 51.9% | 64.8% | 57.6% | 0.672 |
| **XGBoost** | 60.2% | 51.3% | **67.3%** | 58.2% | **0.676** |

**Best Model:** XGBoost (highest ROC-AUC)

> **Reference:** See `pipeline.ipynb` Cell 25 for comparison table, Cell 26 for ROC curves.

### 5.2 Top Predictive Features

From XGBoost feature importance:

1. **vehicle_type_1_bike** (10.3%) - Cyclists have higher injury risk
2. **contributing_factor_1_passing too closely** (8.0%)
3. **contributing_factor_1_failure to yield** (5.9%)
4. **contributing_factor_1_traffic control disregarded** (4.2%)
5. **contributing_factor_1_unsafe speed** (4.1%)

> **Reference:** See `pipeline.ipynb` Cells 29-30 for feature importance analysis.

### 5.3 Regression Model Results

The severity count regression model (XGBoost) performed poorly:
- RMSE: 0.85
- MAE: 0.56
- **R²: -0.012** (worse than predicting the mean)

**Interpretation:** While we can predict *whether* a crash will be severe, predicting *how many* injuries is much harder given available features.

---

## 6. Advantages and Limitations

### Advantages

1. **Reproducible Pipeline:** Single notebook executes end-to-end, from raw CSV to saved models
2. **SQL Integration:** Data stored in SQLite, queries demonstrated for aggregation
3. **Robust Missing Data Handling:** KNN spatial voting outperforms simple imputation
4. **Feature Engineering:** Consolidated 1,842 vehicle types to 10 interpretable categories
5. **Multiple Model Comparison:** Three models evaluated with consistent methodology
6. **Time-Based Validation:** Realistic evaluation simulating deployment

### Limitations

1. **Moderate Predictive Power:** ROC-AUC of 0.676 indicates room for improvement
2. **Regression Model Failure:** Cannot accurately predict injury counts
3. **33% Unspecified Factors:** Contributing factor has limited value when "Unspecified"
4. **No External Data:** Weather, traffic volume, road conditions not included
5. **Class Imbalance:** Despite balanced weights, 24.4% positive rate affects metrics
6. **No Hyperparameter Tuning:** Default/simple parameters used

---

## 7. Changes from Proposal

| Aspect | Original Proposal | Actual Implementation | Reason |
|--------|------------------|----------------------|--------|
| **Train/Test Split** | 2012-2024 / 2025 | 2012-2021 / 2022-2024 | More test data for reliable evaluation |
| **Models** | Logistic Regression, Random Forest | Added XGBoost | XGBoost handles imbalanced data better |
| **Missing Data** | Simple "Unknown" category | KNN spatial voting | Significantly better imputation accuracy |
| **Database** | collisions.db | nyc_accidents.db | Naming clarity |

---

## 8. Visualizations

### From EDA.ipynb:
- Target variable distribution bar chart
- Collisions by year trend
- Borough distribution
- Top contributing factors

> **Reference:** Run `EDA.ipynb` Cell 14 to generate `eda_summary.png`

### From pipeline.ipynb:
- ROC curve comparison (3 models)
- Feature importance bar charts
- Predicted vs actual scatter (regression)

> **Reference:** See `pipeline.ipynb` Cells 26, 28-29

---

## 9. Artifacts

| File | Description |
|------|-------------|
| `pipeline.ipynb` | Main reproducible pipeline |
| `EDA.ipynb` | Exploratory data analysis |
| `nyc_accidents.db` | SQLite database with cleaned data and train/test splits |
| `models/xgb_classifier.pkl` | Trained XGBoost classifier |
| `models/xgb_regressor.pkl` | Trained XGBoost regressor |
| `models/feature_encoder.pkl` | Fitted ColumnTransformer |
| `models/metrics.json` | Evaluation metrics |
| `eda_summary.png` | EDA visualization summary |

---

## 10. How to Reproduce

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Set up environment variable for data path
echo "FILE_PATH=Motor_Vehicle_Collisions_-_Crashes_20251202.csv" > .env

# 3. Run pipeline
jupyter notebook pipeline.ipynb
# Execute all cells in order

# 4. View EDA
jupyter notebook EDA.ipynb
```

---

## 11. References

- NYC Open Data: Motor Vehicle Collisions - Crashes
- scikit-learn documentation
- XGBoost documentation
- Course materials: CS 210 Data Management in Data Science

