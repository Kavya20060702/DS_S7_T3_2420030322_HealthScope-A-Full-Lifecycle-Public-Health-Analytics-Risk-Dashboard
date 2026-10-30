# Healthcare Datasets

This directory contains the healthcare datasets used for disease analysis in HealthScope.

## Datasets

### 1. Diabetes Dataset (`diabetes.csv`)

- **Dataset:** Pima Indians Diabetes Dataset
- **Records:** 768
- **Features:** 8
- **Target:** `Outcome`

**Features:**

`Pregnancies`, `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`, `DiabetesPedigreeFunction`, `Age`

**Target values:**

- `0` — No diabetes
- `1` — Diabetes

**Download Source:**
- [Kaggle – Pima Indians Diabetes Dataset](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database)
- [Direct CSV Download](https://rioultf.users.greyc.fr/uci/files/pima-indians-diabetes/pima-indians-diabetes.csv)

### 2. Heart Disease Dataset (`heart_disease.csv`)

- **Dataset:** UCI Cleveland Heart Disease Dataset
- **Records:** 303
- **Features:** 13
- **Target:** `target`

**Features:**

`age`, `sex`, `cp`, `trestbps`, `chol`, `fbs`, `restecg`, `thalach`, `exang`, `oldpeak`, `slope`, `ca`, `thal`

**Target values:**

- `0` — No heart disease
- `1` — Heart disease

**Download Source:**
- [UCI Machine Learning Repository – Heart Disease](https://archive.ics.uci.edu/dataset/45/heart+disease)
- [Download Processed Cleveland Dataset](https://archive.ics.uci.edu/static/public/45/heart+disease.zip)

**Note:** The original Cleveland dataset uses target values from 0 to 4. Convert values 1–4 into 1 if you require binary classification.

### 3. Hypertension Dataset (`hypertension.csv`)

- **Dataset:** Framingham Heart Study Dataset
- **Records:** 4,240
- **Features:** 13
- **Target:** `prevalentHyp`

**Features:**

`male`, `age`, `currentSmoker`, `cigsPerDay`, `BPMeds`, `prevalentStroke`, `diabetes`, `totChol`, `sysBP`, `diaBP`, `BMI`, `heartRate`, `glucose`

**Target values:**

- `0` — No hypertension
- `1` — Hypertension

**Download Source:**
- [Kaggle – Framingham Heart Study Dataset](https://www.kaggle.com/datasets/amanajmera1/framingham-heart-study-dataset)
- [Direct CSV Download – GitHub](https://github.com/plaguedoc000/framingham-heart-study-dataset/blob/main/framingham.csv)
- [Framingham Heart Study – Official Website](https://www.framinghamheartstudy.org/fhs-for-researchers/data-available-overview/)

### Dataset Summary

| Dataset | Records | Features |
|---|---:|---:|
| Diabetes | 768 | 8 |
| Heart Disease | 303 | 13 |
| Hypertension | 4,240 | 13 |
| **Total** | **5,311** | **34** |

## Data Usage

These datasets are intended for educational and research purposes involving healthcare data analysis and disease classification.

**Note:** Record counts represent the stated dataset sizes. Actual usable records may vary after data preprocessing. Verify the original dataset sources and licensing terms before redistributing the CSV files.
