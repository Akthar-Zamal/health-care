# 🏥 Healthcare Data Analytics Dashboard - Power BI

> **Senior Data Analyst Case Study | End-to-End Project**
> Raw Hospital Data → Cleaning → Star Schema → DAX → 2-Page Management Dashboard

---

## 📌 Problem Statement
A multi-specialty hospital wants to understand **patient admissions, operations, billing, payment collection and patient experience**.

But the raw data had:
- Duplicates
- Missing values (Insurance, Payment Mode, Status)
- Inconsistent casing & extra spaces
- Wrong date formats
- Numbers stored as text

**Goal:** Clean, Validate, Transform and build a Management Dashboard.

---

## ❓ Business Questions
1. Monthly admission trends?
2. Which department has highest patient volume?
3. What is Avg Length of Stay & Waiting Time?
4. How much does each diagnosis contribute to billing?
5. What is Total Billed / Collected / Outstanding & Collection Rate?
6. Which insurance performs best/worst?
7. What factors cause low satisfaction?
8. What is % data quality & duplicate count?
9. Final Management Dashboard

---

## 📂 Dataset
- **Source:** `healthcare_dataset.xlsx`
- **Rows:** 2000+ Admission Records
- **Columns:** Patient_ID, Age, Gender, Department, Diagnosis, Doctor, Insurance, Ward, Bill_Amount_INR, Amount_Paid, Admission_Date, Discharge_Date, Stay_Days, Waiting_Time, Satisfaction_Scores, Payment_Mode, Status

---

## 🧹 Data Cleaning (Power Query)
- Removed Duplicates (based on Patient_ID + Admission_Date)
- Trim, Clean, Proper Case for Department, Diagnosis, Insurance
- Fixed Date Formats (DOB, Admission_Date)
- Changed Bill_Amount from Text to Number (INR)
- Created Columns: Age_Group, Year, Month, Quarter

**Null Handling Strategy:**
Replaced nulls in Admission Status, Payment Mode, DOB, Insurance Provider with **"Unknown"** because Mean/Median is not genuine for categorical data. This preserves audit trail.

**Data Quality Issues Found:**
- Unknown Payment Mode: **116**
- Unknown Status: **325**
- Unknown Insurance Provider: **454 (Critical)**
- % Complete Records: **60%**
- Data Quality Score: **0.53 / 1.0**

---

## 🏗️ Data Model - Star Schema

**Fact Table:** `Fact_Admission`
> Patient_ID, Bill_Amount_INR, Amount_Paid, Admission_Date, Stay_Days, Waiting_Time, Satisfaction_Scores, Month, Ward, Payment Mode

**Dimensions (7) - All 1-to-Many to Fact:**
- `Dim_Patient` - Age, Age_Group, Gender, Patient_ID, Name
- `Dim_Department` - Department_ID, Department_Name
- `Dim_Diagnosis` - Diagnosis_ID, Diagnosis_Name, Cost
- `Dim_Doctor` - Doctor_ID, Doctor_Name
- `Dim_Insurance` - Insurance_ID, Provider
- `Dim_Ward` - Ward_ID, Ward_Name
- `Dim_Payment` - Payment_ID, Payment_Mode

> Why Star Schema? Fast performance, Simple DAX, Easy filtering for Power BI

---

## 📊 DAX Measures - 17 Measures Created

```dax
Total Admissions = COUNTROWS(Fact_Admission) // 2K
Total Billed = SUM(Fact_Admission[Bill_Amount_INR]) // 243.85M
Total Collected = SUM(Fact_Admission[Amount_Paid]) // 196.78M
Total Outstanding = [Total Billed] - [Total Collected] // 47.07M
Collection Rate = DIVIDE([Total Collected], [Total Billed]) // 80.7%
Avg Waiting Time = AVERAGE(Fact_Admission[wait_Time_Minutes]) // 121.85
Avg Satisfaction = AVERAGE(Fact_Admission[Satisfaction_Scores]) // 3.55
Avg Length of Stay = AVERAGE(Fact_Admission[Stay_Days]) // 9.50
Avg Bill Per Admission = DIVIDE([Total Billed], [Total Admissions])

Best Insurance Provider =
  VAR Top1 = TOPN(1, ADDCOLUMNS(VALUES(Dim_Insurance[Provider]), "@Rate", [Collection Rate]), [@Rate], DESC)
  RETURN MAXX(Top1, Dim_Insurance[Provider]) // ICICI Lombard

Worst Insurance Provider =
  VAR Bottom1 = TOPN(1, ADDCOLUMNS(VALUES(Dim_Insurance[Provider]), "@Rate", [Collection Rate]), [@Rate], ASC)
  RETURN MAXX(Bottom1, Dim_Insurance[Provider]) // Medicare

Top Diagnosis by Billing =
  CALCULATE([Total Billed], TOPN(1, ALL(Dim_Diagnosis), [Total Billed], DESC)) // 21.89M
