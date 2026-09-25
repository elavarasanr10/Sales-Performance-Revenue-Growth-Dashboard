# Sales Performance & Revenue Growth Dashboard

A Power BI dashboard that tracks sales trends, revenue growth, and target achievement across regions, product categories, and sales executives — built to mirror how a sales manager, business analyst, or leadership team monitors performance and decides where to focus next.

## Objective

To create an interactive Power BI dashboard that tracks sales trends, revenue growth, and product/category performance to help businesses make data-driven decisions. Specifically, to answer:
1. Are we hitting our sales targets, and by how much?
2. Which regions, categories, and executives are driving growth — and which are lagging?
3. How is revenue trending month over month?
4. Which sales channel and customer type combination performs best?

## Tools Used

- **Power BI Desktop** — data modeling, DAX, dashboard build
- **Power Query** — data cleaning and transformation
- **Microsoft Excel** — source dataset
- **DAX (Data Analysis Expressions)** — KPI and measure logic
- **GitHub** — version control and portfolio hosting

## Dataset Description

`Sales_Performance_Dataset.xlsx` contains 150 transaction-level rows (Jan 2024 – Dec 2025) with 22 columns:

| Column | Description |
|---|---|
| Date | Transaction date |
| Month | Month name, derived from Date |
| Quarter | Q1–Q4, derived from Date |
| Year | Calendar year |
| Region | North / South / East / West / Central |
| State/City | Specific city within the region |
| Sales Executive Name | Executive who closed the sale |
| Product Category | Electronics, Home Appliances, Furniture, Apparel, FMCG |
| Product Name | Specific product sold |
| Units Sold | Quantity sold in the transaction |
| Selling Price | Price per unit |
| Revenue | Units Sold × Selling Price |
| Cost | Direct cost associated with the sale |
| Profit | Revenue − Cost |
| Profit Margin % | Profit ÷ Revenue |
| Customer Type | New / Existing |
| Sales Channel | Online / Offline |
| Target Sales | Planned/target revenue for this transaction's slice |
| Actual Sales | Revenue actually achieved (equals Revenue) |
| Achievement % | Actual Sales ÷ Target Sales |
| Growth % | (Revenue − Previous Period Revenue) ÷ Previous Period Revenue |
| Previous Period Revenue (Reference) | Helper column: a synthetic prior-period revenue baseline used to compute Growth % |

`Revenue`, `Cost`, `Profit`, `Profit Margin %`, `Target Sales`, `Actual Sales`, `Achievement %`, and `Growth %` are all live Excel formulas, not hardcoded — open the file and click any of those cells to see exactly how each number was derived.

A second file, `Raw_Dataset_Before_Cleaning.xlsx`, is the same data before cleanup — it deliberately contains null values, inconsistent text casing, extra whitespace, and duplicate rows for the Power Query cleaning walkthrough.

## Power Query Steps

See [`docs/POWER_QUERY_STEPS.md`](docs/POWER_QUERY_STEPS.md) for the full click-by-click walkthrough. Summary: remove nulls, fix casing, trim whitespace, remove duplicates, correct data types, confirm/derive Month, Quarter, Year, rename columns, and format currency/percentage fields.

## DAX Measures

See [`docs/DAX_MEASURES.md`](docs/DAX_MEASURES.md) for every measure with its formula and a plain-language explanation. Includes: Total Revenue, Total Cost, Total Profit, Profit Margin %, Total Units Sold, Target Sales, Actual Sales, Achievement %, Growth %, Region-wise Revenue, Category-wise Performance, Sales Executive Performance.

## Dashboard Features

- **KPI cards:** Revenue, Profit, Units Sold, Achievement %, Growth %
- **Column chart:** Revenue by Region
- **Bar chart:** Product Category performance
- **Line chart:** Monthly Revenue trend
- **Donut chart:** Sales Channel distribution
- **Clustered column chart:** Target vs. Actual Sales
- **Matrix table:** Region × Revenue × Profit × Achievement %
- **Slicers:** Region, Category, Channel, Sales Executive, Month
- **Corporate color theme:** blue for neutral metrics, green for profit and over-target performance, red/orange for under-target/low performance

## Key Insights

*(Fill in with your actual numbers once you build the dashboard — sample structure below)*

- Which region generates the highest revenue vs. which has the highest achievement % (often not the same)
- Which product category is most profitable, not just highest-revenue
- Whether the company is hitting sales targets overall, and which regions are dragging the average down
- The shape of the monthly revenue trend across the two-year window
- Which sales channel and customer type combination (e.g. Online + New) converts best
- Which sales executives are consistently over-achieving vs. under-achieving target

## Screenshots

Add dashboard screenshots here after building in Power BI Desktop:

```
screenshots/
  01-full-dashboard.png
  02-kpi-cards.png
  03-revenue-by-region.png
  04-target-vs-actual.png
  05-monthly-trend.png
```

`![Dashboard Overview](screenshots/01-full-dashboard.png)`

## Repository Structure

```
sales-performance-revenue-growth-dashboard/
├── README.md
├── Sales_Performance_Dataset.xlsx
├── Raw_Dataset_Before_Cleaning.xlsx
├── Sales-Performance-Revenue-Growth-Dashboard.pbix   (add after building in Power BI Desktop)
├── docs/
│   ├── POWER_QUERY_STEPS.md
│   ├── DAX_MEASURES.md
│   ├── REPORT_BUILD_GUIDE.md
│   ├── PROJECT_OVERVIEW.md
│   ├── RESUME_DESCRIPTIONS.md
│   ├── LINKEDIN_CONTENT.md
│   └── PROJECT_CHECKLIST.md
└── screenshots/
    └── (dashboard images go here)
```

## Conclusion

This project demonstrates an end-to-end BI workflow: messy raw data → cleaned and modeled data → DAX-driven sales KPIs → a decision-ready dashboard. It reflects the kind of sales performance tool used by sales analysts, business analysts, and revenue managers to track growth and target achievement.
