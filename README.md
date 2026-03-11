# 📊 Retrospective Sales Analysis During COVID (2019–2023)

This project performs a retrospective analysis of sales data before and during the COVID period (2019–2023).
The objective is to identify trends and answer key business questions so that stakeholders can better understand the impact of large-scale disruptions and be better prepared for similar events in the future.

The dataset is based on real business data.
The store name has been changed and some values were pre-selected and slightly manipulated to maintain anonymity and security of the business.However, the structure and patterns remain representative of real-world small business scenarios.

## 📁 Dataset Overview

The dataset comes from a US-based game store named "GameTown" (hypothetical name).
All monetary values are expressed in USD.

The dataset is provided as an Excel file (.xlsx) and contains two sheets.

Sheet 1 `orders` (raw dataset):

| Column Name             | Description                                          |
| ----------------------- | ---------------------------------------------------- |
| USER_ID                 | User identifier                                      |
| ORDER_ID                | Order identifier                                     |
| PURCHASE_TS             | Purchase timestamp                                   |
| SHIP_TS                 | Shipping timestamp                                   |
| REFUND_TS               | Refund timestamp                                     |
| PRODUCT_NAME            | Name of the product                                  |
| PRODUCT_ID              | Product identifier                                   |
| USD_PRICE               | Price in US Dollars                                  |
| PURCHASE_PLATFORM       | Platform where purchase was made                     |
| MARKETING_CHANNEL       | Marketing channel that the purchase was done through |
| ACCOUNT_CREATION_METHOD | Account creation method                              |
| COUNTRY_CODE            | Country code                                         |

The dataset contains **44,015** rows.

Sheet 2 `regions`:

This sheet maps country codes to their corresponding regions and is used for geographical analysis.

## 🧹 First Glance & Data Cleaning

Before starting any analysis, an initial review and cleaning of the dataset is required.
For this project, Excel is used for the first data preparation steps.

As a safety measure, a copy of the raw dataset is created before any transformation is applied.

### 📝 Issue Log

All detected issues are documented in a dedicated worksheet named `issue_log`.
This sheet tracks data quality problems and the actions taken to resolve them.

| Column Name       | Description                                                             |
| ----------------- | ----------------------------------------------------------------------- |
| table             | The table/sheet the problem was located at                              |
| column            | The column of the table the problem was located at                      |
| issue             | The issue/problem found                                                 |
| row count         | The number of rows affected by this issue                               |
| problem magnitude | The magnitude/proportion of the problem in relation to the entire table |
| solvable?         | Is the problem solvable currently?                                      |
| solution          | Appropirate measure taken to the issue/problem                          |

The purpose of the `issue_log` is to :

- Maintain transparency
- Document cleaning decisions
- Simplify communication with stakeholders or team members

### 🧼 Data Cleaning Strategy

![alt text](img/issue_log.png)

Several issues were identified during the initial scan. Some could be corrected immediately, while others required further investigation.

Although techniques such as data imputation exist, they are used cautiously in data analysis.
Unlike predictive modeling, EDA focuses on understanding what the data currently represents. Imputation can introduce bias if not properly justified.

Imputation is only considered when:

- Values can be reliably cross-checked with another dataset
- There is a strong business justification

To preserve data integrity:

- A duplicate sheet is created before cleaning
- New columns are created instead of overwriting originals

After the data cleaning process,

- Solutions are recorded in the issue_log
- The proportion of affected rows is calculated to quantify impact

## 🔍 Initial Analysis

After cleaning, exploratory analysis begins.

To avoid unfocused exploration, an `insights_log` worksheet is created to document:

- Questions
- Assumptions
- Observations
- Next steps

As this is a project without external stakeholders to ask us the questions and give decisions, we will have to put ourselves in the stakeholder's position and ask business related questions.

### Primary Business Question

> How did total revenue across all products evolve between 2019 and 2023 (COVID period)?  
> Conduct an initial analysis to help product, marketing, and finance teams understand high-level trends.

This question guides the entire exploratory analysis.

![alt text](img/initial_analysis.png)

As in above image, relevant questions and initial steps are noted down for the analysis.

### 📈 Pivot Table Analysis

To answer the main question, pivot tables are used.

A pivot table `(TCD – Tableau Croisé Dynamique)` is created from the cleaned dataset.

- Metric (Value): Sum of USD_PRICE
- Time granularity: Monthly (good balance between detail and readability)

For the columns, product names are added to observe how each product performs over time.

In a real-world dataset, there could be hundreds of products, which would make the pivot table difficult to interpret. In such cases, analysts typically pre-select a subset of products, such as:

- Top 10 best-performing products
- Newly launched products
- Strategic products with high margins

This approach narrows the scope of the analysis and makes trends easier to interpret.

For this project, the dataset includes 8 products:

