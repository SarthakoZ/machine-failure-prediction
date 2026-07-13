# Machine Failure Prediction

A machine learning project that predicts machine maintenance status (`Normal` vs `Maintenance Required`) from sensor and operational data collected across industrial equipment (CNC, Drill, Lathe, Milling, and Press machines).

## Project Overview

Unplanned machine downtime is costly. This project explores a custom dataset of machine sensor readings to build a predictive model that flags machines likely to need maintenance before they fail, enabling a shift from reactive to predictive maintenance.

## Dataset

**File:** `data/Machine_Failure_Prediction_Custom_Dataset_Messy.xlsx`

- **Rows:** 505 machine records
- **Columns:** 12
- **Target variable:** `Machine_Status` (`Normal` / `Maintenance Required`)
- **Note:** The dataset is intentionally "messy" — it contains missing values and requires cleaning before modeling (see [Data Cleaning](#data-cleaning) below).

| Column | Type | Description |
|---|---|---|
| `Machine_ID` | string | Unique machine identifier |
| `Machine_Type` | string | Machine category: CNC, Drill, Lathe, Milling, Press |
| `Temperature_C` | float | Operating temperature (°C) — **has missing values** |
| `Vibration_mm_s` | float | Vibration level (mm/s) |
| `Pressure_bar` | float | System pressure (bar) |
| `Motor_Current_A` | float | Motor current draw (A) |
| `Power_kW` | float | Power consumption (kW) |
| `Operating_Hours` | int | Cumulative hours of operation |
| `Oil_Level_pct` | float | Oil level (%) — **has missing values** |
| `Maintenance_History` | string | Whether the machine has a prior maintenance record (Yes/No) |
| `Ambient_Humidity_pct` | int | Ambient humidity (%) |
| `Machine_Status` | string | **Target** — Normal / Maintenance Required |

### Class balance
- Normal: 344
- Maintenance Required: 161

### Data Cleaning
Known data quality issues to handle in preprocessing:
- `Temperature_C`: ~12 missing values
- `Oil_Level_pct`: ~23 missing values
- Duplicate rows may be present (handled via `drop_duplicates()`)

## Project Structure

```
.
├── data/
│   └── Machine_Failure_Prediction_Custom_Dataset_Messy.xlsx
├── notebooks/
│   └── Machine_source.ipynb
├── .gitignore
├── CONTEXT.md
├── README.md
└── requirements.txt
```

## Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/SarthakoZ/machine-failure-prediction.git
cd machine-failure-prediction
```

### 2. Create a virtual environment (recommended)
```bash
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the notebook
```bash
jupyter notebook notebooks/Machine_source.ipynb
```

> **Note:** The notebook currently loads the dataset with a hardcoded local Windows path (`D:\PYTHON\...`). Update the `pd.read_excel(...)` call to a relative path, e.g.:
> ```python
> df = pd.read_excel('../data/Machine_Failure_Prediction_Custom_Dataset_Messy.xlsx')
> ```
> before running, so it works on any machine.

## Roadmap
- [ ] Handle missing values (`Temperature_C`, `Oil_Level_pct`)
- [ ] Encode categorical features (`Machine_Type`, `Maintenance_History`)
- [ ] Exploratory data analysis (distributions, correlations, class balance)
- [ ] Train baseline classification models (Logistic Regression, Random Forest, etc.)
- [ ] Evaluate with precision/recall/F1 (class imbalance-aware metrics)
- [ ] Hyperparameter tuning and model selection
- [ ] Save the final model for inference
