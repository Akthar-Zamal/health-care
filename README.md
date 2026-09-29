# Healthcare Analysis - Power BI Dashboard

### 📌 Project Title: Healthcare Operations, Patient Demographics & Data Quality Compliance Dashboard

> A 3-Page end-to-end Power BI dashboard analyzing 2000 patient records for hospital performance, patient distribution, and compliance audit.

**Tool:** Power BI Desktop | **Date:** 29th September 2026
**Pages:** Overview | Patient Demographics | Data Quality & Compliance

---

### 📊 Dashboard Pages Structure

#### Page 1: Overview - Executive Summary
**Goal:** Overall hospital performance at one glance (For Management)
- **KPIs:** Total Billed: 24.82 Cr, Total Collected: 20.04 Cr, Collection Rate: 81%, Outstanding: 4.78 Cr
- **Visuals:**
    - Donut Chart: Age Group Distribution (Adult 45% Highest)
    - Treemap: Total Billed by Department (Emergency 40.84M Highest)
    - Stacked Bar: Admissions by Month (July Peak 195)
    - Table: Insurance Provider vs Billed (No Insurance 459 cases - Highest Risk)
    - Bar: Female/Male by Admission Status

#### Page 2: Patient Demographics
**Goal:** Who are our patients? (Q7)
- **Visuals:**
    - Bar Chart: Total Admissions by Department (General Medicine 330, Cardiology 325)
    - Column Chart: Average Waiting Time by Department (Pediatrics 129 mins Highest vs Avg 121.7 mins)
    - Line Chart: Seasonal Trend of Admissions by Month
    - Funnel Chart: Admission Status Flow (Discharged, Transferred, Admitted)
    - Gauge Chart: Avg Satisfaction Score (3.55 / 5)

#### Page 3: Data Quality & Compliance
**Goal:** Audit data quality and privacy compliance (Q8, Q9, Q10)
- **KPIs:** Unknown Stay Count: 291, Unknown Age Count: 131, Data Quality %: 0.79 (79%), Top Diagnosis Billing: 22.54M (Asthma)
- **Visuals:**
    - Bar: Total Admissions by Admission_Status (Discharged 100% bar)
    - Donut: Total Admissions by Gender (Male 49.8% - 1K, Female 50.2% - 1K) - Balanced
    - Treemap: Total Billed by Department (10 Departments)
    - Table: Diagnosis-wise Admissions & Billing (Asthma 179 Cases - 2.25 Cr, Arthritis 139 Cases Lowest)
    - Slicers: Payment_Mode (Card, Cash, UPI, Insurance) & Ward (Emergency, ICU, General Ward, Private)

---

### 🎯 Key Business Questions Answered (Q1-Q10)

- **Q1. Highest Admissions:** General Medicine (330)
- **Q2. Avg Wait Time:** 121.7 mins, Pediatrics worst (129 mins)
- **Q3. Monthly Trend:** July (195) peak due to monsoon season
- **Q4. Diagnosis Impact:** Asthma highest admissions (179) & billing (2.25 Cr)
- **Q5. Admission Type vs Stay:** Emergency stay 30% longer than Elective
- **Q6. Insurance Risk:** No Insurance = 459 admissions, 81% collection - Highest Outstanding
- **Q7. Demographics:** Balanced Gender, Adult age group max
- **Q8. Data Quality:** 79% compliant, 131 Age missing, 291 Stay missing
- **Q9. Compliance:** Privacy Compliant (No PII shown, only Patient_ID), Data Quality Non-Compliant (21% missing)
- **Q10. Recommendations:** Staffing for Pediatrics, Pre-monsoon prep, Insurance verification, Mandatory data entry validation

### 🛠️ DAX Measures Used
