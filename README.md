# Airtel Call Centre Performance Report

## 📊 Project Overview

This project uses **Python and Pandas** to clean, transform, and analyse Airtel call-centre data and produce a half-hourly performance report.

The objective is to convert raw call-centre and agent-efficiency reports from Excel into a structured report that can be used to monitor call volume, service performance, staffing requirements, and agent utilisation.

---

## 🎯 Objectives

The project focuses on:

* Cleaning raw Excel call-centre data
* Removing unnecessary header and footer rows
* Converting time-based columns into usable numerical values
* Aggregating call data into **30-minute intervals**
* Calculating key call-centre performance metrics
* Calculating required staffing levels
* Calculating actual FTE staffing
* Comparing required staffing with available staffing
* Producing a clean final report suitable for Excel

---

## 🛠️ Technologies Used

* **Python**
* **Pandas**
* **Jupyter Notebook**
* **NumPy**
* **Excel**

---

## 📁 Data Sources

The project works with raw Excel reports containing call-centre performance and agent-efficiency information.

### RAW Data

The queue contains information such as:

* Interval
* Queue / Skill Name
* Calls Offered
* Calls Answered
* Calls Abandoned
* Calls Answered Within Threshold
* Calls Answered After Threshold
* Calls Abandoned Within Threshold
* Talk Time
* Hold Time
* ACW Time
* Calls Handled
* Wait Time
* Maximum Wait Time

### Agent Efficiency Report Raw Data

The agent-efficiency Raw Data contains information such as:

* Agent Name
* Agent ID
* Interval
* Connection Time
* Calls Presented
* Calls Accepted
* Talk Time
* Waiting Time
* Idle Time
* Not Ready Time
* Hold Time
* AHT
* Active + Hold
* Login

---

## 🧹 Data Cleaning

The raw Excel reports contain formatting rows and header information that are not part of the actual dataset.

The Python workflow removes unnecessary rows and resets the DataFrame index before performing calculations.

Time columns are also converted into appropriate Pandas time/duration formats so that they can be used in calculations.

The cleaning process is designed to be reusable because the position of the final rows in the raw reports can change between files.

---

## ⏱️ Half-Hourly Reporting

The raw data is aggregated into **30-minute intervals**, producing a report from:

`12:00 AM` → `11:30 PM`

For each interval, call activity is aggregated across the available queues/skills.

---

## 📈 Key Metrics

The final report contains metrics including:

| Metric          | Description                                        |
| --------------- | -------------------------------------------------- |
| Calls Offered   | Total calls offered during the interval            |
| Calls Answered  | Total calls answered                               |
| Calls Abandoned | Calls not answered                                 |
| AHT             | Average Handle Time                                |
| FD %            | Forecast deviation percentage                      |
| AL %            | Abandonment level                                  |
| SL %            | Service level                                      |
| A2F %           | Answered-to-forecast percentage                    |
| Login Required  | Estimated number of agents required                |
| Login Count     | Calculated agent login requirement/count           |
| FTE             | Full-Time Equivalent staffing                      |
| Deficit/Excess  | Difference between required and available staffing |
|Not_Ready        |The total average Not Ready in minutes              |
---

## 👥 Staffing Calculation

The project calculates staffing requirements using call volume, handling time, and the required operational assumptions.

### Login Required

The calculation follows the equivalent Excel logic:

```python
Login Required = Calls Offered / ((30 × 85%) / (115 / 60))
```

The result is rounded to a whole number.

### FTE

FTE is calculated from the agent-efficiency data using the `Active+Hold` metric and converting the interval value to the appropriate staffing equivalent.

---

## 🔄 Project Workflow

```text
Raw Excel Reports
       ↓
Load Data with Pandas
       ↓
Clean Headers & Unnecessary Rows
       ↓
Clean Time / Numeric Columns
       ↓
Create Active + Hold
       ↓
Aggregate Call Data
       ↓
Create 30-Minute Intervals
       ↓
Calculate AHT & Performance Metrics
       ↓
Calculate Login Required
       ↓
Calculate FTE
       ↓
Calculate Deficit / Excess
       ↓
Create Final Report
       ↓
Export to Excel
```

---

## 📋 Final Report Structure

The final report is designed to contain the following fields:

```text
Interval
Forecast
Calls Offered
Calls Answered
Calls Answered within Threshold
Calls Answered After Threshold
Calls Abandoned Within Threshold
Calls Abandoned
AHT (Seconds)
FD %
AL%
SL%
A2F%
Login Required
Login Count
FTE
Deficit/Excess
Not Ready
Idle Time
Utilization
```

The final report intentionally excludes intermediate calculation columns such as Talk Time, Hold Time, ACW Time, and Calls Handled from the main report.

---

## 💻 Example

A typical half-hour record may look like:

```text
Interval       Calls Offered    Calls Answered    Abandoned    AHT
12:00 AM       19               ...               ...          ...
12:30 AM       ...              ...               ...          ...
01:00 AM       ...              ...               ...          ...
```

---

## 📤 Output

The processed DataFrame can be exported to Excel for further reporting and presentation.

Example:

```python
report_df.to_excel("Airtel_Report.xlsx", index=False)
```

The resulting Excel file can then be used for operational monitoring and workforce analysis.

---

## 🚀 Future Improvements

Potential improvements include:

* Automating the processing of multiple daily reports
* Creating automated Excel formatting
* Adding charts and dashboards
* Automating report generation
* Adding validation checks for missing or incorrect data
* Comparing actual performance against forecast
* Automating daily/weekly/monthly summaries

---

## 👤 Project Author

**Moses Olorunshola**


