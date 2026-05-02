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

<img width="975" height="562" alt="IMG_1107" src="https://github.com/user-attachments/assets/7e725996-6927-47ef-94d2-2be1f02ba908" />
<img width="1614" height="1198" alt="Rplot03" src="https://github.com/user-attachments/assets/532ce21a-87a3-4728-9198-bf860185163b" />

Income
Not included in UCI dataset.
However, population‑level data (BRFSS, WHO) consistently show higher heart disease rates in lower‑income groups — discussed in the written analysis.

# 4. Variables That Contribute Most to Prediction Accuracy
Random forest importance identifies:

oldpeak

ca

thal

thalach

cp

exang

These features reduce classification error the most and appear as top predictors in both models, strengthening the robustness of the findings.

Code Summary
analysis pipeline includes:

# Load packages
library(tidyverse)
library(caret)
library(randomForest)
library(ggplot2)

# Load and clean data
df <- read.csv("heart_disease_uci.csv")
df$target <- factor(ifelse(df$num == 0, "NoDisease", "Disease"))
factor_cols <- c("sex","cp","fbs","restecg","exang","slope","ca","thal")
df[factor_cols] <- lapply(df[factor_cols], factor)
df <- df %>% select(-id, -dataset, -num)

# Exploratory analysis
group_by(df, sex) %>% summarise(rate = mean(target == "Disease"))
ggplot(df, aes(x = target, y = oldpeak)) + geom_boxplot()

# Train/test split
train_index <- createDataPartition(df$target, p = 0.8, list = FALSE)
train <- df[train_index, ]
test  <- df[-train_index, ]


# How to Run This Project
Clone the repository

Place heart_disease_uci.csv in the project directory

Run heart_disease_analysis.R in RStudio

All visualizations and model outputs will be generated automatically


# Main Takeaway
This project shows that exercise capacity, chest pain type, ST depression, age, and thallium test results are the most powerful predictors of heart disease. Both logistic regression and random forest models converge on the same set of high‑importance variables, providing strong evidence for the medical and demographic drivers of heart disease risk.






# (full Code)
# Install 

# Final Project: Heart Disease Prediction
# Dataset: heart_disease_uci.csv

# 1. Packages --------------------------------------------------------------

packages <- c("tidyverse", "caret", "randomForest", "ggplot2")
install.packages(setdiff(packages, rownames(installed.packages())))
library(tidyverse)
library(caret)
library(randomForest)
library(ggplot2)

set.seed(123)

# 2. Load data -------------------------------------------------------------

df <- read.csv("heart_disease_uci.csv")

# Inspect structure
str(df)
names(df)

# 3. Create target + basic cleaning ---------------------------------------

# num: 0 = no disease, >0 = disease
df$target <- ifelse(df$num == 0, "NoDisease", "Disease")
df$target <- factor(df$target)

# Categorical predictors (UCI heart)
factor_cols <- c("sex", "cp", "fbs", "restecg", "exang", "slope", "ca", "thal")
df[factor_cols] <- lapply(df[factor_cols], factor)

# Drop columns not used as predictors
df <- df %>% select(-id, -dataset, -num)

# Check missing values
colSums(is.na(df))

# 4. Exploratory analysis --------------------------------------------------

# 4.1 Overall heart disease prevalence
table(df$target)
prop.table(table(df$target))

# 4.2 Heart disease by sex
df %>%
  group_by(sex) %>%
  summarise(rate = mean(target == "Disease")) %>%
  print()

ggplot(df, aes(x = sex, fill = target)) +
  geom_bar(position = "fill") +
  labs(title = "Heart Disease Rate by Sex", y = "Proportion") +
  theme_minimal()

# 4.3 Age distribution and age groups
summary(df$age)

df <- df %>%
  mutate(age_group = cut(
    age,
    breaks = c(20, 40, 55, 70, 100),
    labels = c("20–39", "40–54", "55–69", "70+"),
    right = FALSE
  ))

df %>%
  group_by(age_group) %>%
  summarise(rate = mean(target == "Disease")) %>%
  print()

ggplot(df, aes(x = age_group, y = as.numeric(target == "Disease"))) +
  stat_summary(fun = mean, geom = "bar", fill = "tomato") +
  labs(title = "Heart Disease Rate by Age Group", y = "Proportion with Disease") +
  theme_minimal()

# 4.4 Lifestyle/physiology-related variables (cp, exang, thalch, oldpeak)

df %>%
  group_by(cp) %>%
  summarise(rate = mean(target == "Disease")) %>%
  print()

ggplot(df, aes(x = cp, y = as.numeric(target == "Disease"))) +
  stat_summary(fun = mean, geom = "bar", fill = "steelblue") +
  labs(title = "Heart Disease Rate by Chest Pain Type", y = "Proportion with Disease") +
  theme_minimal()

df %>%
  group_by(exang) %>%
  summarise(rate = mean(target == "Disease")) %>%
  print()

ggplot(df, aes(x = exang, y = as.numeric(target == "Disease"))) +
  stat_summary(fun = mean, geom = "bar", fill = "darkgreen") +
  labs(title = "Heart Disease Rate by Exercise-Induced Angina", y = "Proportion with Disease") +
  theme_minimal()

ggplot(df, aes(x = target, y = thalch, fill = target)) +
  geom_boxplot() +
  labs(title = "Max Heart Rate (thalch) by Heart Disease Status") +
  theme_minimal()

ggplot(df, aes(x = target, y = oldpeak, fill = target)) +
  geom_boxplot() +
  labs(title = "ST Depression (oldpeak) by Heart Disease Status") +
  theme_minimal()

# 5. Train/test split ------------------------------------------------------

set.seed(123)
train_index <- createDataPartition(df$target, p = 0.8, list = FALSE)
train <- df[train_index, ]
test  <- df[-train_index, ]

# Align factor levels in test to training
for (col in factor_cols) {
  test[[col]] <- factor(test[[col]], levels = levels(train[[col]]))
}



