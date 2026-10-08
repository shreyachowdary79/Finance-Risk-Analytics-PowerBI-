# Finance Risk Analytics | Power BI Dashboard

**End-to-End Data Analytics Project | Power Query | DAX | Power BI**

Transforming raw loan portfolio data into actionable financial risk insights through data cleaning, data modeling, KPI development, and interactive dashboard reporting.

## Project Overview

Finance Risk Analytics is an end-to-end business intelligence project designed to analyze loan portfolio performance, identify credit risk patterns, and monitor loan defaults and recoveries.

The project simulates a banking analytics workflow, combining quarterly loan datasets into a consolidated analytical model and presenting key findings through a three-page Power BI dashboard.

The objective is to help stakeholders understand portfolio exposure, identify high-risk segments, compare regional performance, and monitor changes in lending activity over time.

## Business Problem

Financial institutions need to monitor loan portfolios to identify potential defaults, assess credit risk, and understand lending performance.

Raw loan records often require significant preprocessing before they can support reliable reporting. Without a structured analytical workflow, it can be difficult to identify high-risk customer segments, track non-performing assets (NPA), and compare performance across regions and quarters.

**This project addresses these challenges by building a repeatable data preparation pipeline and an interactive financial risk dashboard.**

## Project Objectives

* Consolidate quarterly loan data into a unified analytical dataset.
* Clean missing, inconsistent, and improperly formatted values.
* Develop calculated columns for credit risk classification and loan analysis.
* Create reusable DAX measures for financial KPIs.
* Analyze loan defaults, NPA exposure, recovery performance, and portfolio distribution.
* Build interactive dashboards to support data-driven decision-making.

## Technology Stack

| Technology       | Purpose                                       |
| ---------------- | --------------------------------------------- |
| Power BI Desktop | Interactive dashboards and reporting          |
| Power Query (M)  | Data extraction, transformation, and cleaning |
| DAX              | KPI calculations and analytical measures      |
| CSV / Excel      | Source data and supporting analysis           |
| Data Modeling    | Organizing data for consistent reporting      |

## Data Analytics Workflow

```text
Quarterly Loan Data (Q1, Q2, Q3)
              |
              v
     Data Extraction
              |
              v
   Data Cleaning & ETL
       Power Query
              |
              v
  Feature Engineering
   Calculated Columns
              |
              v
   Data Model & DAX
      KPI Measures
              |
              v
    Power BI Dashboard
              |
              v
  Financial Risk Insights
```

## Phase 1: Data Cleaning and Transformation

Combined three quarterly CSV datasets into a consolidated loan dataset using Power Query.

Key operations included:

* Appending quarterly files into a master table.
* Handling missing values in loan amount, interest rate, and credit score fields.
* Standardizing interest rate formats and date values.
* Cleaning inconsistent text using `Text.Trim()`, `Text.Clean()`, and `Text.Proper()`.
* Preparing consistent data types for downstream analysis.

These transformations help improve data consistency and prepare the dataset for reliable reporting.

## Phase 2: Feature Engineering

Created additional analytical fields to support financial risk analysis and time-based reporting.

| Feature              | Analytical Purpose                                       |
| -------------------- | -------------------------------------------------------- |
| Quarter              | Compare quarterly loan performance                       |
| Month Name / Number  | Analyze monthly trends and sort months chronologically   |
| Year                 | Support year-based reporting                             |
| Loan Age (Days)      | Examine elapsed time since loan issuance                 |
| Risk Category        | Segment customers by credit score                        |
| Is Bad Loan          | Identify loans meeting the project's bad-loan definition |
| Loan Amount in Lakhs | Simplify portfolio value reporting                       |
| Risk Score           | Support ordered risk classification                      |
| EMI                  | Estimate monthly loan repayments                         |

The EMI calculation uses the standard amortizing-loan formula, with the zero-interest case handled separately where applicable.

## Phase 3: DAX Measures and Analytical Modeling

Developed DAX measures to calculate key portfolio and credit risk indicators dynamically.

### Key KPIs

* Total Loan Portfolio
* Total Number of Loans
* Bad Loan Count
* Bad Loan Rate
* Non-Performing Asset (NPA) Amount
* Defaulted Loan Amount
* Average Credit Score
* Recovery Rate
* High-Risk Loan Count
* Quarterly Portfolio Growth

### Example DAX Measures

**Bad Loan Rate**

