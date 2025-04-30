# Customer-Segmentation-RFM-Analysis

# Overview
About /Intro - This project focuses on leveraging Power BI to create a comprehensive dashboard that provides detailed customer demographics and segmentation analysis. By utilizing key performance indicators (KPIs), expected outcomes, and advanced features such as drill-through capabilities, this project aims to empower decision-makers with actionable insights to drive strategic initiatives. Additionally, the project incorporates RFM (Recency, Frequency, Monetary) analysis to classify customers into segments based on their purchasing behaviors, further enhancing the depth of insights.

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

##Dashboard 1: Customer Demographics##
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
