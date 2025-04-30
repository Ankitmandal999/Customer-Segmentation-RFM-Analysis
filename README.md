# Customer-Segmentation-RFM-Analysis

# Overview
This project focuses on leveraging Power BI to create a comprehensive dashboard that provides detailed customer demographics and segmentation analysis. By utilizing key performance indicators (KPIs), expected outcomes, and advanced features such as drill-through capabilities, this project aims to empower decision-makers with actionable insights to drive strategic initiatives. Additionally, the project incorporates RFM (Recency, Frequency, Monetary) analysis to classify customers into segments based on their purchasing behaviors, further enhancing the depth of insights.

# Steps to perform RFM Analysis:

**Step 1: Prepare Your Data**
Ensure you have a dataset that includes transaction details such as:
* •	Customer ID
* •	Transaction Date
* •	Transaction Amount

**Step 2: Import Data into Power BI**
1.	Open Power BI Desktop.
2.	Click on Home > Get Data > Excel (or your data source).
3.	Select your file and load the data into Power BI.

**Step 3: Create Calculated Columns for RFM Metrics**
You need to create calculated columns for Recency, Frequency, and Monetary values.
**Recency:** Recency measures how recently a customer made a purchase. Create a calculated column to determine the number of days since the last purchase.
Recency = DATEDIFF(
    MAX('TableName'[DateColumn]),
    TODAY(),
    DAY )

**Frequency:** Frequency measures how often a customer makes a purchase. Create a calculated column to count the number of transactions per customer.
Frequency = 
CALCULATE(
    COUNT('TableName'[DateColumn]),
    ALLEXCEPT('TableName', 'TableName'[Key]) )

**Monetary:** Monetary measures how much money a customer spends. Create a calculated column to sum the transaction amounts per customer.
Monetary = 
CALCULATE(
    SUM('TableName'[Amount]),
ALLEXCEPT('TableName', 'TableName'[Key]) )

**Step 4: Create RFM Scores**
Create calculated columns to assign scores for Recency, Frequency, and Monetary values. You can use quintiles or any other method to rank the customers.
**Recency Score**
RecencyScore = 
SWITCH(
    True(),
    [Recency_Value] <= PERCENTILE.INC('RFM Table'[Recency_Value],0.20), "5",
    [Recency_Value] <= PERCENTILE.INC('RFM Table'[Recency_Value], 0.40), "4",
    [Recency_Value] <= PERCENTILE.INC('RFM Table'[Recency_Value], 0.60), "3",
    [Recency_Value] <= PERCENTILE.INC('RFM Table'[Recency_Value],0.80), "2", "1"  
)

**Frequency Score**
FrequencyScore = 
SWITCH(
    True(),
    [Frequency_Value] <= PERCENTILE.INC('RFM Table'[Frequency_Value],0.20), "1",
    [Frequency_Value] <= PERCENTILE.INC('RFM Table'[Frequency_Value], 0.40), "2",
    [Frequency_Value] <= PERCENTILE.INC('RFM Table'[Frequency_Value], 0.60), "3",
    [Frequency_Value] <= PERCENTILE.INC('RFM Table'[Frequency_Value],0.80), "4", "5"  
)

**Monetary Score**
MonetaryScore = 
SWITCH(
    True(),
    [Monetary_value] <= PERCENTILE.INC('RFM Table'[Monetary_value],0.20), "1",
    [Monetary_value] <= PERCENTILE.INC('RFM Table'[Monetary_value], 0.40), "2",
    [Monetary_value] <= PERCENTILE.INC('RFM Table'[Monetary_value], 0.60), "3",
    [Monetary_value] <= PERCENTILE.INC('RFM Table'[Monetary_value],0.80), "4", "5"  
)

**Step 5: Combine RFM Scores**
Create a calculated column to combine the RFM scores into a single score.
RFM SCORE = 'RFM Table'[RecencyScore] & 'RFM Table'[FrequencyScore] & 'RFM Table'[MonetaryScore]

**Step 6: Create RFM Segments**
Create calculated columns to segment customers based on their RFM scores.
RFMCategory = 
SWITCH(
    TRUE(),
    [RFMScore] >= 555, "Champions",
    [RFMScore] >= 444, "Loyal Customers",
    [RFMScore] >= 333, "Potential Loyalists",
    [RFMScore] >= 222, "New Customers",
    [RFMScore] >= 111, "Promising",
    "Others"
)

**Step 7: Visualize RFM Analysis in Power BI**
1.	Create a new report in Power BI.
2.	Add visuals such as tables, charts, and slicers to display the RFM analysis.
3.	Use the calculated columns for Recency, Frequency, Monetary, RFMScore, and RFMCategory in your visuals.

## Dashboard 1: Customer Demographics
<img src="Dashboard 1.png"/>

