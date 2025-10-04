# Tailwind-Traders-Sales-Analysis


This project is part of the **Power BI Data Visualization course on Coursera**.  
It demonstrates the full workflow of preparing, cleaning, analyzing, and visualizing sales data for Tailwind Traders using **Excel** and **Power BI Desktop**.

---

## Step 1: Prepare Sales Excel Data
1. Opened the Excel workbook `Tailwind Traders Sales.xlsx`.
2. Inserted a **Gross Revenue** column and calculated revenue per product using  
   **Formula:** `=E2*G2` (Gross Product Price × Quantity Purchased).
3. Created a **Total Tax** column and calculated tax per product using  
   **Formula:** `=F2*G2` (Tax per Product × Quantity Purchased).
4. Added a **Net Revenue** column and computed net earnings using  
   **Formula:** `=H2-I2` (Gross Revenue – Total Tax).
5. Applied formulas to all rows by dragging down.
6. Reviewed the first 10 records to identify highest and lowest values for **Net Revenue**, **Quantity Purchased**, and **Total Tax**, and observed trends with related columns like **Sales Rep**.

---

## Step 2: Import and Transform Data in Power BI
1. Imported the Excel file into **Power BI Desktop**.
2. Opened **Power Query Editor** to inspect the dataset.
3. Verified data types for all columns and fixed incorrect ones.
4. Removed unnecessary columns and renamed headers for clarity.
5. Ensured numeric columns were properly formatted for aggregations.
6. Closed and applied the changes to load the data model.

---

## Step 3: Create Calendar Table
Created a Calendar Table using DAX to support time intelligence calculations.

```DAX
CalendarTable =
ADDCOLUMNS(
    CALENDAR(DATE(2020, 1, 1), DATE(2023, 12, 31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Quarter", QUARTER([Date]),
    "Weekday", WEEKDAY([Date]),
    "Day", DAY([Date])
)
Then:

- Established a relationship between the **Calendar Table** and the **Sales Table** using the Date column.
- Verified the relationship direction is **one-to-many (1:*)**.

---

## Step 4: Create DAX Measures

Added calculated measures for deeper insights:

**Yearly Profit Margin**

Yearly Profit Margin = 
DIVIDE(
    SUM('Sales in USD'[Net Revenue USD]),
    SUM('Sales in USD'[Gross Revenue USD])
)

**Quarterly Profit Margin**

Quarterly Profit Margin = 
CALCULATE(
[Yearly Profit Margin],
DATESQTD('CalendarTable'[Date]))


**YTD Profit Margin**
YTD Profit Margin = 
DIVIDE(
    TOTALYTD(SUM('Sales in USD'[Net Revenue USD]), 'CalendarTable'[Date]),
    TOTALYTD(SUM('Sales in USD'[Gross Revenue USD]), 'CalendarTable'[Date])
)


**Median Sales**
Median Sales = MEDIAN('Sales in USD'[Gross Revenue USD])


---
## Steps 5 & 6: Sales and Profit Reports Summary

- Created the **Sales Overview** report:
  - Visualized **Loyalty Points by Country**, **Quantity Sold by Product**, **Median Sales Distribution by Country**, and **Median Sales Over Time** using bar, column, pie, and line charts.
  - Added **Card visuals** for Stock, Quantity Purchased, and Median Sales.
  - Inserted a **Country Name Slicer** for dynamic filtering.
  - Enabled data labels and a trend line where applicable.

- Created the **Profit Overview** report:
  - Visualized **Net Revenue by Product**, **Yearly Profit Margin by Country**, and **Yearly Profit Margin Over Time** using bar, donut, and area charts.
  - Added **Card visuals** for YTD Profit and Net Revenue USD.
  - Configured a **KPI visual** for Gross Revenue USD.
  - Inserted a **Calendar Date Slicer** for dynamic filtering.
  - Applied data labels and formatted visuals for clarity and readability.

---

## Conclusion

This project demonstrates the workflow of creating **Power BI Sales and Profit Reports** for Tailwind Traders, including:

- Data preparation and cleaning in Excel.
- Configuring data sources, tables, and relationships in Power BI.
- Creating DAX measures for key business metrics.
- Building interactive **Sales** and **Profit** reports with charts, cards, KPIs, and slicers.

All project files are included in this repository for reference.

