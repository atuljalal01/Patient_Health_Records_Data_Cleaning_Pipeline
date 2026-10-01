# Patient Health Records Data Cleaning Pipeline

## 📌 Project Overview

This project demonstrates a complete **data cleaning and preprocessing pipeline** using Python and Pandas.

The project starts with a raw patient health records dataset containing missing values, inconsistent formats, invalid values, duplicate representations, and mixed data types. The data is cleaned step by step and converted into a structured, analysis-ready dataset.

---

## 🎯 Project Objectives

* Load and inspect raw healthcare data
* Identify missing and invalid values
* Standardize column names
* Remove unnecessary whitespace
* Normalize categorical values
* Convert columns to appropriate data types
* Validate numerical ranges
* Standardize blood pressure values
* Parse multiple date formats
* Validate diagnosis codes
* Handle unknown and missing values appropriately
* Create additional structured columns
* Export a clean, analysis-ready dataset

---

## 🛠️ Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **Google Colab**
* **Git & GitHub**

---

## 📂 Project Structure

```text
Patient-Health-Records-Data-Pipeline/
│
├── data/
│   ├── Patient_Health_Records_Raw.csv
│   └── Patient_Health_Records_Cleaned.csv
│
├── notebooks/
│   └── Patient_Health_Records_Data_Cleaning.ipynb
│
├── README.md
└── .gitignore
```

---

## 📊 Dataset Information

### Raw Dataset

The raw dataset contains **10,000 patient records** and **17 original columns**.

Important fields include:

* Patient ID
* Name
* Age
* Gender
* City
* BMI
* Blood Pressure
* Heart Rate
* Cholesterol Level
* Diabetic Status
* Smoking Status
* Medications
* Last Visit Date
* Follow-Up
* Diagnosis Code
* Notes
* Disease Status

The raw data intentionally contains different types of data-quality problems to demonstrate a realistic cleaning workflow.

---

## 🧹 Data Cleaning Process

### 1. Column Name Standardization

Original column names were converted to a consistent format.

Example:

```text
Patient ID → patient_id
Blood Pressure → blood_pressure
Last Visit Date → last_visit_date
```

---

### 2. Whitespace Cleaning

Leading and trailing spaces were removed from text fields.

Blank or whitespace-only values were converted to proper missing values (`NaN`).

---

### 3. Categorical Data Cleaning

Inconsistent representations were standardized.

For example:

```text
M → Male
F → Female
male → Male
FEMALE → Female
```

Similar standardization was performed for:

* Gender
* City
* Diabetic status
* Smoking status

---

### 4. Age Cleaning

Invalid and non-numeric age values were identified.

Examples:

```text
twenty → 20
-5 → NaN
250 → NaN
```

A valid project range of **0–120 years** was applied.

---

### 5. BMI Cleaning

BMI values containing units were converted to numeric values.

Example:

```text
23 kg/m2 → 23
```

Values outside the project validation range were treated as invalid.

---

### 6. Blood Pressure Cleaning

Different representations were standardized:

```text
120 over 80 → 120/80
120 - 80   → 120/80
120/80     → 120/80
```

Blood pressure was then separated into:

```text
systolic_bp
diastolic_bp
```

Logical inconsistencies were identified and converted to missing values rather than being guessed or corrected automatically.

---

### 7. Heart Rate Cleaning

Text and invalid values were handled.

Example:

```text
eighty → 80
0 → NaN
500 → NaN
```

The project validation range used was **30–220 beats per minute**.

---

### 8. Cholesterol Cleaning

Mixed categorical and numeric cholesterol values were separated into:

```text
cholesterol_level
cholesterol_category
```

For example:

```text
190 → cholesterol_level
250 → cholesterol_level
normal → cholesterol_category
high → cholesterol_category
```

This prevents useful categorical information from being lost.

---

### 9. Medication Cleaning

Different separators were standardized.

Example:

```text
Aspirin;Metformin
Aspirin/Metformin
```

were standardized to:

```text
Aspirin, Metformin
```

---

### 10. Date Standardization

Multiple date formats were converted into a consistent date format.

Examples:

