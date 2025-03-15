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
- Used **Alteryx** to profile data and note issues.  
- Converted **date formats** to `MM/dd/YYYY`.  
- Standardized **time format** to **24-hour (HH:MM:SS)**.  
- **Removed unnecessary spaces, tabs, and unwanted characters**.  
- **Assigned correct data types** (`Auto Field` in Alteryx).  
- Created a **unique identifier** (`RecordID`).  
- Loaded **processed data** into the **SQL database**.  

---

## Dataset Overview

**Dataset:** `311_CallCenterServiceRequests_KansasCity_2007-March2021.tsv`

### ** Data Attributes and Observations**
| Column Name        | Data Type  | Unique Values | Null Count |
|-------------------|------------|--------------|------------|
| CASE ID          | V_String    | >10,000      | 0          |
| SOURCE          | V_String    | 21           | 67         |
| DEPARTMENT      | V_String    | 27           | 0          |
| WORK GROUP      | V_String    | 146          | 0          |
| TYPE            | V_String    | 295          | 0          |
| DETAIL          | V_String    | 574          | 0          |
| CREATION DATE   | V_String    | 5229         | 0          |
| STATUS         | V_String    | 6            | 0          |
| CLOSED DATE    | V_String    | 4995         | 12702      |
| DAYS TO CLOSE  | V_String    | 2748         | 26515      |
| ZIP CODE       | V_String    | 65           | 826        |
| CATEGORY1      | V_String    | 82           | 0          |

## Visualizations & Dashboards

The following Power BI dashboards provide insights into **Kansas City Call Center Service Requests**. The visualizations analyze trends, workload distribution, response times, and efficiency.

---

### **Service Requests Overview**
![Service Requests Overview](images/service_requests_overview.png)

#### **Key Insights:**
- **Service Request Trend:** Shows the number of requests over the years.
- **Yearly Service Request Trend (Department Wise):** Tracks department-specific trends.
- **Service Request by Source:** Highlights major request channels (Phone, Web, Email, etc.).
- **Service Request by Departments:** Displays the distribution of requests across different departments.

---

### **Geographical & Workload Distribution**
![Geographical & Workload](images/geographical_workload.png)

#### **Key Insights:**
- **Service Request by Area (Top 10):** Identifies the locations with the highest request volume.
- **Service Request (Department and Work Group Wise):** Compares workload among various departments and work groups.
- **Average Response Time by Department:** Displays response time differences across departments.
- **Service Request by Year and Status:** Shows trends of open, closed, and resolved requests over time.

---

### **Response Time & Efficiency Analysis**
![Response Time & Efficiency](images/response_time_efficiency.png)

#### **Key Insights:**
- **Average Response Time by Category (Top 10):** Identifies categories with the longest response times.
- **Top 10 Performance Metrics:** Highlights cases with the fastest response times.
- **Workload Efficiency:** Examines the relationship between workload volume and efficiency in closing requests.

---

## Publishing Dashboards
- **📌 Power BI:** Published to **Power BI Workspace** for interactive reporting.
- **📌 Tableau:** Uploaded to **Tableau Cloud** for accessibility and analysis.

---

 **These dashboards provide data-driven insights to optimize resource allocation and improve service efficiency in Kansas City’s Call Center Operations.** 🚀


## Business Questions & SQL Queries

### Service Requests Over Time
**What is the trend in service requests from 2018-2021?**

```sql
SELECT YEAR(Creation_Date) AS Year, COUNT(*) AS Service_Request_Count
FROM Kansas_City
WHERE YEAR(Creation_Date) BETWEEN 2018 AND 2021
GROUP BY YEAR(Creation_Date)
ORDER BY Year;
```

### Volume of Service Requests by Source
**Which sources generate the most service requests?**

```sql
SELECT SOURCE, COUNT(*) AS Service_Request_Count
FROM Kansas_City
GROUP BY SOURCE
ORDER BY Service_Request_Count DESC;
```

### Volume of Service Requests by Department
**How are service requests distributed among departments?**

```sql
SELECT DEPARTMENT, COUNT(*) AS Service_Request_Count
FROM Kansas_City
GROUP BY DEPARTMENT
ORDER BY Service_Request_Count DESC;
```

### Geographical Analysis (Top 10 Areas)
**Which ZIP codes had the highest number of service requests?**

```sql
SELECT TOP 10 ZIP_CODE, COUNT(*) AS RequestCount
FROM Kansas_City
GROUP BY ZIP_CODE
ORDER BY RequestCount DESC;
```

### Departmental Workload Comparison
**How does workload vary among departments and work groups?**

```sql
SELECT DEPARTMENT, WORK_GROUP, COUNT(*) AS Service_Request_Count
FROM Kansas_City
GROUP BY DEPARTMENT, WORK_GROUP;
```

### Response Time Analysis
**How does response time vary across departments?**

```sql
SELECT DEPARTMENT, AVG(DAYS_TO_CLOSE) AS AvgDaysToClose
FROM Kansas_City
GROUP BY DEPARTMENT
ORDER BY AvgDaysToClose DESC;
```

### Service Request Status Composition
**How has the status of service requests changed from 2018-2021?**

```sql
SELECT YEAR(Creation_Date) AS Year, STATUS, COUNT(*) AS RequestCount
FROM Kansas_City
WHERE YEAR(Creation_Date) BETWEEN 2018 AND 2021
GROUP BY YEAR(Creation_Date), STATUS;
```

### Time to Closure Analysis
**Which categories take the longest to close? (Top 10)**

```sql
SELECT TOP 10 CATEGORY1, AVG(DAYS_TO_CLOSE) AS AvgDaysToClose
FROM Kansas_City
GROUP BY CATEGORY1
ORDER BY AvgDaysToClose DESC;
```

###  Workload Efficiency
**How does workload (requests count) relate to closure efficiency?**

```sql
SELECT DEPARTMENT, COUNT(*) AS Service_Request_Count, AVG(DAYS_TO_CLOSE) AS AvgDaysToClose
FROM Kansas_City
GROUP BY DEPARTMENT;
```
