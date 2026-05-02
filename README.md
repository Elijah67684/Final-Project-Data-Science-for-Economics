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