**Key Performance Indicators (KPIs)**
1.	Total Sales: Measures the overall revenue generated.
2.	Number of Customers: Tracks the total number of customers.
3.	Sales by Gender: Breaks down sales by male and female customers.
4.	Sales by Customer Status: Differentiates sales between single and married customers.
5.	Sales by Age Group: Categorizes sales based on different age groups.

**Expected Outcomes**
1.	Increase in Total Sales: Aim to boost overall revenue.
2.	Growth in Number of Customers: Target an increase in the customer base.
3.	Balanced or Targeted Sales Distribution Across Genders: Achieve a balanced sales distribution or target specific gender demographics.
4.	Insights into Customer Status: Use data on customer status to tailor marketing strategies effectively.
5.	Identification of Key Age Groups: Identify and focus on age groups that contribute significantly to sales for targeted marketing efforts.

**Features**
1.	Dashboard Displaying Customer Demographics and Sales Data: A comprehensive dashboard that visualizes key metrics and demographic data.
2.	Interactive Map Showing Total Sales by Country: A world map highlighting sales distribution across different countries.
3.	Graphs and Charts Illustrating Sales Distribution:
*•	By Gender: Visual representation of sales split between male and female customers.
*•	By Customer Status: Charts showing sales distribution among single and married customers.
*•	By Age Group: Graphs depicting sales contributions from various age groups.

## Dashboard 2: Customer Segmentation
<img src="Dashboard 2.png"/>

**Key Performance Indicators (KPIs)**
1.	Number of Customers by Segment: Tracks the number of customers in each segment.
2.	Total Sales by Segment: Measures the total sales generated by each customer segment.
3.	Recency Value by Segment: Indicates how recently customers in each segment made a purchase.
4.	Frequency Value by Segment: Shows how often customers in each segment make purchases.
5.	Monetary Value by Segment: Represents the total monetary value of purchases made by customers in each segment.

**Expected Outcomes**

1.	Identification of Customer Segments: Classify customers into segments based on RFM (Recency, Frequency, Monetary) analysis.
2.	Understanding Customer Distribution: Gain insights into the distribution of customers across different segments.
3.	Sales Contribution by Segment: Understand the total sales contributed by each customer segment.
4.	Tailored Marketing Strategies: Use insights from recency, frequency, and monetary values to develop targeted marketing strategies for each segment.

**Features**
1.	Bar Charts for Number of Customers: Visual representation of the number of customers in each segment.
2.	Bar Charts for Total Sales: Visual representation of total sales for each customer segment.
3.	Bar Charts for Recency Value: Visual representation of recency values for each customer segment.
4.	Bar Charts for Frequency Value: Visual representation of frequency values for each customer segment.
5.	Bar Charts for Monetary Value: Visual representation of monetary values for each customer segment.

## Dashboard 3: Customer Details
<img src="Dashboard 3.png"/>

**Key Performance Indicators (KPIs)**

1.	Total Sales: Measures the overall revenue generated by each customer.
2.	Number of Customers: Tracks the total number of customers.
3.	Age Distribution: Categorizes customers based on their age.
4.	Marital Status Distribution: Differentiates customers based on their marital status.

**Expected Outcomes**
1.	Identification of High-Value Customers: Recognize customers who contribute significantly to total sales.
2.	Understanding Customer Demographics and Segmentation: Gain insights into customer demographics such as age, marital status, city, and country.
3.	Customer Distribution Analysis: Analyze the distribution of customers across different cities and countries.

**Features**
1.	Drill-Through Capability: Allows users to drill through from summary pages to view detailed customer information.
2.	Filtering Options: Dropdown menus for selecting specific products (ProductName) to filter the data.

**Specific Use for Drill-Through Feature**
This page is specifically designed to be used for the drill-through feature, enabling users to navigate from summary visuals to detailed customer information.

## Dashboard 4: Segment Description (Hidden Page)
<img src="Dashboard 4.png"/>

The hidden page provides detailed explanations of RFM (Recency, Frequency, and Monetary Value) analysis and its application in marketing actions. It includes definitions of each metric, what they measure, why they are important, and specific marketing actions based on customer segments derived from these metrics.

RFM analysis segments customers based on three key metrics: **Recency**, **Frequency**, and **Monetary Value**.
These metrics help businesses understand customer behavior and tailor marketing efforts effectively.

**1. Recency(R)**
*• What it measures: How recently a customer made a purchase or interacted with the business.
*• Why it’s important: Recent customers are more likely to respond to promotions or offers.

**2.Frequency(F)**
*• What it measures: How often a customer makes purchase or interacts with the business.
*• Why it’s important: Frequent customers are more loyal and ideal for upselling or retention campaigns.

**3.Monetary Value(M)**
*• What it measures: How much money a customer spend within a given period.
*• Why it’s important: Higher spenders are more profitable and should be targeted with personalized offers.

