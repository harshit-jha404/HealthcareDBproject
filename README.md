# 🏥 Healthcare Database & Risk Stratification Platform

An end-to-end data engineering, SQL analytics, and machine learning pipeline for healthcare management, patient risk prediction, and clinical data analysis.

---

## 📂 Project Structure

```text
├── .venv/                      # Python virtual environment
├── __pycache__/                # Python bytecode cache
├── schema_and_queries.sql      # Database schema creation scripts & complex SQL queries
├── model_training.ipynb        # Jupyter Notebook for data ingestion, feature engineering & model training
├── app.py                      # Interactive Streamlit Web Application for real-time risk prediction
├── riskmodel1.pkl              # Serialized scikit-learn Logistic Regression model
└── README.md                   # Project documentation
```

---

## 🗄️ 1. Database Schema & SQL Analytics (`schema_and_queries.sql`)

The relational database (`healthcare`) is structured to handle patient medical records, lab tests, diagnoses, and treatment tracking.

### Tables Overview:
* **`Diagnoses`**: Stores diagnostic categories and descriptions.
* **`Outcomes`**: Tracks patient discharge statuses (e.g., Recovered, Complicated, Deceased).
* **`Patients`**: Core patient table containing demographics, admission/discharge dates, foreign keys to diagnoses/outcomes, and treatment costs.
* **`Labs`**: Records specific test results and normal ranges linked to patients.

### Key SQL Analytics & Queries Included:
* **Detailed Patient Lab History**: Joins patient details with diagnosis, outcomes, and lab logs [cite: 1].
* **Average Lab Results by Diagnosis**: Computes group averages of lab results per diagnosis category [cite: 1].
* **Abnormal Lab Results Counter**: Filters and counts critical clinical flags (e.g., Blood Pressure $\ge 150$, Blood Sugar $> 120$, Cholesterol $> 200$) ordered by frequency [cite: 1].
* **High-Risk Demographics Analysis**: Identifies elderly patients ($> 65$ years old, male) with non-recovered outcomes [cite: 1].
* **Advanced Window Functions**: Utilizes `RANK()` to rank treatment costs per diagnosis and computes cumulative moving averages (`RUNNING_AVG`) for lab history over time [cite: 1].

---

## 📊 2. Machine Learning Pipeline (`model_training.ipynb`)

A complete scikit-learn workflow processing patient databases to predict patient risk and outcome metrics:
* **Data Ingestion & Merging**: Consolidates CSV datasets (`patients.csv`, `diagnoses.csv`, `outcomes.csv`, `labs.csv`) [cite: 4].
* **Feature Engineering**: Derives key clinical indicators including `LengthofStay`, `OutcomeEncoded`, `HighRisk` classification flags, and `AbnormalLabcount` [cite: 4].
* **Model Training**: Trains a **Logistic Regression** classifier (`max_iter=500`) optimized on demographic and clinical features (`Age`, `LengthofStay`, `TreatmentCost`) [cite: 4].
* **Model Persistence**: Exports the trained classifier to `riskmodel1.pkl` using `joblib` [cite: 4].

---

## 🚀 3. Streamlit Web Application (`app.py`)

An interactive web interface built with Streamlit allowing clinical staff to perform real-time risk stratification:

```bash
# Run the application locally
streamlit run app.py
```

### Features:
* Input fields for **Age**, **Length of Stay (days)**, and **Treatment Cost** [cite: 6].
* Instant classification (`High Risk` vs `Low Risk`) with probability scoring powered by the serialized machine learning model [cite: 6].

---

## 🛠️ Requirements & Environment

* **Python 3.13+**
* Key Libraries: `pandas`, `scikit-learn`, `numpy`, `joblib`, `streamlit`, `matplotlib`

---
