# 📱 Megaline Telecom Customer Behavior Analysis

## Overview
This project analyzes the behavior of **500 Megaline customers** across two prepaid plans — **Surf** and **Ultimate** — to determine which plan generates more revenue and how usage patterns differ between them. The goal is to help the commercial department make data-driven decisions about advertising budget allocation.

---

## Tools & Libraries
- **Python** — core language
- **Pandas** — data manipulation and aggregation
- **NumPy** — numerical operations (e.g., rounding call durations)
- **Matplotlib & Seaborn** — data visualization
- **SciPy** — statistical hypothesis testing

---

## Skills Demonstrated
- Multi-table data cleaning and preprocessing
- Feature engineering (datetime extraction, GB conversion, revenue calculation)
- Exploratory Data Analysis (EDA) by plan
- Statistical hypothesis testing (Welch's t-test)
- Data visualization (line charts, histograms, boxplots)

---

## Dataset
Five interconnected CSV files covering one year of user activity:

| File | Description |
|---|---|
| `megaline_users.csv` | 500 users — age, city, plan, registration/churn date |
| `megaline_plans.csv` | Plan conditions — limits, monthly fee, overage rates |
| `megaline_calls.csv` | 137,735 call records — user, date, duration |
| `megaline_messages.csv` | 76,051 message records — user, date |
| `megaline_internet.csv` | 104,825 session records — user, date, MB used |

---

## Data Cleaning & Preprocessing
- Converted `reg_date`, `churn_date`, `call_date`, `message_date`, and `session_date` to datetime
- Rounded call durations **up** to the nearest whole minute using `np.ceil`
- Kept internet usage in MB at the session level; aggregated to monthly totals, then converted to GB and rounded up
- Extracted `month` from date columns for monthly aggregation
- Converted MB to GB in the plans table for consistent comparison
- Checked for missing values and duplicates across all five tables

---

## Revenue Calculation
Monthly revenue per user was calculated as:

```
revenue = monthly_fee
        + max(0, minutes_used - minutes_included) × rate_per_minute
        + max(0, messages_sent - messages_included) × rate_per_message
        + max(0, gb_used - gb_included) × rate_per_gb
```

---

## Key Findings

### 📞 Calls
- Calling behavior is **broadly similar** between plans
- Both Surf and Ultimate users average around **428–430 minutes** per month
- High variability exists in both groups

### 💬 Messages
- **Surf users send more messages** per month on average than Ultimate users
- The distributions show clear differences between plans

### 🌐 Internet
- **Ultimate users consume more data** per month, consistent with their larger included allowance (30 GB vs 15 GB)
- Both distributions are right-skewed, with some heavy users far exceeding their limits

### 💰 Revenue
- **Ultimate plan generates higher average monthly revenue**
- **Surf plan shows greater revenue variability** — users frequently exceed limits and pay overage charges, which drives up both mean and variance

---

## Hypothesis Tests

### Test 1 — Surf vs Ultimate Revenue
- **H₀:** Average monthly revenue from Surf users = Average monthly revenue from Ultimate users
- **H₁:** The averages are different
- **Result:** p-value < 0.05 → **Null hypothesis rejected** — there is a statistically significant difference in revenue between plans

### Test 2 — NY-NJ Region vs Other Regions
- **H₀:** Average monthly revenue from NY-NJ users = Average from other regions
- **H₁:** The averages are different
- **Result:** Determined by p-value relative to α = 0.05

---

## How to Run
1. Clone the repository
2. Open `telecom_customer_behavior_analysis.ipynb` in Jupyter Notebook or JupyterLab
3. Update dataset file paths if running locally (datasets load from `/datasets/`)
4. Run all cells in order

---

## Project Status
Completed as part of the **TripleTen Machine Learning & AI Bootcamp** — Statistical Data Analysis sprint.
