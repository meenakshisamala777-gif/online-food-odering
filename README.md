# 🍽️ FoodWise AI — Online Food Ordering & Delivery Analytics

> **IBM SkillsBuild Internship Project**  
> End-to-end data analytics and machine learning pipeline to predict and understand online food ordering behaviour in Bengaluru, India.

---

## 📋 Table of Contents

1. [Project Overview](#-project-overview)
2. [Problem Statement](#-problem-statement)
3. [Dataset](#-dataset)
4. [Technologies Used](#-technologies-used)
5. [Project Features](#-project-features)
6. [Project Workflow](#-project-workflow)
7. [File Structure](#-file-structure)
8. [Setup & Installation](#-setup--installation)
9. [Run Instructions](#-run-instructions)
10. [Results](#-results)
11. [Key Findings](#-key-findings)
12. [Reproducing the Project](#-reproducing-the-project)
13. [License](#-license)

---

## 🔍 Project Overview

**FoodWise AI** is a complete data science project that analyses the online food ordering and delivery behaviour of customers in Bengaluru, India. Using a survey-based dataset of 388 respondents, the project performs:

- Thorough **data cleaning and preprocessing**
- Rich **exploratory data analysis (EDA)** with 11+ visualisations
- **Feature engineering** including ordinal encoding and derived features
- Training and evaluation of **6 machine learning classifiers**
- Business **insight extraction** and real-world recommendations

The ultimate goal is to predict whether a customer will order food online (`Output: Yes / No`) based on their demographic, socio-economic, and behavioural profile.

---

## ❓ Problem Statement

Food delivery platforms invest heavily in customer acquisition without a reliable means of identifying which segments are likely to convert to online ordering. Misallocated marketing spend and poorly targeted promotions reduce ROI.

> **"Given a customer's demographic, socio-economic, and behavioural profile, can we accurately predict whether they will place food orders online — and which factors drive that decision?"**

---

## 📊 Dataset

| Property | Detail |
|---|---|
| **File** | `online food delivery dataset.csv` |
| **Records** | 388 rows |
| **Features** | 13 columns |
| **Geography** | Bengaluru, Karnataka, India |
| **Source** | Customer survey across Bengaluru PIN code zones |
| **Target column** | `Output` — `Yes` (orders online) / `No` (does not) |
| **Missing values** | None |
| **Duplicates** | 103 rows (removed during cleaning → 285 unique records) |

### Feature Descriptions

| Feature | Type | Description |
|---|---|---|
| `Age` | Numerical | Respondent age in years (18–33) |
| `Gender` | Categorical | Male / Female / Prefer not to say |
| `Marital Status` | Categorical | Single / Married / Prefer not to say |
| `Occupation` | Categorical | Student / Employee / Self Employed / House wife |
| `Monthly Income` | Ordinal | No Income → Below ₹10,000 → ₹10,001–25,000 → ₹25,001–50,000 → >₹50,000 |
| `Educational Qualifications` | Ordinal | Uneducated → School → Graduate → Post Graduate → Ph.D |
| `Family size` | Numerical | Number of household members (1–6) |
| `Customer Type` | Categorical | New / Regular / Frequent |
| `latitude` / `longitude` | Numerical | Geolocation coordinates |
| `Pin code` | Categorical | Bengaluru postal zone |
| `Output` | **Target** | Does the customer order food online? Yes / No |
| `Feedback` | Categorical | Post-order sentiment — Positive / Negative |

---

## 🛠️ Technologies Used

| Library | Version | Purpose |
|---|---|---|
| Python | ≥ 3.9 | Core programming language |
| Jupyter Notebook | ≥ 7.0.0 | Interactive development environment |
| Pandas | ≥ 2.0.0 | Data loading, cleaning, manipulation |
| NumPy | ≥ 1.24.0 | Numerical operations and array handling |
| Matplotlib | ≥ 3.7.0 | Core plotting framework |
| Seaborn | ≥ 0.12.0 | Statistical visualisations and styling |
| Scikit-learn | ≥ 1.3.0 | ML models, preprocessing, evaluation metrics |
| Joblib | ≥ 1.3.0 | Model serialisation (save/load best model) |

---

## ✨ Project Features

- ✅ **Data Cleaning** — Removes duplicates, strips whitespace, handles unnamed columns, IQR outlier report
- ✅ **11+ EDA Visualisations** — Histograms, bar charts, pie charts, box plots, heatmaps, pair plots, scatter maps
- ✅ **Ordinal & Label Encoding** — Meaningful numeric mappings for income and education levels
- ✅ **Derived Features** — Age group bins, family size category, income flag
- ✅ **6 ML Classifiers** — Logistic Regression, Decision Tree, Random Forest, Gradient Boosting, SVM (RBF), KNN
- ✅ **5-Fold Stratified Cross-Validation** — Robust training evaluation with mean ± std accuracy
- ✅ **Comprehensive Evaluation** — Accuracy, Precision, Recall, F1, ROC-AUC, confusion matrices, ROC curves
- ✅ **Feature Importance** — Random Forest importances, Gradient Boosting importances, LR coefficient plot
- ✅ **Model Persistence** — Best model saved as `foodwise_best_model.pkl` via `joblib`
- ✅ **Business Insights** — 7 actionable recommendations derived from data findings

---

## 🔄 Project Workflow

```
Raw CSV Dataset
      │
      ▼
┌─────────────────┐
│  Data Loading   │  read_csv, inspect shape / dtypes / describe
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Data Cleaning  │  Drop unnamed col → strip whitespace → remove 103 duplicates
└────────┬────────┘
         │
         ▼
┌──────────────────────┐
│  Exploratory Data    │  11+ plots: distributions, crosstabs,
│  Analysis (EDA)      │  heatmap, geo scatter, pair plot
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Feature Engineering │  Ordinal encode income & education
│                      │  Label encode nominal cols
│                      │  Derive Age_Group, Family_Cat, Has_Income
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Train / Test Split  │  80:20 stratified split (random_state=42)
│  + StandardScaler    │  Scaler fit on train, transform test
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Model Training      │  6 classifiers × 5-fold CV
│  (6 Classifiers)     │
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Evaluation          │  Accuracy · Precision · Recall · F1 · AUC
│                      │  Confusion matrices · ROC curves
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Feature Importance  │  RF importances · GB importances
│  & Insights          │  LR coefficients · Business recommendations
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Model Save          │  joblib.dump → foodwise_best_model.pkl
└──────────────────────┘
```

---

## 📁 File Structure

```
IBM ptoject/
│
├── FoodWise_AI_Analytics.ipynb       # Main Jupyter Notebook (53 cells)
├── online food delivery dataset.csv  # Raw survey dataset (388 records)
├── requirements.txt                  # Python dependencies
├── README.md                         # This file
└── foodwise_best_model.pkl           # Saved best model (generated on run)
```

> **Note:** `foodwise_best_model.pkl` is created automatically when you run the final cell of the notebook.

---

## ⚙️ Setup & Installation

### Prerequisites

- Python **3.9 or higher**
- `pip` package manager
- A terminal / command prompt

### 1 — Clone or download the project

```bash
# If using Git
git clone <your-repo-url>
cd "IBM ptoject"

# Or simply place all files in the same folder
```

### 2 — (Recommended) Create a virtual environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

### 3 — Install dependencies

```bash
pip install -r requirements.txt
```

### 4 — Verify installation

```bash
python -c "import pandas, numpy, matplotlib, seaborn, sklearn, joblib; print('All dependencies OK')"
```

---

## ▶️ Run Instructions

### Option A — Jupyter Notebook (recommended)

```bash
jupyter notebook FoodWise_AI_Analytics.ipynb
```

Then in the browser: **Kernel → Restart & Run All**

### Option B — JupyterLab

```bash
jupyter lab FoodWise_AI_Analytics.ipynb
```

### Option C — VS Code

Open `FoodWise_AI_Analytics.ipynb` in VS Code with the **Jupyter** extension installed, then click **Run All**.

### Option D — Command line (script conversion)

```bash
jupyter nbconvert --to script FoodWise_AI_Analytics.ipynb
python FoodWise_AI_Analytics.py
```

> ⚠️ **Important:** Ensure `online food delivery dataset.csv` is in the **same directory** as the notebook before running.

---

## 📈 Results

### Model Performance — Test Set

| Model | CV Accuracy | Test Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---|---|---|---|---|---|
| **SVM (RBF) ★** | 82.0% | **80.7%** | 83.3% | 93.0% | 87.9% | **86.0%** |
| Random Forest | **85.5%** | 78.9% | 83.0% | 90.7% | 86.7% | 82.5% |
| Logistic Regression | 84.2% | 80.7% | 83.3% | 93.0% | 87.9% | 79.8% |
| KNN | 83.3% | **82.5%** | 83.7% | **95.3%** | **89.1%** | 72.5% |
| Gradient Boosting | 79.8% | 77.2% | 84.1% | 86.0% | 85.1% | 77.8% |
| Decision Tree | 82.0% | 77.2% | **85.7%** | 83.7% | 84.7% | 72.5% |

**★ Best overall model: SVM (RBF)** — highest ROC-AUC (86.0%), tied best accuracy, and 93% recall on the minority class.

### Top Feature Importances (Random Forest)

| Rank | Feature | Importance |
|---|---|---|
| 1 | Feedback (sentiment) | 26.87% |
| 2 | Age | 16.20% |
| 3 | Family size | 10.22% |
| 4 | Income Level | 8.76% |
| 5 | Education Level | 7.60% |

---

## 💡 Key Findings

- **77.6%** of surveyed customers order food online
- **Positive feedback** is the single strongest predictor — customers who had a good experience are ~90% likely to reorder online vs. ~52% for those with negative feedback
- **Students** (53% of dataset) dominate the user base despite having no income, driven by convenience
- **Larger families** (4–6 members) show higher ordering rates — bundle deals are well-targeted here
- **Age 21–27** is the core ordering demographic; digital-native marketing channels (app notifications, social media) are most effective
- The dataset contained **103 duplicate rows (26.5%)** — a critical cleaning step that significantly affected model reliability

---

## 🔁 Reproducing the Project

To reproduce all results exactly:

| Step | Requirement |
|---|---|
| Python version | ≥ 3.9 |
| All dependencies | Install via `pip install -r requirements.txt` |
| Dataset file | `online food delivery dataset.csv` in the project root |
| Random state | All models and splits use `random_state=42` |
| Train/test split | 80:20, `stratify=y` |
| Cross-validation | 5-fold `StratifiedKFold`, `shuffle=True`, `random_state=42` |
| Scaler | `StandardScaler` fit on training data only |
| Execution order | Run all notebook cells **top to bottom** without skipping |

> All metrics reported in this README were computed on the cleaned dataset (285 rows after deduplication) using the exact parameters above.

---

## 📄 License

This project was developed as part of the **IBM SkillsBuild Internship Programme**.  
For educational and non-commercial use only.
