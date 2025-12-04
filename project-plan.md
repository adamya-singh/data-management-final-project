# NYC Collision Injury Prediction Pipeline

## Structure

```
course-project/
├── EDA.ipynb                              # Existing EDA
├── pipeline.ipynb                         # Full pipeline notebook (NEW)
├── collisions.db                          # SQLite database (NEW)
├── NYPD Motor Vehicle Collisions Dec 3 2025.csv
└── plan.md
```

## Notebook Structure (`pipeline.ipynb`)

### Section 1: Setup and Configuration

- Imports (pandas, numpy, sklearn, sqlite3, matplotlib, seaborn)
- Configuration variables (file paths, DB path, train/test years)

### Section 2: Data Loading and Cleaning

- Load raw CSV
- Parse dates, handle dtypes
- Handle missing values (Borough → "Unknown", etc.)
- Create target variable `SEVERE`
- Basic validation checks

### Section 3: Store Cleaned Data in SQLite

- Create SQLite database (`collisions.db`)
- Store cleaned DataFrame as `collisions_clean` table
- Demonstrate SQL queries:
  - Sample query to verify data
  - Aggregation query (e.g., count by borough, injury rate by year)
- This satisfies the data storage/management requirement

### Section 4: Feature Engineering

- Load data from SQLite (demonstrate SQL → pandas workflow)
- Time features (hour, day_of_week, is_weekend, is_rush_hour)
- Vehicle type consolidation (~10 categories)
- Contributing factor consolidation (~10 categories)

### Section 5: Train/Test Split

- Time-based split: train on 2012-2024, test on 2025
- Store splits in SQLite as `train` and `test` tables
- Print split sizes and class distributions

### Section 6: Modeling Pipeline

- Load train/test from SQLite
- Build sklearn ColumnTransformer + Pipeline
- Train Logistic Regression (class_weight='balanced')
- Train Random Forest

### Section 7: Evaluation

- Metrics table (Accuracy, Precision, Recall, F1, ROC-AUC)
- ROC curve plot
- Feature importance analysis
- Brief interpretation

## SQL Integration Points

1. **Storage**: Cleaned data → `collisions_clean` table
2. **Querying**: Demonstrate useful aggregations via SQL
3. **Splits**: Train/test sets stored as separate tables
4. **Retrieval**: Load from DB for modeling

### To-dos

- [ ] Create project structure (directories, config.yaml)
- [ ] Build data cleaning module with missing value handling and target creation
- [ ] Build feature engineering module with time, location, vehicle, and factor features
- [ ] Implement time-based train/test split (2012-2024 train, 2025 test)
- [ ] Build sklearn Pipeline with ColumnTransformer for preprocessing + models
- [ ] Create evaluation module (metrics, ROC curve, feature importance)
- [ ] Create main.py entry point to run full pipeline end-to-end