```dax
Bad_Loan_Rate_% =
ROUND(
    DIVIDE(
        [Bad_Loan_Count],
        [Total_Loans],
        0
    ) * 100,
    2
)
```

**NPA Amount**

```dax
NPA_Amount =
COALESCE(
    CALCULATE(
        SUM(Row_Data[Loan_Amount]),
        Row_Data[Status] = "NPA"
    ),
    0
)
```

**Recovery Rate**

```dax
Recovery_Rate_% =
ROUND(
    DIVIDE(
        [Recovered_Loan_Count],
        [Eligible_Loan_Count],
        0
    ) * 100,
    2
)
```

*Note: The numerator and denominator for the recovery rate should match the business definition used in the dataset. Replace the example measure references with the actual measures in the Power BI model.*

## Phase 4: Interactive Power BI Dashboard

The report is organized into three pages, each designed to answer a different set of business questions.

### 1. Executive Summary

Provides a high-level view of the loan portfolio and overall performance.

**Visualizations and KPIs:**

* Total portfolio and loan count KPI cards
* Bad loan rate, average credit score, and recovery rate
* Loan type distribution
* Regional portfolio comparison
* Quarterly portfolio trends
* Bad loan rate gauge against a configurable target

**Business question:** What is the overall health of the loan portfolio?

### 2. Risk Analysis

Focuses on identifying risk concentrations and understanding loan quality.

**Visualizations and KPIs:**

* NPA amount and defaulted amount
* High-risk loan count
* Risk category distribution
* Loan status distribution
* Regional bad-loan comparison

**Business question:** Where is credit risk concentrated, and which segments require closer monitoring?

### 3. Loan Details

Provides a detailed view of individual loan records and customer-level risk indicators.

**Visualizations and KPIs:**

* Loan-level detail table
* Conditional formatting for risk indicators
* Top five high-risk customers
* Quarterly portfolio values
* Quarter-over-quarter growth indicators

**Business question:** Which loans and customer segments should be investigated further?

## Key Findings

The initial analysis reports the following findings, which should be validated against the source data and final dashboard:

* **Bad Loan Rate:** 37.5%, compared with the project's illustrative 20% monitoring target.
* **Regional Exposure:** The North region has the highest reported portfolio exposure at 2,790K.
* **Regional Credit Risk:** The East region has the highest reported bad-loan concentration.
* **Loan Type:** Personal loans show the highest reported default rate.
* **Quarterly Trends:** Q2 has the highest reported disbursement, followed by a slight decline in Q3.

These findings can help stakeholders investigate risk concentrations and determine where further analysis may be needed. The 20% target is a project assumption unless supported by an appropriate external benchmark.

## Repository Structure

```text
Finance-Risk-Analytics/
├── Data/
│   ├── Loan_Data_Q1.csv
│   ├── Loan_Data_Q2.csv
│   └── Loan_Data_Q3.csv
├── Output/
│   └── Current_Working_Project.xlsx
├── Finance_Risk_Analytics.pbix
└── README.md
```

## How to Run the Project

1. Clone or download the repository.
2. Install or open Power BI Desktop.
3. Open `Finance_Risk_Analytics.pbix`.
4. In Power Query, update the source folder path to match your local `Data` directory.
5. Refresh the data and verify that all queries and measures load correctly.
6. Navigate through the Executive Summary, Risk Analysis, and Loan Details pages.

**Requirements:** Power BI Desktop and access to the project's source data.

## Skills Demonstrated

* End-to-end data preparation and ETL
* Power Query M language and transformation logic
* Missing-value handling and data standardization
* Feature engineering for financial analytics
* DAX measures and KPI development
* Financial reporting and business intelligence
* Interactive dashboard design and data visualization
* Credit risk, loan default, and NPA analysis
* Quarterly trend and portfolio analysis
* Translating business questions into analytical outputs

## Future Enhancements

* Add automated data refresh and a reusable source-folder configuration.
* Introduce more robust validation rules for missing and inconsistent records.
* Add drill-through pages for detailed customer and loan investigations.
* Compare risk metrics across additional periods.
* Document data definitions and the assumptions used in each KPI.
* Add a reproducible data validation checklist.

## Project Purpose

This project demonstrates the application of data analytics and business intelligence techniques to a financial services use case. It showcases how raw data can be transformed into structured reporting and actionable insights using Power Query, DAX, and Power BI.

**Focus areas:** Data Analytics | Business Intelligence | Financial Risk Analytics | Power BI | DAX
