# 💳 Loan Risk Analysis & Default Prediction

A complete end-to-end data pipeline to analyze customer loan default behavior and risk profiling using Azure Data Factory, Snowflake, and Power BI.

---

## 🔷 Project Overview

This project predicts loan defaults and categorizes customers into risk levels using historical banking data. It implements cloud-based data ingestion, transformation, and real-time reporting through BI dashboards.

---

## 🛠️ Tools & Technologies

| Purpose              | Technology Used             |
|----------------------|-----------------------------|
| Orchestration        | Azure Data Factory (ADF)    |
| Storage              | Azure Data Lake Storage Gen2|
| Data Warehouse       | Snowflake                   |
| Scripting & Analysis | SQL, Python (Snowflake Notebooks) |
| Reporting            | Power BI                    |

---

## 🧱 Architecture

The architecture showcases the flow from data ingestion to final visualization:

- Source: HTTP API / GitHub
- ADF: Extracts and lands data into ADLS
- Snowflake: Three-tier schema (RAW → REFINED → REPORTING)
- Power BI: Connects directly to REPORTING layer via DirectQuery

![Architecture](Architecture.png)

---

## 📌 Entity Relationship Diagram

Shows the schema relationships between `Customers`, `Loans`, `Payments`, and `Assets`.

![ER Diagram](ER%20Diagram.png)

---

## 🧪 Azure Data Factory Pipeline

The ADF pipeline is built with parameterized ingestion logic and includes failure notifications using webhook/Logic App integrations.

![ADF Pipeline](ADF.png)

---

## 📊 Power BI Dashboard

A fully interactive dashboard built on top of the reporting layer in Snowflake.

- KPIs: Default Rate, High-Risk Customers, Total Default Amount
- Heatmap: Defaults by Income & Age
- Loan Type-wise Default Rates
- Monthly Default Trends

![Dashboard](Bankdata.pbix)

---

## 🧠 Business Logic

### 🔸 Default Prediction:
- Rule: If missed_payments ≥ 3 → `Defaulter`

### 🔸 Risk Scoring (DTI Logic):
```sql
DTI = EMI / Monthly Income
If DTI:
  < 0.2 → Low
  0.2–0.35 → Moderate
  0.35–0.5 → Elevated
  > 0.5 → High
