# CS210 Projects

## Customer Churn Prediction for a Telecom Company

### 1. Data Collection

* Use sample data from dummy APIs, or download a Kaggle dataset with customer reviews.
* Extract the data in Python using Pandas or API calls.

### 2. Data Storage

Choose appropriate databases for different data types:

* **Relational Database (PostgreSQL):** Customer profiles, orders, transactions.
* **NoSQL Database (MongoDB):** Unstructured data such as customer reviews, social media posts, logs.

### 3. Data Cleaning

Use Pandas to:

* Handle missing values (impute or drop).
* Detect and handle outliers.
* Address data inconsistencies.

### 4. Data Transformation

* **Feature Engineering:** Create new features (aggregations, ratios).
* **Normalization:** Min-Max scaling or Z-score normalization.

### 5. Exploratory Data Analysis (EDA)

* Visualize trends and distributions (e.g., customer age groups).
* Identify skewness or normalization.
* Use Matplotlib and Seaborn.

### 6. Sentiment Analysis

* Analyze customer reviews and classify as positive, neutral, or negative.

### 7. Database Enhancement

* Store review sentiment type in the database.
* Plot number of review types.

---

## Twitter API Project

1. Use Tweepy API to collect Twitter data (requires developer account and credentials). Apply proper rate limits.
2. Set up MongoDB and store tweets with PyMongo in JSON format.
3. Use Apache Kafka for real-time streaming; create a Kafka consumer to store tweets in MongoDB.
4. Clean tweets using `re` and NLTK (remove URLs and mentions).
5. Remove English stopwords, then tokenize and stem using NLTK.
6. Generate a word-frequency dictionary and plot word frequencies using Matplotlib.
7. Use TextBlob for sentiment analysis; classify tweets as positive, negative, or neutral, and store sentiment in MongoDB.
8. Build a real-time dashboard with Streamlit to visualize sentiment.

---

## Healthcare Data Management and Analysis

### 1. Data Collection

* Download a Kaggle hospital dataset and import using Pandas.

### 2. Data Storage

Use relational databases (MySQL) for structured patient data (records, demographics, visit history).

### 3. Data Cleaning

* Handle missing values.
* Remove duplicate records.
* Fix inconsistent formats (e.g., dates).

### 4. Data Transformation

* **Feature Engineering:** Create grouped ages or disease categories.
* **Normalization:** Scale numerical values for ML models.

### 5. Exploratory Data Analysis

* Use Matplotlib, Seaborn, or Tableau to plot trends (e.g., age groups with diseases).

### 6. Predictive Modeling

* Use Scikit-learn to build models such as readmission prediction or outbreak detection.
* Choose prediction targets based on your dataset.

### 7. Model Deployment

* Deploy models as APIs using Flask or Django.

---

## Sales Forecasting for an E-commerce Platform

### 1. Data Collection

Retrieve time-series sales data from Kaggle or UCI.

### 2. Data Storage

Store data in MySQL, AWS, or MongoDB (for unstructured portions).

### 3. Data Cleaning

* Handle missing values and outliers.
* Standardize formats, especially dates.

### 4. Data Transformation

* Create lag features (previous day’s sales).
* Generate moving averages or rolling sums.
* Decompose time series to identify seasonality and trends.

### 5. EDA

* Visualize sales trends, patterns, and correlations.

### 6. Forecasting Models

* Fit ARIMA models for stationary data with seasonality.

### 7. Model Evaluation

* Use metrics like MSE for regression; cross-entropy for classification.
* Deploy via Flask or Django.

---

## Building a Recommendation System for an Online Retailer

### 1. Data Extraction

* Download retailer dataset from Kaggle and import using Pandas.

### 2. Data Storage

* Store in MySQL; normalize tables as needed.

### 3. Data Cleaning

* Handle missing values.
* Standardize formats.
* Remove duplicates.

### 4. Data Transformation

* Convert data types.
* Create new features when needed.

### 5. EDA

* Visualize user behavior, product popularity, and correlations.

### 6. Recommendation Algorithms

* Implement:

  * Collaborative filtering
  * Content-based filtering
  * Hybrid approaches
* Use Scikit-learn or Surprise.

### 7. Model Evaluation and Deployment

* Use precision, recall, F1-score.
* Deploy using Flask or Django and integrate into retailer website.
