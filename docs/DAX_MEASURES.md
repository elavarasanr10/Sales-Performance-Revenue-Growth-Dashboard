# DAX Measures

Create each of these under **Home → New Measure** (with `Sales_Data` selected in the Fields pane). Put them all into a dedicated `_Measures` table for a clean model: **Modeling → New Table**, type `_Measures = {}`, then move each measure into it via its properties pane.

## Core sales measures

**Total Revenue**
```
Total Revenue = SUM('Sales_Data'[Revenue])
```
Adds up every transaction's revenue — the base number most other measures build on.

**Total Cost**
```
Total Cost = SUM('Sales_Data'[Cost])
```

**Total Profit**
```
Total Profit = [Total Revenue] - [Total Cost]
```

**Profit Margin %**
```
Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)
```
`DIVIDE` avoids errors when Total Revenue is 0 for a filtered slice.

**Total Units Sold**
```
Total Units Sold = SUM('Sales_Data'[Units Sold])
```

## Target and achievement measures

**Target Sales**
```
Target Sales = SUM('Sales_Data'[Target Sales])
```

**Actual Sales**
```
Actual Sales = SUM('Sales_Data'[Actual Sales])
```

**Achievement %**
```
Achievement % = DIVIDE([Actual Sales], [Target Sales], 0)
```
Above 100% means the region/category/executive in the current filter context beat target; below means they missed it.

**Growth %**
```
Growth % = AVERAGE('Sales_Data'[Growth %])
```
Averages the row-level Growth % (already calculated in the Excel source against a prior-period baseline) across the current filter context. For a true time-intelligence version instead of averaging a pre-computed column, use:
```
Growth % (MoM) =
VAR CurrentRevenue = [Total Revenue]
VAR PreviousRevenue = CALCULATE([Total Revenue], DATEADD('Sales_Data'[Date], -1, MONTH))
RETURN DIVIDE(CurrentRevenue - PreviousRevenue, PreviousRevenue, 0)
```
This needs a proper Date table marked as the model's date table for `DATEADD` to work correctly.

## Breakdown measures

**Region-wise Revenue**
```
Region-wise Revenue = CALCULATE([Total Revenue], ALLEXCEPT('Sales_Data', 'Sales_Data'[Region]))
```
Forces revenue to always break down by Region regardless of other active slicers — powers the "Revenue by Region" column chart and the "top performing region" insight.

**Category-wise Performance**
```
Category-wise Performance = CALCULATE([Total Profit], ALLEXCEPT('Sales_Data', 'Sales_Data'[Product Category]))
```
Same pattern applied to Product Category and Profit — the highest-revenue category isn't always the most profitable one, so this is deliberately profit-based.

**Sales Executive Performance**
```
Sales Executive Performance = CALCULATE([Actual Sales], ALLEXCEPT('Sales_Data', 'Sales_Data'[Sales Executive Name]))
```
Same pattern applied to Sales Executive Name — powers an executive leaderboard visual.

## Helper measures for KPI cards and insights

**Top Performing Region**
```
Top Performing Region =
VAR RankedRegions =
    TOPN(1, VALUES('Sales_Data'[Region]), CALCULATE([Total Revenue]), DESC)
RETURN
    CONCATENATEX(RankedRegions, 'Sales_Data'[Region])
```

**Top Performing Product Category**
```
Top Performing Product Category =
VAR RankedCategories =
    TOPN(1, VALUES('Sales_Data'[Product Category]), CALCULATE([Total Profit]), DESC)
RETURN
    CONCATENATEX(RankedCategories, 'Sales_Data'[Product Category])
```
Ranked by profit rather than revenue, deliberately, since the highest-revenue category isn't always the most profitable.

**Best Sales Executive**
```
Best Sales Executive =
VAR RankedExecs =
    TOPN(1, VALUES('Sales_Data'[Sales Executive Name]), CALCULATE([Achievement %]), DESC)
RETURN
    CONCATENATEX(RankedExecs, 'Sales_Data'[Sales Executive Name])
```
Ranked by Achievement %, so it rewards hitting target rather than just having the largest territory.

**Channel-wise Sales Performance**
```
Channel-wise Sales Performance = CALCULATE([Total Revenue], ALLEXCEPT('Sales_Data', 'Sales_Data'[Sales Channel]))
```
Same ALLEXCEPT pattern applied to Sales Channel, for the donut chart and channel comparison.
