# KPI_Dashboard
A beginner-friendly finance dashboard project built using Power BI to track key financial metrics and KPIs. Designed to develop practical skills in financial analysis, data visualization, and interactive reporting.

In this blog post, I’ll walk you through the end-to-end process of building a powerful and interactive KPI dashboard in Power BI, starting from a raw Excel file to a fully functional report. Whether you're a beginner or a data enthusiast looking to sharpen your Power BI skills, this quick overview which covers key features like Power Query, Data Modeling, DAX calculations, and dashboard design best practices.
Tools used: Power BI Desktop
Dataset: https://github.com/AkashParit/KPI_Dashboard/blob/main/Dataset/actual-vs-target-dataset.xlsx
Skills covered: Power Query, DAX, Data Modeling, Visual Design

  

Step 1: Data Preparation using Power Query

What I did:

Imported the Excel file (actual-vs-target-dataset.xlsx) into Power BI.
Used Power Query Editor to clean and transform the data.
Applied Unpivot Columns to restructure monthly data into a tall format (essential for time-based analysis).
Before and After of Unpivoted Data


Tips: Rename columns for clarity.

Step 2: Data Modelling – Building the Semantic Layer

What I did:

Created relationships between multiple fact tables (e.g., Actuals and Targets).
Ensured proper cardinality and cross-filter directions.
Made use of star schema design principles.
Model View (connecting the relationship from one to many)



Note: 

I initially encountered issues with broken relationships and formula errors in my Power BI model. To resolve this, I carefully reviewed the data types and formats of the related columns. I then established proper relationships by:

Connecting the Actual table to DimPeople using Salesperson → Salesperson
Connecting the Target table to DimPeople using Salesperson → Salesperson
Linking the Actual table to the Calendar table via Month → Date
Linking the Target table to the Calendar table via Month → Date
To ensure these relationships functioned correctly, I changed the format of the Month column in both the Actual and Target tables to match the Date format used in the Calendar table. After fixing the formats and reconnecting the tables, I revalidated the DAX measures, and the calculations started working as expected.



Step 3: DAX Calculations for Insights

Key Calculations Built:

Year-To-Date (YTD) metrics
Target vs Actual comparisons
KPI indicators using Emoji + DAX
Used FILTER, CALCULATE, TOTALYTD, and other powerful functions
Note: 

DAX formulas in Power Pivot

1. Total Sales Actual = SUM(Actual[Sales])
2. Total Sales Target = Sum(Targets[Sales])
3. Variance = [Total Sales Actual] - [Total Sales Target]
4. Variance % = DIVIDE([Variance], [Total Sales Target])
5. YTD Sales Actual = CALCULATE([Total Sales Actual], DATESYTD('Calendar'[Date]))
6. YTD Sales Target = CALCULATE([Total Sales Target], DATESYTD('Calendar'[Date]))
7. YTD Variance = CALCULATE([Variance], DATESYTD('Calendar'[Date]))
8. YTD Variance % = CALCULATE([Variance %], DATESYTD('Calendar'[Date]))
9. Trend Chart Title =
 var month_count = COUNTROWS('Calendar') 
 RETURN
   "We meet targets for " & [Months Target Reached] & " out of " & month_count
10. Variance Pct Label = VAR up = "🟢"

VAR down = "🔴"

VAR formated_var_pct = FORMAT(ABS([Variance %]), "0.0%")

RETURN

formated_var_pct & " " & IF([Variance %] >0, up, down)

 

Step 4: Visualizing the Dashboard & Enhancing Interactions

Dashboard Features:

Card visuals with reference labels and emoji
Sparklines inside table visuals for trend lines
Custom data labels on charts
Smart Narrative auto-summary of KPI data
Polished executive-style table formattin
Final KPI dashboard overview




Team 1 Performance



Overall performance as per month 



Showing the overall performance of a Salesperson





Key Learnings and Tips
Here are some standout tips and tricks I applied in the project:

Power Query Unpivot – Transforms wide month-based data to tidy time-series format.

Multiple Fact Tables – Learn to manage complex models with proper relationships.

YTD Calculations – Use TOTALYTD with proper time intelligence setup.

Emoji in DAX – Use Unicode characters to make KPIs intuitive and engaging.

FILTER Function – Essential for building dynamic calculated measures.

Smart Narrative – Auto-generate executive summaries.

Custom Labels & Themes – Boost the polish and readability of your visuals.


Challenges I Overcame
DAX errors due to incorrect formats: Fixed by cleaning column types and checking relationships.

Model issues: Rebuilt the relationship view from scratch for better clarity.

Performance tweaks: Disabled auto date and optimized calculated columns.


Final Thoughts
Building this Power BI dashboard was a deep dive into some of the most essential features of the platform. From data wrangling to interactive storytelling, this project gave me hands-on experience in crafting executive-ready reports.

