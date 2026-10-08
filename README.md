# Healthcare Data Analytics Dashboard | Power BI

### 📌 Project Overview
Built an end-to-end Healthcare Analytics dashboard for a multi-specialty hospital to track admissions, operations, billing, and patient experience. Raw data had duplicates, missing values, inconsistent text, and wrong date formats.

This project covers full lifecycle: **Data Cleaning → Data Modeling → DAX → Dashboard → Insights.**

### 🎯 Business Questions Solved
- Monthly admission trends
- Highest patient volume department
- Avg Length of Stay & Waiting Time
- Diagnosis contribution to billing
- Total Billed / Collected / Outstanding & Collection Rate
- Insurance performance (Best / Worst)
- Factors for low satisfaction
- Data Quality % & Duplicate handling

### 🛠️ Tools Used
- **Power BI Desktop** - Dashboard & Modeling
- **Power Query** - Data Cleaning & Transformation
- **DAX** - 17 KPI Measures
- **Excel** - Source data
- **Star Schema** - Data Modeling (1 Fact + 7 Dims)

### 🧹 Data Cleaning Done
- Removed duplicates, Trim & Clean, Fixed casing
- Fixed date formats, Converted Bill Amount Text → Number
- Replaced Nulls in Status, Payment Mode, Insurance, DOB with **"Unknown"** (Mean/Median not valid for categorical)
- Created: Age_Group, Year, Month, Quarter

**Data Quality Issues Found:**
- Unknown Payment: 116 | Unknown Status: 325 | Unknown Insurance: 454
- % Complete Records: 60% | Data Quality Score: 0.53

### 🏗️ Data Model - Star Schema
**Fact:** Fact_Admission (Bill_Amount, Amount_Paid, Admission_Date, Stay_Days, Waiting_Time, Satisfaction)
**Dimensions (7):** Dim_Patient, Dim_Department, Dim_Diagnosis, Dim_Doctor, Dim_Insurance, Dim_Ward, Dim_Payment
**Relationship:** 1-to-Many

### 📊 KPIs Created (DAX)
- Total Admissions = 2K | Total Billed = 243.85M | Collected = 196.78M | Outstanding = 47.07M
- Collection Rate = 80.7% | Avg Stay = 9.50 Days | Avg Waiting = 121.85 mins | Avg Satisfaction = 3.55
- Best Insurance = ICICI Lombard | Worst = Medicare | Top Diagnosis Billing = 21.89M

### 📈 Dashboard - 2 Pages

**Page 1: OVERVIEW (For Management)**
- 8 KPI Cards
- Gender Donut: 977 Male (49%) vs 980 Female (50%)
- Dept Bar: General Medicine 315 (Top), Emergency 312, Cardiology 297
- Insurance Table: Unknown Insurance 5.56M Highest Risk
- Line Chart: Admissions by Month - Declining trend
- Billed by Year: ~80M stable

**Page 2: ANALYSIS (For Data Quality)**
- Age Group Donut: Adult 32.93% (650) Highest
- Funnel: Billed vs Collected vs Outstanding - 19.3% pending
- Treemap: Billed by Dept - Emergency 39.48M Highest
- Donut: Billed by Diagnosis - Cancer & Heart Disease top
- Filters: Year, Ward, Quarter

### 🔍 Key Insights

1. **Revenue Issue:** Only 80.7% collected, 47.07M outstanding (19.3% pending) - collection weak
2. **Insurance Risk:** ICICI Lombard best payer, Medicare worst - 454 unknown insurance = 5.56M leakage
3. **Data Quality:** Only 53% quality score - major data entry gaps
4. **Operational Load:** General Medicine & Emergency handle 31% admissions - over-utilized
5. **Patient Experience:** Avg waiting 121 mins very high → Satisfaction low 3.55/5
6. **Business Trend:** Monthly admissions declining, Yearly billing flat at 80M - no growth

### ✅ Recommendations

1. **Revenue:** Dedicated team for 47M outstanding, fix 454 unknown insurance, renegotiate Medicare, promote ICICI Lombard
2. **Operations:** Make Insurance/Payment mandatory fields, add staff to Emergency & General Medicine, reduce waiting to <60 mins
3. **Management:** Monthly data quality audit (target 0.90), marketing for declining admissions, focus on high-billing packages (Heart/Cancer)
4. **IT:** Implement RLS for doctors, auto-email for >30 days outstanding

### 📂 Files in Repo
- `Healthcare_Dashboard.pbix`
- `healthcare_dataset.xlsx`

---
**Author:** [Akthar Zamal Patan] | [https://www.linkedin.com/in/akthar-zamal-patan]
