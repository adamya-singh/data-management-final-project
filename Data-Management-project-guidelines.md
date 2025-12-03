# CS 210 : Data Management in Data Science

## Course Project Guidelines

### General Instruction

You should work on a project related to the theme of the course: **data management in data science**. The scope is broad and may include data collection, storage, integration, transformation, analysis, and visualization. Choose a problem you are excited about. Flexibility will be provided if the project relates to topics and research papers covered in lectures.

There are two forms of final projects:

### 1. Research Project (Recommended) / Applied Project

Formulate your own research question on data management in data science and attempt to provide a solution (partial or preliminary results allowed). Project types can be computational, theoretical, experimental, or empirical.
Projects may be completed individually (not recommended) or in groups of 2 (recommended, maximum of 2 students).

#### Extra Notes

* **Start Early:** Begin thinking about your project as soon as possible and spend adequate time developing it.

---

# Deliverables

## 1. Project Proposal

**Due:** June 20th, 2024 at 23:59 (early submission encouraged)
**Length:** 2 pages (max 3), typed, single-spaced.

### Content Requirements

#### Define Project

* What problem are you solving?
* Strategic aspects involved?
* How does your project relate to the lectures/papers?

#### Novelty and Importance

* Why is your project important or exciting?
* Existing issues in current data management practices?
* Prior related work? (Brief summary)

#### Plan (Be Specific)

* Data: What type? How will you get it? Will you create/simulate it?
* Models/techniques/algorithms?
* Hypothesis?
* How will you evaluate your method and measure success?

---

## 2. Final Report

**Due:** July 10th, 2024 at 23:59
**Length:** 6–8 pages, typed, single-spaced.

### Content Requirements

#### Project Definition

* Problem statement, strategic aspects
* Relationship to lectures/papers
* Novelty, importance, related work
  *(May expand or revise the original proposal.)*

#### Progress and Contribution

* Data used and sourcing
* Models/techniques/algorithms implemented
* Experimental design
* Key findings and whether they support/refute hypothesis
* Method evaluation
* Advantages and limitations

#### Changes After Proposal

* Differences from the proposal
* Reasons for changes
* Bottlenecks or obstacles

---

# Note to All Students

You may use tools to help with writing, but **cannot use generated content directly**. Cite all tools, web sources, papers, and textbooks used.
You are responsible for originality and correctness. **Plagiarism is not allowed.**

---

# Project Suggestions / Examples

## 1. Customer Churn Prediction for a Telecom Company

**Objective:** Predict customer churn using historical customer data.

**Steps & Technologies**

1. Data Collection: CRM system; web scraping/APIs (e.g., reviews)
2. Data Storage: PostgreSQL; MongoDB for unstructured data
3. Data Integration: ETL; Airflow
4. Data Cleaning: Pandas
5. Data Transformation: Feature engineering; normalization
6. Exploratory Data Analysis: Matplotlib, Seaborn
7. Model Building: Logistic regression, random forests
8. Deployment: Accuracy/precision/recall; Flask/Django APIs

---

## 2. Real-Time Sentiment Analysis on Social Media

**Objective:** Real-time sentiment analysis of tweets.

**Steps & Technologies**

* Data Collection: Twitter API
* Data Storage: MongoDB
* Data Integration: Kafka; ETL pipeline
* Cleaning: Regex, NLTK
* Transformation: Tokenization, stop word removal, lemmatization
* EDA: Word/hashtag frequency, sentiment distribution
* Sentiment Analysis: TextBlob, VADER
* Dashboard: Dash or Streamlit

---

## 3. Sales Forecasting for an E-commerce Platform

**Objective:** Forecast future sales from historical data.

**Steps & Technologies**

* Data Collection
* Storage: Redshift, BigQuery
* Integration: NiFi, ETL
* Cleaning: Pandas, NumPy
* Transformation: Lag features, moving averages, seasonality handling
* EDA: Trend and seasonality visualization
* Forecasting: ARIMA, Prophet
* Evaluation & Deployment: MAE/RMSE; Flask/Django; UI for forecasts

---

## 4. Healthcare Data Management and Analysis

**Objective:** Analyze patient records to predict disease outbreaks and readmission rates.

**Steps & Technologies**

* Data Collection: Hospital databases; public health sources
* Storage: MySQL (structured), Cassandra (semi-structured)
* Integration: NiFi or Talend; Airflow
* Cleaning: Missing values, duplicates
* Transformation: Age groups, disease classification
* EDA: Trend and anomaly visualization
* Predictive Models: Scikit-learn
* Deployment: Flask/Django API; Dash dashboard

---

## 5. Recommendation System for an Online Retailer

**Objective:** Recommend products based on browsing and purchasing history.

**Steps & Technologies**

* Data Collection: Logs; scraping/API for reviews
* Storage: Data lake (S3, Azure Blob)
* Integration: ETL; Airflow
* Cleaning: Pandas, NumPy
* Transformation: User profiles, item vectors
* EDA: User behavior and product popularity
* Algorithms: Collaborative filtering, content-based, hybrid
* Evaluation & Deployment: Precision/recall/F1; Flask/Django; web integration