- 27in 4K gaming monitor
- Acer Nitro V Gaming Laptop
- Dell Gaming Mouse
- JBL Quantum 100 Gaming Headset
- Lenovo IdeaPad Gaming 3
- Nintendo Switch
- Razer Pro Gaming Headset
- Sony PlayStation 5 Bundle

![TCD](img/TCD.png)
_Snippet of the pivot table_

Conditional color formatting is applied to the pivot table to make patterns and performance differences easier to identify across products and months.

### 📝 Documenting Initial Insights

As done earlier with the issue_log, a structured table is created to document insights and analytical observations.

![alt text](img/init_table.png)
_Initial findings table_

This table is created in the `insights_log` worksheet and records:

- Observed patterns
- Potential explanations
- Follow-up questions
- Relevant teams that may need to investigate further

For example one of the findings is :

> `Large sales spike in 2022 Dec. Check promotional campagins around that time. The most contributing product is the PS5.`

Based on this observation, multiple teams may be involved:

- Finance Team
  - Evaluate margins and overall ROI from the spike in revenue.

- Marketing Team
  - Investigate promotional campaigns or seasonal marketing efforts that may have driven the increase in sales.

- Product / Operations Team
  - Prepare inventory and warehousing strategies for upcoming high-demand periods.

Documenting insights in this way helps transform raw analysis into actionable business intelligence, enabling cross-team collaboration and data-driven decision-making.

## 📈 Tableau Analysis

After completing the initial analysis in Excel, the next step is to perform a deeper exploration of the data using a Business Intelligence (BI) tool.

Common BI tools used in data analytics include Power BI, Looker, and Tableau.
For this project, Tableau is used to perform deeper analysis and to build the final interactive dashboard. The Tableau workbook is included in this repository.

Multiple worksheets are created in Tableau to explore different aspects of the data, such as:

- Revenue trends over time
- Product performance
- Regional sales distribution

Platform and marketing channel impact

To keep track of the insights discovered during this process, a new table named `Deep Dive Analysis` is created in Excel.

Since this project generates a large number of observations and insights, not every detail is documented in this README.

![alt text](img/deepDive.png)
_Snippet of the Deep Dive Analysis table_

As shown in the table snippet above, three columns are used to structure the analysis:

- Tableau worksheet/tab – The worksheet where the insight originates

- Findings / Insights – Key observations discovered during analysis

- Recommendations – Suggested actions for relevant teams based on the findings

This structure helps ensure that insights discovered in Tableau are clearly documented and can be communicated effectively to stakeholders.

### 📌 Business Recommendations

After documenting the insights from the deep dive analysis, the final step is to translate these insights into clear and actionable recommendations.

To facilitate communication between teams, a separate table named `Recommendations` is created.

![alt text](img/recommendations.png)
_Recommendations table_

In this table:

- The left column identifies the relevant team (e.g., Marketing, Finance, Sales, Development).
- The right column outlines clear actions or recommendations based on the insights obtained during the analysis.

This step is important because the goal of data analysis is not only to generate insights, but also to support decision-making and guide business actions.

## 📈 Tableau Dashboard

After completing the analysis, the final step is to present the insights in a clear and structured dashboard.

An important aspect of dashboard design is understanding the target audience.
Depending on the audience and their level of technical expertise, the dashboard must be structured differently.
For example:

- Executives usually need high-level KPIs and trends.
- Operational teams may require more detailed breakdowns and drill-down views.

For this reason, effective dashboards focus less on flashy colors or complex graphics and more on clarity, readability, and meaningful metrics.

The goal is to ensure that every chart, metric, and dimension serves a clear analytical purpose.

![alt text](img/dash1.png)
![alt text](img/dash2.png)

You can interact with the dashboard and explore the visualizations here 👉 [Interactive Tableau Dashboard](https://public.tableau.com/views/GameTown_Dashboard/SalesDashboard?:language=en-GB&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link).

### Dashboard Structure

The dashboard, titled `Sales Performance Dashboard (2019-2023)`, is structured to guide the user from high-level overview to detailed insights.

Top Section (Executive KPIs)

- Total Sales
- Average Order Value (AOV)
- Total Orders

These metrics provide quick insights for executives and decision-makers.

Middle Section (Sales Metrics)

- Product sales across time
- Product performance comparisons

This section helps identify seasonal patterns and the impact of the COVID period.

Bottom Section (Regional Sales)

- A stacked graph of regional sales to identify peak regions across time

The layout follows a top-to-bottom and left-to-right reading flow, moving from summary metrics toward more detailed analysis.

## 📊 Final Deliverables

This project includes:

- Cleaned dataset
- Issue log documenting data quality problems
- Initial exploratory analysis in Excel
- Deep dive analysis using Tableau
- Business recommendations derived from insights
- Interactive Tableau dashboard

## 🎯 Key Skills Demonstrated

- Exploratory Data Analysis (EDA)
- Data Cleaning & Data Quality Documentation
- Pivot Table Analysis
- Business Intelligence (Tableau)
- Translating data insights into business recommendations
- Stakeholder-oriented analytical thinking
