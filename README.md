# 🩺 HealthScope – A Full-Lifecycle Public Health Analytics & Risk Dashboard

**HealthScope** is an end-to-end Data Science and Machine Learning platform designed to analyze public healthcare datasets, identify disease-associated risk factors, compare predictive models, and provide interactive health-risk assessments.

The platform integrates three disease modules—**Diabetes, Heart Disease, and Hypertension**—into a unified Streamlit dashboard that combines population-level analytics, data quality assessment, model evaluation, and individual risk prediction.

> **Note:** HealthScope is an educational and research-oriented project. Its predictions are not medical diagnoses and must not replace professional medical advice.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Objectives](#-objectives)
- [Key Features](#-key-features)
- [Datasets](#-datasets)
- [Machine Learning Pipeline](#-machine-learning-pipeline)
- [Dashboard Modules](#-dashboard-modules)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Installation and Setup](#-installation-and-setup)
- [Model Evaluation](#-model-evaluation)
- [Expected Outcomes](#-expected-outcomes)
- [Limitations](#-limitations)
- [Team Members](#-team-members)
- [Supervisor](#-supervisor)
- [Medical Disclaimer](#️-medical-disclaimer)

---

## 📖 Overview

Healthcare datasets contain valuable information about patient characteristics, medical measurements, lifestyle factors, and disease outcomes. However, extracting meaningful insights from these datasets requires systematic preprocessing, exploratory analysis, statistical investigation, and predictive modeling.

HealthScope addresses this challenge through a unified data science workflow that transforms raw healthcare data into interpretable analytical insights.

The platform supports three disease-specific modules and follows a complete workflow:

**Data Collection → Data Validation → Preprocessing → Exploratory Data Analysis → Feature Engineering → Model Training → Model Evaluation → Automatic Model Selection → Risk Assessment → Interactive Visualization**

The system trains multiple machine learning classifiers for each disease module and compares their performance using standard classification metrics. The selected model is then used by the risk assessment interface.

## 🎯 Problem Statement

Healthcare datasets contain numerous interrelated variables, including age, glucose levels, blood pressure, body mass index (BMI), cholesterol, and lifestyle indicators. Understanding how these variables relate to disease outcomes can be challenging through manual analysis alone.

A unified analytical platform is needed to:

- Process and validate healthcare datasets efficiently.
- Identify patterns and relationships between health variables.
- Analyze disease distributions and potential risk factors.
- Train and compare multiple machine learning models.
- Estimate disease risk from user-provided health parameters.
- Present analytical findings through an interactive dashboard.

HealthScope addresses these needs by integrating data preprocessing, population analytics, model evaluation, and risk prediction into one application.

## 🎯 Objectives

- Utilize publicly available healthcare datasets.
- Validate datasets and handle missing or inconsistent values.
- Perform exploratory data analysis (EDA) and statistical analysis.
- Investigate relationships between health attributes and disease outcomes.
- Prepare relevant features for machine learning.
- Develop disease-specific classification models.
- Compare model performance using standard evaluation metrics.
- Automatically select a suitable model based on validation results.
- Build an interactive dashboard for population analytics and individual risk assessment.
- Present model outputs and risk factors in an accessible format.

## ✨ Key Features

### 1. Multi-Disease Analytics
Supports diabetes, heart disease, and hypertension analysis through separate disease-specific modules.

### 2. Automated Data Preprocessing
Includes dataset validation, missing-value handling, feature preparation, and numerical scaling.

### 3. Comparative Machine Learning
Trains Logistic Regression, Decision Tree, and Random Forest classifiers for each disease module.

### 4. Automatic Model Selection
Selects the best-performing validated model using F1-score and accuracy according to the implemented selection logic.

### 5. Interactive Risk Assessment
Accepts disease-specific health parameters and displays the selected model's prediction and probability score.

### 6. Population-Level Insights
Provides cohort summaries, outcome distributions, demographic breakdowns, correlation heatmaps, and descriptive statistics.

### 7. Risk Factor Analysis
Displays feature-importance rankings and clinical parameter distributions to support interpretation of the models.

### 8. Model Intelligence
Compares model metrics and confusion matrices across the available classifiers.

### 9. Data Quality Auditing
Summarizes dataset integrity, missing values, duplicate records, and raw-versus-processed dataset counts.

### 10. Assessment Reports
Provides a summary of the most recent assessment and an option to download the report as a `.txt` file.

---

## 📊 Datasets

HealthScope uses three publicly available healthcare datasets.

| Disease Module | Dataset | Records | Input Features | Target Variable |
|---|---|---:|---:|---|
| Diabetes | Pima Indians Diabetes Dataset | 768 | 8 | `Outcome` |
| Heart Disease | UCI Cleveland Heart Disease Dataset | 303 | 13 | `target` |
| Hypertension | Framingham Heart Study Dataset | 4,240 | 13 | `prevalentHyp` |
| **Total** | **Three datasets** | **5,311** | — | — |

### 1. Diabetes Dataset

**File:** `data/diabetes.csv`

Contains patient attributes associated with diabetes prediction.

Features:

- `Pregnancies`
- `Glucose`
- `BloodPressure`
- `SkinThickness`
- `Insulin`
- `BMI`
- `DiabetesPedigreeFunction`
- `Age`

**Target:** `Outcome`

- `0` — No diabetes recorded
- `1` — Diabetes recorded

### 2. Heart Disease Dataset

**File:** `data/heart_disease.csv`

Based on the UCI Cleveland Heart Disease dataset.

Features:

- `age`
- `sex`
- `cp`
- `trestbps`
- `chol`
- `fbs`
- `restecg`
- `thalach`
- `exang`
- `oldpeak`
- `slope`
- `ca`
- `thal`

**Target:** `target`

- `0` — No heart disease
- `1` — Heart disease

The target encoding follows the project's documented binary classification setup.

### 3. Hypertension Dataset

**File:** `data/hypertension.csv`

Based on the Framingham Heart Study dataset.

Features:

- `male`
- `age`
- `currentSmoker`
- `cigsPerDay`
- `BPMeds`
- `prevalentStroke`
- `diabetes`
- `totChol`
- `sysBP`
- `diaBP`
- `BMI`
- `heartRate`
- `glucose`

**Target:** `prevalentHyp`

- `0` — No hypertension recorded
- `1` — Hypertension recorded

**Dataset note:** Record counts represent the stated dataset sizes. Actual usable counts may differ after preprocessing, depending on missing values, duplicates, filtering, and the implementation.

---

## 🤖 Machine Learning Pipeline

Each disease module follows an independent model development and evaluation workflow.

### Step 1: Dataset Validation
Load the dataset and inspect its structure, feature columns, target variable, missing values, and duplicate records.

### Step 2: Data Preprocessing
Prepare the features and target, handle missing values using `SimpleImputer`, and scale numerical features using `StandardScaler`.

Preprocessing is fitted only on the training split to prevent information leakage from the test set.

### Step 3: Train-Test Split
Split the dataset into training and testing subsets using an **80:20 stratified split**.

Stratification helps preserve the target-class distribution across the subsets.

### Step 4: Model Training
Train and evaluate the following classifiers independently for each disease:

| Algorithm | Purpose |
|---|---|
| Logistic Regression | Baseline linear classification |
| Decision Tree Classifier | Rule-based classification |
| Random Forest Classifier | Ensemble-based classification |

### Step 5: Model Evaluation
Evaluate each classifier using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion matrix

### Step 6: Automatic Model Selection
Compare the evaluated models and select the best-performing validated model using the implemented F1-score and accuracy selection criteria.

### Step 7: Risk Prediction
Use the selected disease-specific model to generate a prediction from the health parameters supplied through the dashboard.

Where supported by the trained classifier, the application displays a probability score alongside the predicted class.

### Step 8: Visualization and Reporting
Present the results through population analytics, model comparison charts, risk-factor visualizations, and downloadable assessment summaries.

---

## 🖥️ Dashboard Modules

HealthScope organizes its functionality into the following sidebar sections.

| Module | Description |
|---|---|
| **Executive Dashboard** | Displays overall record totals, disease prevalence summaries, cohort composition, and epidemiological overviews. |
| **Risk Assessment** | Accepts disease-specific inputs and displays model predictions, probability scores, and relevant risk-factor information. |
| **Population Analytics** | Presents demographic distributions, outcome distributions, correlation heatmaps, and descriptive statistics. |
| **Risk Factor Insights** | Shows model feature-importance rankings and clinical parameter distributions. |
| **Model Intelligence** | Compares model accuracy, F1-scores, and confusion matrices. |
| **Data Quality** | Summarizes missing values, duplicates, dataset integrity, and preprocessing results. |
| **Assessment Report** | Displays the latest assessment summary and provides a downloadable text report. |
| **Methodology** | Documents the datasets, analytical workflow, technology stack, and project disclaimers. |

---

## 🏗️ System Architecture

The platform follows a modular architecture that separates data processing, model development, prediction, and dashboard presentation.

```text
       Public Healthcare Datasets
                  |
                  v
       Dataset Validation
                  |
                  v
        Data Preprocessing
     (Imputation and Scaling)
                  |
                  v
     Exploratory Data Analysis
                  |
                  v
        Feature Preparation
                  |
                  v
        Train-Test Splitting
                  |
                  v
       Disease-Specific Models
       /          |           \
      v           v            v
 Logistic      Decision      Random
 Regression     Tree         Forest
       \          |           /
                  v
         Model Evaluation
                  |
                  v
      Automatic Model Selection
                  |
                  v
       Saved Model Artifacts
                  |
                  v
       Streamlit Dashboard
       /         |          \
      v          v           v
 Population    Risk        Reports &
 Analytics   Assessment   Visualizations
```

The actual execution order, persistence mechanism, and model-loading behavior are determined by the implementation in `src/` and `app.py`.

---

## 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Dashboard Framework | Streamlit |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn |
| Data Visualization | Matplotlib, Seaborn, Plotly |
| Preprocessing | SimpleImputer, StandardScaler |
| Model Persistence | Joblib / Pickle |
| Development Environment | VS Code, Python environment |
| Version Control | Git, GitHub |

The exact installed packages and versions are specified in `requirements.txt`.

---

## 📁 Project Structure

```text
HealthScope/
│
├── app.py
├── requirements.txt
├── README.md
│
├── .streamlit/
│   └── config.toml
│
├── data/
│   ├── diabetes.csv
│   ├── heart_disease.csv
│   └── hypertension.csv
│
├── models/
│   ├── diabetes/
│   ├── heart_disease/
│   └── hypertension/
│
└── src/
    ├── __init__.py
    ├── preprocessing.py
    ├── eda.py
    ├── train_models.py
    └── prediction.py
```

### Main Files

- **`app.py`** — Main Streamlit dashboard and user interface.
- **`requirements.txt`** — Python dependency list.
- **`src/preprocessing.py`** — Dataset validation and preprocessing pipelines.
- **`src/eda.py`** — Exploratory data analysis and visualization functions.
- **`src/train_models.py`** — Disease-specific model training and evaluation.
- **`src/prediction.py`** — Prediction and inference pipeline.
- **`data/`** — Input healthcare datasets.
- **`models/`** — Saved model artifacts, where generated or supplied by the project.

---

## 🚀 Installation and Setup

### Prerequisites

Ensure that Python and pip are installed on your system.

### 1. Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd HealthScope
```

Replace the placeholder with your actual GitHub repository URL.

### 2. Create a Virtual Environment (Recommended)

**Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

**Linux/macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Train the Models (Optional)

If the required trained model artifacts are not already available, execute:

```bash
python src/train_models.py
```

This step depends on the training script and the required datasets being available in the expected locations.

### 5. Launch the Dashboard

```bash
streamlit run app.py
```

Open the local URL displayed in the terminal, typically:

```text
http://localhost:8501
```

### 6. Explore HealthScope

Use the sidebar to navigate between population analytics, risk assessment, model evaluation, data quality, and assessment reporting.

---

## 📈 Model Evaluation

The project evaluates its classification models using standard metrics.

| Metric | Purpose |
|---|---|
| Accuracy | Measures the proportion of correct predictions. |
| Precision | Measures the proportion of positive predictions that are correct. |
| Recall | Measures the proportion of actual positive cases identified. |
| F1-score | Balances precision and recall through their harmonic mean. |
| Confusion Matrix | Summarizes correct and incorrect predictions by class. |

For binary classification:

\[
\text{Accuracy} =
\frac{TP+TN}{TP+TN+FP+FN}
\]

\[
\text{Precision} = \frac{TP}{TP+FP}
\]

\[
\text{Recall} = \frac{TP}{TP+FN}
\]

\[
F_1 = 2 \cdot
\frac{\text{Precision}\cdot\text{Recall}}
{\text{Precision}+\text{Recall}}
\]

Here, \(TP\), \(TN\), \(FP\), and \(FN\) denote true positives, true negatives, false positives, and false negatives.

**Experimental results:** Actual accuracy, precision, recall, F1-score, and confusion-matrix values should be reported from the executed training and evaluation pipeline. No performance values are claimed in this README because no verified benchmark results are provided here.

---

## 🌟 Expected Outcomes

HealthScope is designed to provide:

- A unified interface for three healthcare disease datasets.
- Cleaned and analysis-ready data.
- Visual insights into health attributes and disease outcomes.
- Comparative evaluation of multiple machine learning classifiers.
- Disease-specific individual risk predictions.
- Automatic selection of a suitable model based on evaluation metrics.
- A dashboard integrating population analytics, model intelligence, and reporting.
- A practical demonstration of an end-to-end data science workflow.

The platform demonstrates how data analytics and machine learning can support the exploration of public health patterns and preliminary risk assessment.

---

## ⚠️ Limitations

- The models are trained on specific public datasets and may not generalize to every population or clinical setting.
- Dataset quality, class imbalance, missing values, and measurement differences can affect model performance.
- Model predictions represent statistical estimates and should not be interpreted as confirmed diagnoses.
- A probability score is not necessarily a clinically calibrated estimate of disease probability.
- Feature importance and predictive associations do not establish causation.
- External clinical validation, prospective testing, and fairness assessment are necessary before considering clinical deployment.
- Model performance must be interpreted using the actual test results and the limitations of the underlying datasets.

---

## 👥 Team Members

| Name | University ID |
|---|---|
| Masuma Fathema | 2420030400 |
| Ch. Bhargavi Devi | 2420030588 |
| Dama Poojitha | 2420030697 |
| P. Kavya Sai | 2420030322 |

**Course:** Data Science — 24AD3107  
**Academic Year:** 2026–2027

## 👩‍🏫 Supervisor

**Mrs. Bonagani Prathusha**  
Department of Computer Science and Engineering  
KLH CSE, Bowrampet Campus

---

## ⚕️ Medical Disclaimer

HealthScope is developed strictly for educational, academic, and data science demonstration purposes.

The application is not a medical device and is not intended to diagnose, treat, cure, or prevent any disease. Predictions and visualizations must not be used as a substitute for professional medical advice, diagnosis, or treatment. Users should consult qualified healthcare professionals for medical decisions.

---

## 📌 Project Summary

**HealthScope brings together healthcare data preprocessing, exploratory analytics, machine learning, model comparison, and interactive risk assessment in a unified public health dashboard.**

By integrating three disease-specific workflows into one platform, the project demonstrates a practical application of data science and machine learning for exploring health-related patterns and communicating predictive insights.

