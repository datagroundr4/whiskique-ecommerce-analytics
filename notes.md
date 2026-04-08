## Notes

### Data model and tables
Snowflake data model 
Tables: 
- Fact table: Sales -> Trnasaction Date, Customer ID, Description, Stock Code, Invoice No, Sales, Unit Price, Quantitty 
- Dimension tables:
    - Customers: Customer ID, Order State, Order City, Order Postal
    - Products: Stock code, Description, category, Shipping_Cost_1000_mile, Landed Cost, Weight
    - State Mapping: State, Region.

New created tables.

The fact_sales table (Sales) have 24404 rows representing uniques transactions at a item level
There are 11427 unique records at Invoice No

The total number of custumers of the store is 3141 being California the state that holds the mojority of clients with with 419 

The average Customer Life Time Value is $494.72 
DAX -> Customer LTV (avg) = SUM(Sales[Sales])/[Number of Customers]

The best-selling product is "Sheba Perfect Portions Pat Wet Cat Food" with an average quantity of 7.07 
The lowest-selling product is Indoor Pet Camera (Wi-Fi)

The product with the highest delivery cost per 1000 miles is "Taste of the Wild High Prairie Grain-Free Dry Dog Food 40lb" with $20
The lowest shipping cost per 1000 mile product is "Sheba Perfect Portions Pat Wet Cat Food" with $2.50

Implemented a grouped by `Invoice No` table on Power Query based on a duplicated of Sales, to view aggregated total for `Sales` & `Quantity`.

The five most frequent product groupings in a single transaction are: 2 items (7.22%), 3 items (6.68%), 4 items (6.52%), 1 item (5.98%), and 6 items (5.28%).

Now we want to understand better our customer purchasing patterns: If they buy one specific product, what else do they buy?
Implemented a new table based on a duplcate of Sales and named Market Basket, also created a new relationship with sales using the `Invoice No` field.

Implemented an interaction between two visuals: A table with product description and a horizaontal bar with product description counts. Using this visuals we can determine which products are purchased together.

## E-commerce analytics
Shipping constas by What-If analysis

implemented a map visual by State and region 
The states that holds more customers per region are: California in the west region, Texas in the Central region, and New York in the East Region
Florida is the state with highest sales in the east region

# What-If Analysis
Adding the `Shipping Cost`column from the `Customers`table
Adding a new measure in `Sales`:
Shipping (Baseline) = SUMX(Sales, IF(Sales[Quantity] = 1, Sales[Shipping Cost], Sales[Shipping Cost] + (((Sales[Quantity])-1)* Sales[Shipping Cost]*0.07)))
To calculate adjusted shipping costs: The original `Shipping Cost`field represents the base cost for a single item. For orders with multiple items, the shipping cost increases by 70% for each aditional unit beyond the first.
Creating a new integer parameter `What-if quantity` with values from 1 to 20 in steps of one, with the current value set to 5.
Creation af a new measure in the `What-if quantity` table called `Blended Shipping Cost Factor`which calculates the disconunted shipping cost based on the following table
| What-if quantity Value <= (less than or equal) | Cost multiplier (output) |
|---------------|----------------|
| 1 | 1 |
| 2 | 0.8 |
| 4 | 0.6 |
| 7 | 0.5 |
| 9 | 0.4 |
| else, | 0.3 |
Blended Shipping Cost Factor = IF('What-if Quantity'[What-if quantity Value]<=1, 1, IF('What-if quantity'[What-if quantity Value]<=2, 0.8, IF('What-if Quantity'[What-if quantity Value]<=4, 0.6, IF('What-if Quantity'[What-if quantity Value]<=7, 0.5, IF('What-if Quantity'[What-if quantity Value]<=9, 0.4, 0.3)))))
The shipping baseline is $385,15K
We can show the differences between the baseline values and the what-if values, changing the value of the parameter.
Creating a new measure in the `Sales`table `Shipping What-if` with the same DAX formula used in `Shipping (Baseline)` but using `Blended Shipping Cost Factor` instead of a fixed value of 0.7
Shipping (What-if) = SUMX(Sales, IF(Sales[Quantity] = 1, Sales[Shipping Cost], Sales[Shipping Cost] + (((Sales[Quantity])-1) * (Sales[Shipping Cost] * [Blended Shipping Cost Factor]))))
We want to show the running total of the shipping metrics over time:
Create a new measure `Baseline Running Total` summing the the `Shipping (Baseline)` acrioss the whole table ensuring that all values are selcted, and each new total is summed for a date before the max `Transaction Date`
Baseline Running Total = SUMX(FILTER(ALLSELECTED(Sales), Sales[Transaction Date] <=MAX('Market Basket'[Transaction Date])), [Shipping (Baseline)])
Creating the measure `What-if running total`
What-if running total = SUMX(FILTER(ALLSELECTED(Sales), Sales[Transaction Date] <= MAX('Market Basket'[Transaction Date])), [Shipping (What-if)])
Creating the measure `Difference running total` 
Difference running total = SUMX(FILTER(ALLSELECTED(Sales), Sales[Transaction Date] <= MAX('Market Basket Analysis'[Transaction Date])), Shipping (Difference)])

## Main questions
- Who are my top customers
- What are the company profits?
- 

Creation of a new column `COGS` in the `Sales` table and set it as Currency format with two decimal places:
COGS = Sales[Quantity] * RELATED(Products[Landed Cost])
Creation of a new column `Profit (Baseline)` in the `Sales` table and set it as Currency format with two decimal places:
Profit (Baseline) = Sales[Sales] - Sales[COGS] - [Shipping (Baseline)]
Creation of a new column `Profit %` in the `New_Measures` table and set it as Currency format with two decimal places:
Profit % = SUM(Sales[Profit (Baseline)]) / SUM(Sales[Sales])

## Final dashboard pages
### Executive Summary
- KPI Cards: Tatal Sales · Total Profit (Baseline) · Profit % · Shipping (Baseline)
- Slicer filter for Product Description
- Treeemap: Profit % by product category
- Filled Map: Total Sales by State
- Bar chart: Total Sales by Description and Category
Electronics has the highest overall profit percentage margin with 44.28%

### Shipping Metrics
- KPI Cards: Shipping (Baseline) · Shipping (What-if) · Shipping (Difference)
- What-if Quantity parameter slicer
- Column charts: Impact of Shipped Quantity on Shipping Costs by Product · Average Quantity by Category
- Area chart: Impact of Shipped Quantity on Shipping Costs
- Map: Shipping cost by State and Region

### Market Basket Analysis
- Table with interaction filter: Product Description 
- Bar Chart: Combination of Purchased Items
- Column Chart: Total Sales and Profit % by Description
