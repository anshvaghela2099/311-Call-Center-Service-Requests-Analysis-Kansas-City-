# 311 Call Center Service Requests Analysis (Kansas City)

## Project Overview
This project involves **analyzing 311 Call Center Service Requests** in **Kansas City** from **2007 to 2021**. The analysis includes:
- **Data profiling and documentation** of inconsistencies.
- **Data staging** using SQL Server / Azure SQL / MySQL.
- **Building dashboards** in **Power BI & Tableau**.
- **Providing insights** on workload distribution, response time, and efficiency.

---

## Scope of Work
### Data Preparation & Staging
- **Profile** data using **Alteryx** to identify inconsistencies.
- **Load cleaned data** into SQL Server / Azure SQL / MySQL for further analysis.

### Data Visualization
- **Connect Power BI & Tableau** to staged data.
- **Create interactive dashboards** answering key business questions.

### Insights & Documentation
- **Interpret findings** from data profiling and visualizations.
- **Summarize observations** into a report.

---

## Data Connection & Preparation
- **Dataset:** `311_CallCenterServiceRequests_KansasCity_2007-March2021.tsv`
- **Database Options:** Azure SQL / Microsoft SQL Server / MySQL
- **Data Issues Identified:**
  - **Missing Values**: `SOURCE (67)`, `EXCEEDED EST TIMEFRAME (23)`, `ZIP CODE (826)`, `NEIGHBORHOOD (46,106)`, `CATEGORY2 (1,001,657)`, etc.
  - **Date Format Issues**: `CREATION DATE` & `CLOSED DATE` have different formats.
  - **Time Format Issues**: `CREATION TIME` format was inconsistent.
  - **Null Values**: Found in multiple categorical attributes.
  - **Data Type Inconsistencies**: All fields were initially `V_String`.
  - **Duplicate Entries**: Some service requests had duplicate records.

### **Data Processing Steps**
✔ Used **Alteryx** to profile data and note issues.  
✔ Converted **date formats** to `MM/dd/YYYY`.  
✔ Standardized **time format** to **24-hour (HH:MM:SS)**.  
✔ **Removed unnecessary spaces, tabs, and unwanted characters**.  
✔ **Assigned correct data types** (`Auto Field` in Alteryx).  
✔ Created a **unique identifier** (`RecordID`).  
✔ Loaded **processed data** into the **SQL database**.  

---

## Business Questions & SQL Queries

### Service Requests Over Time
**What is the trend in service requests from 2018-2021?**

```sql
SELECT YEAR(Creation_Date) AS Year, COUNT(*) AS Service_Request_Count
FROM Kansas_City
WHERE YEAR(Creation_Date) BETWEEN 2018 AND 2021
GROUP BY YEAR(Creation_Date)
ORDER BY Year;

### Service Requests Over Time
**What is the trend in service requests from 2018-2021?**

```sql
SELECT YEAR(Creation_Date) AS Year, COUNT(*) AS Service_Request_Count
FROM Kansas_City
WHERE YEAR(Creation_Date) BETWEEN 2018 AND 2021
GROUP BY YEAR(Creation_Date)
ORDER BY Year;
