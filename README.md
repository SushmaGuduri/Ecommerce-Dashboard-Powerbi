# E-Commerce Sales & Profitability Analysis | Power BI

## Project Overview

This project is a Power BI dashboard analyzing an e-commerce business's sales and profitability performance across customer segments, regions, cities, products, and discount trends. The business had rich sales data but no clear view into whether high sales were actually translating into profit — this dashboard was built to answer that question.

**Goal:** build an interactive dashboard that could answer:
- Which customer segment generates the most sales?
- Which months and regions perform best?
- Which cities generate the most sales *and* profit?
- Which products are profitable or loss-making?
- Is there a relationship between discounts and profitability?
- Where should the business focus its attention?

---

## Dashboard

### Page 1 — Sales Overview
[![Sales Overview](https://github.com/SushmaGuduri/Ecommerce-Dashboard-Powerbi/raw/main/sales_page1.png)](/SushmaGuduri/Ecommerce-Dashboard-Powerbi/blob/main/sales_page1.png)

Covers: Total Sales, Total Orders, Average Order Value, Total Quantity, Sales by Segment, Monthly Sales Trend, Top 5 Cities by Sales & Profit, Sales by Sub-Category, Average Discount by Category.

### Page 2 — Profitability Analysis
[![Profitability Analysis](https://github.com/SushmaGuduri/Ecommerce-Dashboard-Powerbi/raw/main/profitability_page2.png)](/SushmaGuduri/Ecommerce-Dashboard-Powerbi/blob/main/profitability_page2.png)

Covers: Total Profit, Profit Margin, Profit per Order, Sales & Profit Margin by Region, Sales & Profit by Year, Profit Margin by Sub-Category, Discount vs Profit Margin, Monthly Profit & Profit Margin.

---

## Approach

Using Power BI, I:
- Prepared and explored the raw sales data
- Built KPIs for Sales, Profit, Orders, Quantity, and Average Order Value
- Analyzed sales by customer segment, region, city, and sub-category
- Compared discount levels against profit margins to test for a relationship
- Built the data model and DAX measures below to power both dashboard pages

**Data model & key measures:**

Built a star schema with a dedicated `DateTable` on the "one" side and the `Superstore` sales table on the "many" side, joined on date, to support proper time-intelligence calculations.

Key DAX measures:

```dax
Total Sales = SUM(Superstore[Sales])
Total Profit = SUM(Superstore[Profit])

Previous Year Sales = 
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DateTable[Date])
)

Profit Margin% = DIVIDE([Total Profit], [Total Sales], 0)

Sales YoY % = 
DIVIDE(
    [Total Sales] - [Previous Year Sales],
    [Previous Year Sales],
    0
)
```

`Profit Margin%` and `Sales YoY %` power the profitability and trend visuals across both dashboard pages; the dedicated date table enables the `SAMEPERIODLASTYEAR` time-intelligence pattern used in the year-over-year comparisons.
---

## Key Results & Insights

- The **Consumer segment** generated the highest sales at approximately **$1.16M**.
- **West** was the strongest region, with approximately **$725K in sales** and a **14.94% profit margin**.
- **New York City** led the top five cities on both sales and profit — **$256K in sales, $62K profit**.
- **Philadelphia** generated **$109K in sales but recorded a $13.84K loss** — flagged as a market needing investigation.
- **Tables** generated **$207K in sales** but carried a **-8.56% profit margin**.
- Within Furniture, higher discounts tracked with weaker margins — Tables carried a **26.13% average discount** alongside that -8.56% margin.
- **Labels, Paper, and Envelopes** were the strongest-margin categories, with Labels reaching **~44.42%**.

---

## Business Impact

The core finding: **high sales do not always mean high profitability.**

This supports:
- Identifying strong-performing regions and cities to double down on
- Investigating loss-making markets like Philadelphia
- Reviewing negative-margin products
- Reconsidering heavy discounting in low-margin categories
- Prioritizing **profitable growth over sales growth alone**

The discount-margin relationship shown here is an association, not proof of causation — a natural next step would be a controlled test isolating discount impact from other variables.

---

## Tools Used
Power BI · DAX

---

## Key Takeaway

A good dashboard isn't just about displaying numbers — it's about turning data into a decision-ready story: **Data → Analysis → Insight → Business Impact.**

The biggest lesson from this project: increasing sales alone isn't enough. The business also needs to know whether those sales are generating healthy profit.
