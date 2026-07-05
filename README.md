# jcars_assignment
The goal of this project is to build an interactive Power BI dashboard that helps JCARS Logistics management understand     
- Overall sales performance for the period.
- The most profitable vehicle makes and the best performing branches and regions.
- The logistics cost efficiency of the branches.
- The best performing sales rep and the lead source with the most turn arround into an actual sale.
- The payment behaviors of the customers. 
- The trends of order cancellations and returns after sales.
## Data Importation into Aiven
- Requires an established PostgreSQL service on your console.
- Launch DBeaver
- Go to database Navigator and find your Aiven connection. Right click the specific Table and select Import Data.
- Browse your computer for the file you want to upload.
- Review the settings and click Finish.
## Connecting Power BI to the database
 - In Power BI Desktop: Get Data → Database → PostgreSQL database.
 - Entered the Aiven host and port, and selected Import or DirectQuery mode.
 - Provided the database credentials (username/password).
 - Selected the relevant tables in Navigator and loaded them into the Power BI data model.
## Relevant Measures
- `Total Sales Revenue = SUM('public jcars'[Revenue Recorded])`
- `Total Units Sold = SUM('public jcars'[Units Sold])`
- `Order Count = DISTINCTCOUNT('public jcars'[Order ID])`
- `Gross Profit = [Total Sales Revenue]-[Total COGS]`
- `Gross Profit Margin = DIVIDE([Gross Profit],[Total Sales Revenue],0)`
- `Profit Margin = DIVIDE([Gross Profit],[Total Sales Revenue],0)`
- `Average Revenue Per Order = DIVIDE([Total Sales Revenue],DISTINCTCOUNT('public jcars'[Order ID]))`
- `Logistics Cost % of Revenue = DIVIDE([Total Logistics Cost],[Total Sales Revenue],0)`
- `Cancelled Count = CALCULATE([Order Count],'public jcars'[Delivery Status]="Cancelled")`
- `Returned Count = CALCULATE([Order Count],'public jcars'[Returned]="Yes")`
- `Average Rating = AVERAGE('public jcars'[Customer Rating])`
## Visuals Used
### Sales Overview
- KPI cards: Total Units Sold, Total Sales Revenue, Gross Profit, Gross Profit Margin
- Bar chart: Total Sales Revenue by Car Make
- Clustered bar chart: Total Sales Revenue & Total Units Sold by Vehicle Type
### Branch & Sales Rep Performance
- Bar chart: Total Sales Revenue by Branch
- Bar chart: Total Sales Revenue by County
- Clustered column chart: Total Sales Revenue & Total Units Sold by Sales Rep
- Clustered column chart: Total Sales Revenue & Average Revenue Per Order by Lead Source
### Trends Over Time
- Line-and-column combo chart: Total Sales Revenue, Total Units Sold, and Gross Profit by Date
### Payments & Fulfillment
- Donut chart: Total Sales Revenue by Payment Method
- Donut chart: Total Sales Revenue by Payment Status
- Donut chart: Order Count by Payment Status
- Bar chart: Order Count by Delivery Status
### Customers & Returns
- Bar chart: Total Sales Revenue by Customer Name (top customers)
- Clustered bar chart: Cancelled Count & Returned Count by Car Make
- Column charts: Total Sales Revenue and Total Units Sold
### Executive Summary
- Title banner: "JCARS Logistics"
- KPI cards: Total Sales Revenue, Total Units Sold, Order Count, Gross Profit, Average Rating
- Line-and-column combo chart: Revenue, Units Sold, Gross Profit over time
- Bar charts: Revenue by County, Profit Margin by Car Make
- Slicers: County, Car Make, Payment Status, Month
## Key Insights
- Kakamega Branch and Region lead in total revenue.
- Customers do not necessarily prefer a specific payment method.
- Nairobi Branch has the highest logistics cost.
- Dealers and the Government make up the largest percentage of the customers.
- Toyota makes up the majority of returned and cancelled orders
## Recommendations
- Double down on top performers, allocate more inventory/marketing budget to the car make(s) and branches driving the most revenue.
- Investigate underperforming branches, review pricing, staffing, or local demand in low-revenue branches/counties.
- Improve profit margins on high-volume, low-margin models. Renegotiate procurement costs or adjust pricing for these car makes.
- Reduce logistics costs, target branches with a high Logistics Cost % of Revenue for route optimization or vendor renegotiation.
- Address payment/delivery bottlenecks, follow up on pending payments and investigate causes of delivery delays.
- Reduce cancellations/returns, investigate root causes for the car make(s) with the highest cancelled/returned counts (e.g., quality issues, misleading listings, financing problems).
- Reward top sales reps and lead sources, replicate the practices of the highest-performing reps/channels across the team.


