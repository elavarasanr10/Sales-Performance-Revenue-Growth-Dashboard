# Power Query Steps (Beginner-Friendly, Click-by-Click)

Follow every step in order. If you want the full cleaning practice, load `Raw_Dataset_Before_Cleaning.xlsx`; otherwise load `Sales_Performance_Dataset.xlsx` directly (already clean) and skip to Step 8.

## Step 1 — Open Power BI Desktop and load the file

1. Open **Power BI Desktop**.
2. On the Home ribbon, click **Get Data → Excel workbook**.
3. Browse to and select your chosen file.
4. Click **Open**.
5. In the Navigator window, tick the checkbox next to the data sheet (**Raw_Data** or **Sales_Data**).
6. Click **Transform Data** (not "Load") to open the Power Query Editor.

## Step 2 — Remove null values

The raw file has a few blank cells in **Region** and **Units Sold**.

1. Click the **Region** column header.
2. Right-click → **Remove Empty**. A missing region breaks every region-based visual, so that row is dropped.
3. Click the **Units Sold** column header.
4. Right-click → **Replace Values** → leave "Value To Find" blank, type `0` in "Replace With" → **OK**. This keeps the row (the rest of the transaction data is still valid) with a safe default instead of a gap.

## Step 3 — Fix inconsistent text casing

Some **Region** values came in lowercase (e.g. `west` instead of `West`).

1. Click the **Region** column header.
2. Go to **Transform → Format → Capitalize Each Word**.

## Step 4 — Trim extra whitespace

Some **State/City** values have extra spaces (`"  Pune "`).

1. Click the **State/City** column header.
2. Go to **Transform → Format → Trim**.

## Step 5 — Remove duplicate rows

1. Select all columns (click the top-left corner or press **Ctrl+A** in the column header area).
2. Go to **Home → Remove Rows → Remove Duplicates**. Power Query only removes a row if every column matches exactly, which correctly catches the accidental duplicate transactions in the raw file.

## Step 6 — Change data types

Check each column's type icon in the header and correct any that were guessed wrong:

- **Date** → Date
- **Selling Price, Revenue, Cost, Profit, Target Sales, Actual Sales** → Fixed Decimal Number
- **Profit Margin %, Achievement %, Growth %** → Percentage
- **Year, Units Sold** → Whole Number
- **Everything else** (Region, State/City, Sales Executive Name, Product Category, Product Name, Customer Type, Sales Channel, Month, Quarter) → Text

Click the type icon on the left of each column header, or use **Transform → Data Type**.

## Step 7 — Confirm/derive Month, Quarter, Year

Already included as columns in this dataset, but if you're working from a raw date-only source:

1. Click the **Date** column header.
2. **Add Column → Date → Month → Name of Month** → adds `Month`.
3. Click **Date** again → **Add Column → Date → Quarter → Quarter of Year** → adds a numeric Quarter; optionally wrap it with **Add Column → Custom Column** using `"Q" & Text.From([Quarter])` to match the "Q1" style used in this dataset.
4. Click **Date** again → **Add Column → Date → Year → Year** → adds `Year`.

## Step 8 — Rename columns

Keep names business-friendly, matching the style already used in this dataset: full words, title case, no abbreviations (e.g. `Sales Executive Name`, not `SalesExecName`). Right-click a column header → **Rename** if you need to adjust anything.

## Step 9 — Format currency and percentage fields

Formatting in Power Query is cosmetic and doesn't change the underlying value — the important step is the correct **data type** from Step 6. Apply visual-level currency/percentage formatting later in Report view via the **Format** pane on each visual, or set it globally on the column in **Model view** (`$ English (United States)` for currency fields, `Percentage` for Profit Margin %, Achievement %, and Growth %).

## Step 10 — Add calculated columns where needed

`Revenue`, `Cost`, `Profit`, `Profit Margin %`, `Target Sales`, `Actual Sales`, `Achievement %`, and `Growth %` already exist as formula-driven columns in the Excel source. If you're rebuilding from a different raw file, add them in Power Query as custom columns, or — preferably — build them as **DAX measures** instead (see `DAX_MEASURES.md`), since measures recalculate dynamically as slicers filter the report while Power Query columns are fixed at refresh time.

## Step 11 — Close & Apply

1. Go to **Home → Close & Apply**.
2. Power BI loads the cleaned table into the data model. Move on to `DAX_MEASURES.md`.
