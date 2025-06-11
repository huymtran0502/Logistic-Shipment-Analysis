# Project: Logistic Shipment Analysis

## **Overview:**

* This project shows an analysis of logistics performance. The dashboard provides insights into key performance indicators (KPIs) such as delivery times, transportation costs, shipment volumes, and delay rates. The goal is to help stakeholders optimize logistics operations and reduce costs.

## **Objectives:**

* Visualize logistics performance metrics to identify bottlenecks.
* Analyze trends in delivery times and costs over time.
* Provide actionable recommendations for improving operational efficiency.

## **Dataset:**

The dataset consists of multiple CSV files, which are used together to create a relational model in Power BI. The files include:
![image_alt](https://github.com/huymtran0502/Logistic-Shipment-Analysis/blob/main/Model%20View.png?raw=true)

* Country.csv: Contains country-related data, such as country codes, names, and possibly regions.
* Product.csv: Includes product details, such as product IDs, names, categories, and prices.
* SalesPerson.csv: Contains salesperson information, such as IDs and names.
* Shipment.csv: Includes shipment details, such as shipment IDs, dates, costs, and foreign keys linking to other tables.


## **Dashboard:**
![image_alt](https://github.com/huymtran0502/Logistic-Shipment-Analysis/blob/main/Dashboard.png?raw=true)

* KPI Overview: Displays key metrics including total revenue ($2M), shipment categories (5K Active at 33%, 2K Completed at 62%, 3K Return at 5%), and average delivery time (10 days).
* Trend Analysis: Visualizes monthly shipment volumes (Active, Completed, Return) via a stacked bar chart and revenue trends via a line chart, showing fluctuations from $110K to $157K over the year.
* Geographic Insights: Features a bar chart of average delivery time by country (Australia: 20 days, USA: 1 day) with performance categories (Too Long, Fine, Perfect) and a pie chart breaking down revenue by product category (68% Electronics, 51% Computing).
* Interactive Filters: Includes a date range filter (01/01/2022 to 31/12/2024), a product category filter (Audio, Computing, Electronics, Office Equipment), and a country list for dynamic data exploration.

## **DAX Calculations:**
The following DAX measures were used to power the dashboard's analytics:

* Active Shipment % = DIVIDE([Active Shipments], [Shipment])
* Active Shipments = CALCULATE([Shipment], Shipment[Status] = "Active")
* Avg Delivery Time = DIVIDE([Delivery Time], [Completed Shipments])
* Avg Delivery Time Color = SWITCH(TRUE(), [Avg Delivery Time] <= 4, "#BCEEB7", [Avg Delivery Time] <= 10, "#BDE1F6", [Avg Delivery Time] > 10, "#F9D2D4")
* Completed Shipment % = DIVIDE([Completed Shipments], [Shipment])
* Completed Shipments = CALCULATE([Shipment], Shipment[Status] = "Completed")
* Delivery Time = SUM(Shipment[Delivery Time])
* Return Shipments = CALCULATE([Shipment], Shipment[Status] = "Returned")
* Returned Shipment % = DIVIDE([Return Shipments], [Shipment])
* Revenue = CALCULATE(SUM(Shipment[Sales]), Shipment[Status] = "Completed")
* Target % = [Revenue] / 1000000
* Target Difference = 1 - [Target %]
* Shipments Slicer = {("Month", NAMEOF('Calendar'[Month]), 0), ("Year", NAMEOF('Calendar'[Year]), 1)}

## **Key Insights:**

* Identified that 33% of shipments (5,000 out of 10,000) are active, while 20% (2,000) are completed and 5% (3,000) are returned, indicating a high volume of active shipments.
* Achieved an average delivery time of 10 days, with significant variations by country: Australia (20 days) and Japan (18 days) suggest potential delays, while USA (1 day) and Canada (2 days) perform exceptionally well.
* Generated $2M in revenue from completed shipments, with Electronics contributing 68% and Computing 51% of the total, highlighting key product categories driving sales.
