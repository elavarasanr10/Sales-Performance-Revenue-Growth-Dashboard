# Report Building & Dashboard Design — Beginner Walkthrough

This picks up after `DAX_MEASURES.md` — you should already have your cleaned table loaded and your measures created in a `_Measures` table before starting here.

## Step 1 — Set up the canvas

1. Switch to the **Report** view (middle icon on the left sidebar).
2. Click the blank canvas → **Format pane (paint roller icon) → Canvas settings** → set page size to **16:9**.
3. Go to **View → Themes**, pick a base theme close to corporate blue, or use **Format → Customize current theme** to set exact colors (see Step 6 below).

## Step 2 — Add the KPI cards (top section)

1. Drag **Total Revenue** from the Fields pane onto the canvas → click the **Card** visual icon in the Visualizations pane to convert it from the default table.
2. Resize it to a small rectangle, place it at the top-left.
3. Repeat for **Total Profit**, **Total Units Sold**, **Achievement %**, and **Growth %** — five cards total in a single row.
4. Select all five (click one, Shift+click the rest) → **Format → Align → Align Top** and **Distribute Horizontally** for even spacing.
5. Set each card's title via **Format pane → General → Title** to match its measure name.

## Step 3 — Add the middle-section charts

1. **Column chart — Revenue by Region:** click **Clustered Column Chart** → drag **Region** to the X-axis and **Region-wise Revenue** (or **Total Revenue**) to the Y-axis (values).
2. **Bar chart — Product Category performance:** click **Clustered Bar Chart** → drag **Product Category** to the Y-axis and **Category-wise Performance** to the X-axis (values).
3. **Line chart — Monthly Revenue trend:** click **Line Chart** → drag **Month** (and **Year**, for a proper two-year trend) to the X-axis and **Total Revenue** to the Y-axis (values). Sort the axis chronologically if it defaults to alphabetical (right-click the visual → **Sort by → Date**, or use a numeric Month column instead of the name).
4. **Donut chart — Sales Channel distribution:** click **Donut Chart** → drag **Sales Channel** to Legend and **Total Revenue** to Values.
5. **Clustered column chart — Target vs. Actual Sales:** click **Clustered Column Chart** → drag **Region** (or **Sales Executive Name**) to the X-axis, then drag both **Target Sales** and **Actual Sales** into Values — Power BI will show them as two side-by-side columns per category automatically.
6. Place these five visuals in the middle two-thirds of the canvas: column and bar charts side by side in one row, the line chart full-width in the next row, and the donut and Target-vs-Actual clustered column charts side by side in the row after that.

## Step 4 — Add the bottom section

1. Click the **Matrix** visual icon.
2. Drag **Region** to Rows, and **Total Revenue**, **Total Profit**, and **Achievement %** to Values.
3. Place this matrix at the bottom-left of the canvas.
4. Next to it, add a **Text Box** (**Insert → Text Box**) and type 3–4 plain-language insight bullets once you've reviewed your actual numbers (see the README's "Key Insights" section for the categories to cover).

## Step 5 — Add slicers and filters (side panel)

1. Click the **Slicer** visual icon → drag **Region** into it.
2. Repeat for **Product Category**, **Sales Channel**, **Sales Executive Name**, and **Month** — five separate slicer visuals.
3. Stack all five vertically along the left or right edge of the canvas.
4. Optionally add a **Date Slicer** on **Date** so the whole report can be filtered by date range, placed above or below the other slicers.
5. Select all slicer visuals → **Format → Align** and **Distribute Vertically** so they line up cleanly.

## Step 6 — Apply the color theme

- **Corporate blue** (e.g. `#1F4E78`) for card backgrounds, chart axis lines, and neutral structural elements.
- **Green** (e.g. `#2E8B57`) for profit and over-target/achieving performance.
- **Orange/Red** (e.g. `#E67E22` / `#C0392B`) for low performance, under-target results, and negative growth.
- Apply this via **Format pane → Colors** on each visual — set Actual Sales bars to blue and Target Sales bars to a contrasting neutral tone in the Target-vs-Actual chart so the comparison reads clearly at a glance.

## Step 7 — Polish for a premium, recruiter-friendly look

1. **Font:** pick one family (Segoe UI is the Power BI default) and apply it consistently via **Format → Text** on every visual.
2. **Alignment and spacing:** use **Format → Align** and **Distribute** (after multi-selecting visuals) rather than eyeballing positions.
3. **Chart sizing:** keep chart heights consistent within each row.
4. **Icons:** use Power BI's built-in icon sets under **Insert → Icons** for small KPI card accents (e.g. an upward arrow near Growth %), kept small and consistent.
5. **Background:** a light gray or white background reads cleaner than a heavily colored one — save color for the data itself.
6. **Title:** add a report-level title text box above the KPI card row (e.g. "Sales Performance & Revenue Growth Dashboard").

## Step 8 — Test before exporting

1. Click through each slicer (try filtering by one Region, then by one Sales Executive) and confirm every visual updates correctly.
2. Check that KPI cards show sensible totals with no filters applied (should match the `KPI_Summary` sheet in the Excel file).
3. If a visual doesn't respond to slicers, check **Model view** to confirm relationships are correctly set (especially if you added a separate Date table).
