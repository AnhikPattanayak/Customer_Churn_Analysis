# 📉 Customer Churn Analysis

A data analytics project exploring telecom customer data to uncover the drivers behind customer churn — using **Python**, **Jupyter Notebook**, and **Power BI**.

---

## 📌 Project Overview

This project analyzes **7,043 telecom customer records** to understand who churns, why they churn, and how much revenue is at risk as a result. The goal is to derive actionable insights that guide retention strategy, contract design, and customer support priorities.

---

## 📂 Dataset Summary

| Property | Details |
|---|---|
| Total Rows | 7,043 |
| Total Columns | 21 |
| Churned Customers | 1,869 (26.54%) |
| Retained Customers | 5,174 (73.46%) |
| Data Issues Found | Blank string values in `TotalCharges` |

**Key Features:**
- **Customer Demographics** — gender, SeniorCitizen, Partner, Dependents
- **Account Details** — tenure, Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges
- **Subscribed Services** — PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies
- **Target Variable** — Churn (Yes/No)

---

## 🔧 Tools & Technologies

| Tool | Purpose |
|---|---|
| Python (pandas, matplotlib, seaborn) | Data cleaning & exploratory data analysis |
| Jupyter Notebook | Analysis workflow & visual storytelling |
| Power BI | Interactive dashboard & visualization |

---

## 🧹 Data Preparation (Python)

- **Data Loading** — Imported dataset using `pandas`
- **Data Exploration** — Checked shape, data types, summary statistics, null values, and duplicate `customerID` entries
- **Missing/Invalid Data Handling** — Found blank (`' '`) string entries in `TotalCharges`; converted the column to numeric (`float`)
- **Feature Engineering** — Recoded `SeniorCitizen` from binary (0/1) to categorical (`yes`/`no`) for readability
- **Consistency Check** — Reviewed value counts across all columns to catch inconsistent or unexpected categories
- **Output** — Cleaned dataset exported for use in dashboarding and further analysis

---

## 🔍 Exploratory Data Analysis (Python)

Key questions explored in the notebook:

1. **Overall Churn Split** — 1,869 churned vs. 5,174 retained customers → **26.5% churn rate**
2. **Churn by Demographics** — gender, senior citizen status, partner, and dependents
   - Male churn: 930 | Female churn: 939 (roughly even split)
3. **Churn by Subscribed Services** — phone, internet, online security, backup, device protection, tech support, streaming TV/movies
4. **Churn by Tenure** — distribution of churned vs. retained customers across tenure (months); churn is concentrated in early-tenure customers
5. **Churn by Payment Method** — comparison across electronic check, mailed check, bank transfer (automatic), and credit card (automatic)

---

## 📊 Power BI Dashboard

An interactive **3-page Customer Churn Dashboard** was built featuring:

### Page 1 — Customer Churn Analysis (Overview)
- KPI cards: Total Customers (7,043), Churn Rate (26.54%), Avg Monthly Charge ($64.76), Avg Monthly Tenure ($32.37)
- Churn distribution (donut chart)
- Churn rate by Contract Type and Internet Service
- Tenure distribution histogram
- Churn by Payment Method

### Page 2 — Churn Drivers
- Churn breakdown by OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV
- Total customers by Partner, Dependents, and SeniorCitizen status
- Monthly Charges vs. Tenure scatter plot, colored by churn status

### Page 3 — Revenue Impact
- KPI card: **Total Revenue at Risk — $2.86M**
- Revenue at Risk by Contract type (Month-to-month leads at $1.93M)
- Revenue at Risk by Charge Band (Low / Medium / High / Premium)
- Table of Top Individual At-Risk Customers by total charges

Filter slicers available: `InternetService`, `Contract`, `SeniorCitizen`, `gender`

---

## 🧮 DAX Measures & Calculated Columns

All measures and calculated columns live in a single table, `Cleaned_data`, inside the Power BI data model.

### Measures
- `Total Customers`
- `Churn Customers`
- `Retain Customers`
- `Churn Rate`
- `Total Revenue`
- `Revenue at Risk`
- `Avg Monthly Charge`
- `Avg Monthly Tenure`

### Calculated Columns
- `ChargeBand` — bins `MonthlyCharges` into Low / Medium / High / Premium; used as the axis on the "Revenue at Risk by Charge Band" chart (Page 3)
- `Tenure Bucket` — bins `tenure` into ranges

### Where They Show Up
| Dashboard element | Measure(s)/Column(s) used |
|---|---|
| Total Customers KPI (Page 1) | `Total Customers` |
| Churn Rate KPI (Page 1) | `Churn Rate` |
| Avg Monthly Charge KPI (Page 1) | `Avg Monthly Charge` |
| Avg Monthly Tenure KPI (Page 1) | `Avg Monthly Tenure` |
| Churn Distribution donut, Churn Rate by Contract/Internet Service bars (Page 1) | `Total Customers` sliced by `Churn` |
| Churn Drivers charts (Page 2) | `Total Customers` sliced by each service/demographic column |
| Revenue at Risk KPI and bar charts (Page 3) | `Revenue at Risk` |
| Revenue at Risk by Charge Band chart (Page 3) | `Revenue at Risk`, `ChargeBand` |

> Note: `Churn Customers` and `Retain Customers` exist in the model but aren't shown as standalone visuals — they're most likely feeding into `Churn Rate` behind the scenes. `Tenure Bucket` exists in the model but the Page 1 tenure chart in the current dashboard uses the raw `tenure` column as a continuous histogram rather than the bucketed version.

---

## 💡 Business Recommendations

- **Target Month-to-Month Customers** — This segment drives the highest churn and the largest revenue at risk ($1.93M of $2.86M); incentivize migration to longer-term contracts
- **Promote Add-On Services** — Customers without OnlineSecurity or TechSupport churn at roughly 2–3x the rate of those with them; bundle these services into retention offers
- **Review Electronic Check as a Payment Option** — This payment method shows the highest churn; consider nudging customers toward automatic payment methods
- **Early Tenure Retention Program** — Churn is heavily concentrated among customers in their first few months; strengthen onboarding and early-lifecycle engagement
- **Prioritize High-Value At-Risk Customers** — Premium and high charge-band customers account for the largest share of revenue at risk ($1.77M and $0.79M respectively); focus retention outreach here first
- **Fiber Optic Experience Review** — Fiber optic customers churn more than DSL customers; investigate service quality or pricing as potential causes

---

## 📁 Project Structure

```
├── data/
│   ├── 1_Customer_Churn.csv          # Raw dataset
│   └── 2_Cleaned_data.csv            # Cleaned dataset
├── notebooks/
│   └── 3_Customer_churn_analysis.ipynb
├── dashboard/
│   └── 4_Customer_Churn_Dashboard.pbix
├── screenshots/
│   ├── 5_Overview.png
│   ├── 6_Churn_Drivers.png
│   └── 7_Revenue_Impact.png
└── README.md
```
