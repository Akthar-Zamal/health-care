# Healthcare Data Analytics Dashboard - Power BI

> Senior Data Analyst Case Study | End-to-End Project

### Live Dashboard Preview
![Overview] (Page 1)
![Analysis] (Page 2)

---

### 1. Problem Statement
A multi-specialty hospital wants to understand patient admissions, operations, billing, payment collection and patient experience. The raw data had duplicates, missing values, inconsistent casing, wrong date formats, and numbers stored as text.

**Business Questions Answered:**
- Monthly admission trends?
- Highest patient volume department?
- Avg Length of Stay & Waiting Time?
- Diagnosis contribution to billing?
- Total Billed / Collected / Outstanding & Collection Rate?
- Insurance performance (Best/Worst)?
- Factors for low satisfaction?
- % Data Quality & Duplicate handling?

---

### 2. Dataset
- **Records:** 2000+ Admissions
- **File:** `healthcare_dataset.xlsx`
- **Columns:** Patient_ID, Age, Gender, Department, Diagnosis, Doctor, Insurance, Ward, Bill_Amount, Amount_Paid, Admission_Date, Stay_Days, Waiting_Time, Satisfaction_Score, Payment_Mode, Status

---

### 3. Data Cleaning (Power Query)
- Removed duplicates
- Trimmed & Cleaned text, Fixed inconsistent casing (UPPER/Proper)
- Fixed date formats (Admission_Date, DOB)
- Converted Bill_Amount from Text to Number
- **Null Handling:** Replaced nulls in Admission Status, Payment Mode, Insurance Provider, DOB with "Unknown" (Mean/Median not suitable for categorical)
- Created new columns: Age_Group, Month, Year

**Data Quality Issues Found:**
- Unknown Payment Mode: 116
- Unknown Status: 325
- Unknown Insurance: 454 (Critical)
- % Complete Records: 60%
- Data Quality Score: 0.53

---

### 4. Data Modeling - Star Schema
**Fact Table:** `Fact_Admission` - All measures + keys
**Dimension Tables (7):**
- `Dim_Patient` - Age, Age_Group, Gender
- `Dim_Department` - Department_ID, Name
- `Dim_Diagnosis` - Diagnosis_ID, Name
- `Dim_Doctor` - Doctor_ID, Name
- `Dim_Insurance` - Insurance_ID, Provider
- `Dim_Ward` - Ward_ID, Name
- `Dim_Payment` - Payment_ID, Mode

**Relationship:** 1-to-Many from Dimensions to Fact

---

### 5. DAX Measures (17 Created)

```dax
Total Admissions = COUNTROWS(Fact_Admission) // 2K
Total Billed = SUM(Fact_Admission[Bill_Amount_INR]) // 243.85M
Total Collected = SUM(Fact_Admission[Amount_Paid]) // 196.78M
Total Outstanding = [Total Billed] - [Total Collected] // 47.07M
Collection Rate = DIVIDE([Total Collected], [Total Billed]) // 80.7%
Avg Length of Stay = AVERAGE(Fact_Admission[Stay_Days]) // 9.5 Days
Avg Waiting Time = AVERAGE(Fact_Admission[wait_Time_Minutes]) // 121.85 mins
Avg Satisfaction = AVERAGE(Fact_Admission[Satisfaction_Scores]) // 3.55
Avg Bill Per Admission = DIVIDE([Total Billed], [Total Admissions])
Best Insurance = TOPN(1, Insurance, [Collection Rate], DESC) // ICICI Lombard
Worst Insurance = TOPN(1, Insurance, [Collection Rate], ASC) // Medicare
