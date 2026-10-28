# Superstore-Sales-Performance
An interactive two-page Power BI dashboard that shows senior management of a national retail company where the business makes, and loses, money, with insights and recommendations drawn from four years of sales data (2014–2017).

> AnalystLab Africa Data Analytics Internship · Week 2: Business Intelligence & Interactive Dashboard Development

---

## Business Problem

Management had four years of order data but no single view of sales, profitability, customers and regions. They needed an executive dashboard to monitor performance and recommendations they could act on. The dashboard answers seven business questions:

1. What is the overall sales performance of the company?
2. Which regions generate the highest sales and profit?
3. Which customer segments contribute the most revenue?
4. Which product categories perform best?
5. Which products are the most profitable?
6. What trends can be observed over time?
7. What recommendations should management implement to improve business performance?

## Dataset

[Superstore Sales Dataset](https://github.com/adaeudoxie/Superstore-Sales-Performance/blob/main/Dataset.csv)

9,994 order lines × 21 columns, covering orders placed between 3 January 2014 and 30 December 2017 across the United States (4 regions, 49 states, 5,009 orders, 793 customers, 1,862 products). Each row is one product within an order.

## Data Preparation (Power Query)

| Check | Finding and Action |
| --- | --- |
| Missing values | None found (column quality 100% valid across the full dataset) |
| Duplicates | 1 duplicate order line (Row IDs 3406 and 3407 identical except Row ID). Removed by checking all columns except Row ID, a running record number that would otherwise hide the duplicate. 9,994 → 9,993 rows |
| Dates | Order Date and Ship Date converted using the English (United States) locale, because the file stores dates as M/D/YYYY |
| Postal Code | Converted to text and padded to 5 digits to restore leading zeros dropped in the CSV (e.g. 1040 → 01040) |
| Data types | Sales, Discount, Profit as decimal; Quantity and Row ID as whole numbers; all other fields as text |
| New columns | `Processing Duration` (Ship Date − Order Date) and `Profit Status` (Profit / Loss) |
| Calendar table | DAX date table (2014–2017) marked as a date table and related to Order Date, used for the year slicer and time analysis |

## Data Model & DAX

| KPI | Formula | Value |
| --- | --- | --- |
| Total Sales | `SUM(Orders[Sales])` | $2,296,919 |
| Total Profit | `SUM(Orders[Profit])` | $286,409 |
| Total Orders | `DISTINCTCOUNT(Orders[Order ID])` | 5,009 |
| Average Sales (average order value) | `DIVIDE([Total Sales], [Total Orders])` | $458.56 |
| Profit Margin | `DIVIDE([Total Profit], [Total Sales])` | 12.47% |

## Dashboard

| Page | Visuals |
| --- | --- |
| **Performance Overview** | 5 KPI cards · Yearly Sales Performance (sales, profit and margin) · Regional Sales Performance · Segment Sales Performance (donut) · Sales Trend Analysis (monthly line) |
| **Detailed Analysis** | Top 10 Most Profitable Products · Sales Performance per Product Category · Profit by State (map) · Sub-category matrix · Key Insights panel |

Year, Region and Segment slicers are synced across both pages, and Next / Back buttons link the pages.

[*Figure 1: Performance Overview Dashboard*](https://github.com/adaeudoxie/Superstore-Sales-Performance/blob/main/Dashboards/Pg.%201.png)
<img width="3026" height="1736" alt="Performance Overview" src="https://github.com/user-attachments/assets/ddb93892-5ace-4524-bcb1-c8a2fb268f59" />

*Figure 2: Detailed Analysis Dashboard*
<img width="3028" height="1740" alt="Detailed Analysis" src="https://github.com/user-attachments/assets/e2089b50-88ef-44ad-ab62-b90a53e6f0d3" />


## Key Insights

1. *Profit is concentrated.* The West and East regions generate 70% of profit, and California and New York alone earn over half of all profit ($150K). Texas is the 3rd-largest state by sales but the biggest loss-maker (−$25.7K).
2. *Consumers drive revenue, Home Office drives margin.* Consumers bring in 50.6% of sales, but Home Office earns the highest margin (14.0% vs 11.5%).
3. *Furniture category barely makes a profit.* It sells almost as much as Technology ($742K vs $836K) but earns a 2.5% margin vs 17.4%. Tables (−$17.7K), Bookcases (−$3.5K) and Supplies (−$1.2K) lose money.
4. *Copiers are the most profitable products.* Copiers earn $55.6K at a 37.2% margin; the Canon imageCLASS 2200 alone earns $25.2K.
5. *Steady growth with year-end peaks.* Sales grew 51% from 2014 to 2017 and profit grew 89%. September–December brings in 52% of yearly sales.

## Recommendations

1. Reprice, renegotiate or cut loss-making Tables and Bookcases lines.
2. Run a profitability review (pricing, discounts, shipping) in Texas, Ohio, Pennsylvania and Illinois.
3. Apply West-region pricing and product-mix practices to the Central region (7.9% margin).
4. Promote high-margin lines such as Copiers, Paper, Labels and Envelopes.
5. Build bundles and loyalty pricing for the Home Office segment.
6. Plan stock and staffing for the September–December peak and run promotions in January–February.

Full analysis, including risks and opportunities, is in the [Executive Summary Report](https://github.com/adaeudoxie/Superstore-Sales-Performance/blob/main/Reports/Executive%20Summary.pdf).

## Repository structure

```
├── data/        Superstore_Dataset.csv (raw data)
├── dax/         measures.dax (KPI measures and Calendar table)
├── docs/        BI Overview Report and Executive Summary Report
├── images/      Dashboard screenshots
└── report/      Power BI file (.pbix) and PDF export
```

## Tools & Skills

- Power BI Desktop
- Power Query
- DAX
- Data Modelling
- Dashboard Design
- Report Writing

---

*Tags: #AnalystLabAfrica #PowerBI #DataAnalytics #BusinessIntelligence*