```text
2021-07-10
Apr 15 2021
20241113
09/03/2024
21/04/2024
```

All valid dates were converted to a standard date representation.

---

### 11. Follow-Up Cleaning

Follow-up values were converted into numeric days.

Example:

```text
two weeks → 14
```

The resulting values represent follow-up duration in days.

---

### 12. Diagnosis Code Validation

Diagnosis codes were checked using a structured pattern.

Examples of valid codes:

```text
A00
B20
I10
E11.9
```

Unknown and invalid diagnosis codes were converted to missing values.

---

### 13. Notes Cleaning

Extra whitespace in notes was removed while preserving the actual content.

---

### 14. Disease Status Cleaning

Disease status values were converted to numeric values:

```text
0 → No disease
1 → Disease
unknown → NaN
```

Unknown values were **not** incorrectly converted to `0`.

---

## 📈 Final Data Quality

After cleaning:

| Metric                           | Result |
| -------------------------------- | -----: |
| Records                          | 10,000 |
| Final columns                    |     20 |
| Duplicate rows                   |      0 |
| Invalid diagnosis codes          |      0 |
| Successfully parsed dates        | 10,000 |
| Invalid numeric values remaining |      0 |

### Validated Numeric Ranges

| Field        | Observed Range |
| ------------ | -------------: |
| Age          |          0–100 |
| BMI          |          15–35 |
| Heart Rate   |         50–120 |
| Systolic BP  |         90–160 |
| Diastolic BP |         60–100 |
| Cholesterol  |        190–250 |
| Follow-Up    |     14–30 days |

---

## ➕ Additional Columns Created

The cleaning process created structured fields from existing information:

```text
systolic_bp
diastolic_bp
cholesterol_category
```

These columns make the dataset easier to analyze and use for further data processing.

---

## 📋 Final Dataset Columns

The cleaned dataset contains:

```text
patient_id
name
gender
city
age
bmi
heart_rate
cholesterol_level
blood_pressure
systolic_bp
diastolic_bp
cholesterol_category
diabetic
smoker
follow_up
diagnosis_code
has_disease
last_visit_date
medications
notes
```

---

## 🔍 Key Data Cleaning Principles

This project follows several important data-quality principles:

* **Do not guess missing values unnecessarily**
* **Preserve useful information whenever possible**
* **Separate mixed-format data into structured fields**
* **Use validation rules to identify invalid values**
* **Keep unknown values different from valid negative values**
* **Standardize categorical representations**
* **Convert data types appropriately**
* **Validate the final dataset after cleaning**

---

## 🚀 How to Run the Project

### 1. Clone the repository

```bash
git clone <your-repository-url>
```

### 2. Open the notebook

Open:

```text
notebooks/Patient_Health_Records_Data_Cleaning.ipynb
```

using Google Colab or Jupyter Notebook.

### 3. Place the raw dataset in the data folder

```text
data/Patient_Health_Records_Raw.csv
```

### 4. Run the notebook

Execute the cells sequentially to reproduce the cleaning pipeline.

### 5. Generate the cleaned dataset

The final processed dataset can be saved as:

```text
data/Patient_Health_Records_Cleaned.csv
```

---

## 📁 Project Files

### `Patient_Health_Records_Raw.csv`

Original dataset containing the data-quality issues used for the cleaning exercise.

### `Patient_Health_Records_Cleaned.csv`

Final structured and cleaned dataset.

### `Patient_Health_Records_Data_Cleaning.ipynb`

Step-by-step Python notebook containing the complete cleaning process.

### `README.md`

Project documentation.

### `.gitignore`

Prevents unnecessary, temporary, and potentially sensitive files from being committed to GitHub.


---

## 📌 Project Outcome

The project transforms an inconsistent raw patient dataset into a **structured, validated, and analysis-ready dataset**.

The pipeline demonstrates practical skills in:

* Data cleaning
* Data validation
* Missing-value handling
* Data transformation
* Data type conversion
* Feature extraction
* Healthcare data preprocessing
* Pandas-based ETL workflows
* Reproducible data processing

---

## 👨‍💻 Author

**Your Name** - Atul Singh Jalal

Data Cleaning & Data Analytics Internship Project

---
