# Project Plan: Injury Severity Prediction for NYC Motor Vehicle Collisions

## 1. Overview

Build a reproducible data pipeline that predicts whether a NYC collision results in any injuries or fatalities, with an emphasis on data management (cleaning, transformation, feature engineering, and pipeline design) rather than complex modeling.

---

## 2. Research Question

Given collision context (time, location, vehicle types, contributing factors), can we predict if a crash will cause at least one injury or fatality?

- Target variable: `SEVERE = 1` if `(# persons injured + # persons killed) > 0`, else `0`.

---

## 3. Data and Storage

- **Source:** NYC Motor Vehicle Collisions dataset (NYPD).
- **Raw storage:** Single raw CSV (or Parquet) file as downloaded.
- **Processed storage:**
  - `collisions_clean` table/file with:
    - Core identifiers (collision ID, date/time).
    - Aggregated injury/fatality counts.
    - Cleaned location features (borough, zip, basic lat/lon).
    - Engineered features (see below).
- Keep clear versioning: `raw/`, `intermediate/`, `processed/`.

---

## 4. Data Cleaning & Transformation

1. **Filtering & basic cleaning**
   - Drop obviously corrupt rows (e.g., missing date/time, all injuries/fatalities negative or impossible).
   - Restrict to a reasonable time window (e.g., last 5–10 years) if needed.

2. **Handling missing data**
   - For `BOROUGH/ZIP`: create explicit `"Unknown"` category.
   - For coordinates: keep but add a flag for missing or invalid.
   - For contributing factors/vehicle types: group rare categories into `"Other"` and missing into `"Unknown"`.

3. **Feature engineering**
   - Time:
     - Hour of day, weekday vs weekend, month, season, rush-hour flag.
   - Location:
     - Borough, zip.
     - Optional: simple spatial clustering (e.g., bin lat/lon into grid cells).
   - Vehicles & contributing factors:
     - Count of vehicles involved.
     - Presence of specific high-level groups (e.g., truck present, two-wheeler present).
     - Top N contributing factor categories (drowsy driving, distraction, alcohol, etc.), others → `"Other"`.

4. **Train/test split**
   - Use time-based split (train on earlier years, test on later years) to mimic real deployment.
   - Store splits deterministically (e.g., year-based rule).

---

## 5. Modeling & Evaluation

1. **Baseline models**
   - Logistic Regression.
   - Random Forest (or Gradient Boosted Trees).

2. **Pipeline implementation**
   - Use `sklearn` `Pipeline` + `ColumnTransformer` for:
     - Numerical scaling (if needed).
     - Categorical encoding (one-hot or target encoding for medium-cardinality features).

3. **Metrics**
   - Accuracy, Precision, Recall, F1.
   - ROC-AUC.
   - Class imbalance handling:
     - Check baseline prevalence of `SEVERE=1`.
     - Consider class weights or resampling if necessary.

4. **Model interpretation**
   - Feature importance (for tree-based model).
   - Coefficients (for logistic regression).
   - Brief discussion of which factors/time/location aspects are most associated with severe crashes.

---

## 6. Reproducible Pipeline Design

- Single entry script/notebook that executes:
  1. Load raw data.
  2. Clean + engineer features.
  3. Save processed dataset.
  4. Train model(s) and evaluate on held-out test set.
- Use configuration (e.g., a small YAML/JSON file) to specify:
  - Input file paths.
  - Columns to use.
  - Train/test time window.

---

## 7. Deliverables

- **Code:**
  - ETL + feature engineering pipeline.
  - Modeling + evaluation scripts/notebooks.
- **Artifacts:**
  - Processed dataset (or description of how to generate it).
  - Evaluation tables and key plots (e.g., ROC curve, feature importances).
- **Report:**
  - Problem statement and motivation.
  - Data description and cleaning decisions.
  - Pipeline design and modeling approach.
  - Results, limitations, and potential extensions.
