# Final-Project-Data-Science-for-Economics
Heart Disease Prediction Using Machine Learning
ECON 4970 — Data Science for Economics
Elijah Bennett‑Hughes — April 2026

# Project Overview 

This project investigates the medical, demographic, and physiological factors that predict heart disease using the UCI Heart Disease Dataset. The analysis connects machine learning outputs to economic and public‑health questions:

Which factors are the strongest predictors of heart disease?

How do lifestyle‑related variables (exercise capacity, chest pain, angina) relate to disease prevalence?

Does heart disease risk differ across age groups and genders?

Which variables contribute most to prediction accuracy?

Using logistic regression and random forest models, this project identifies the most influential predictors and evaluates how demographic and physiological characteristics shape heart disease risk.

# Dataset
The dataset used is the Heart Disease UCI dataset, containing 303 patient records with:

Demographics: age, sex

Physiology: resting blood pressure, cholesterol, max heart rate

Exercise‑related variables: exercise‑induced angina, ST depression

Medical imaging: number of major vessels, thallium stress test results

Chest pain type: four clinically distinct categories

Target variable: presence or absence of heart disease

The dataset is cleaned and preprocessed to remove unu

# Methodology
This project is implemented entirely in R, using the following workflow:

1. Data Cleaning & Preparation
Converted num into a binary target variable (Disease vs. NoDisease)

Standardized categorical predictors (sex, cp, exang, thal, etc.)

Created age groups for demographic analysis

Removed unused columns (id, dataset)

2. Exploratory Data Analysis
Visualizations and summaries include:

Heart disease prevalence by sex

Age‑group disease rates

Chest pain type vs. disease

Exercise‑induced angina vs. disease

Boxplots of max heart rate and ST depression

These reveal strong patterns in exercise capacity, chest pain type, and age.

3. Machine Learning Models
Two models were trained:

Logistic Regression  
Used to interpret coefficient direction and magnitude.

Random Forest  
Used to measure variable importance and predictive contribution.

Train/test split: 80% training, 20% testingsed identifiers and convert categorical variables into factors.

# Key Findings
1. Strongest Predictors of Heart Disease
Across logistic regression and random forest importance:
Key Findings


| Variable | Why It Predicts Heart Disease |
| --- | --- |
| **oldpeak** | ST depression after exercise → ischemia indicator |
| **thalach** | Lower max heart rate → reduced exercise capacity |
| **cp** | Typical angina strongly associated with disease |
| **exang** | Exercise‑induced angina is a major risk marker |
| **ca** | Number of major vessels visualized |
| **thal** | Thallium stress test abnormalities |
thal	Thallium stress test abnormalities1. Strongest Predictors of Heart Disease
Across logistic regression and random forest impo

These consistently appear at the top of:

Logistic regression 

2. Lifestyle‑Related Insights
Although the UCI dataset does not include smoking or alcohol use, it includes exercise‑related variables that act as proxies:

exang: individuals with exercise‑induced angina have much higher disease rates

thalach: lower max heart rate → higher disease prevalence

oldpeak: higher ST depression → higher risk

These variables clearly show that reduced exercise capacity is strongly associated with heart disease.
<img width="800" height="940" alt="Rplot01" src="https://github.com/user-attachments/assets/9e45251d-9298-4c78-a709-84aafebcd326" />
<img width="1614" height="1198" alt="Rplot02" src="https://github.com/user-attachments/assets/27b6841d-85b4-44a9-a857-e0628a5d7cbb" />


# 3. Demographic Differences
Age
Heart disease prevalence increases sharply with age:

20–39: lowest risk

40–54: moderate risk

55–69: high risk

70+: highest risk

Gender
Males show a significantly higher prevalence of heart disease than females in this dataset.

