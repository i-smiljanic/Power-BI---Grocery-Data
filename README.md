# Grocery Sales Performance – Power BI

A one-page, interactive Power BI dashboard that analyzes sales performance of a grocery retail chain: what sells, where it sells, and how outlet size, location and type relate to sales, ratings and item visibility.

**Tools:** Power BI · DAX · Power Query · Field parameters
**Data:** 8,523 item sales records from 10 outlets (`Grocery Data.xlsx`, sheet "BlinkIT Grocery Data", 12 columns) – [TODO: add data source / link]

## Business questions

1. How much do we sell in total, and what does the average item sale and rating look like?
2. Which item types and fat-content groups drive sales?
3. How do outlet location tier, size and type compare?
4. Do outlets differ in item visibility, ratings or average sales?

## Dashboard

KPI cards (total sales, average sales, number of items, average rating), a filter panel (outlet location type, outlet size, item type) with a *Clear all filters* button, and a measure switch (Total Sales / Average Sales / Number of Items / Average Rating) that changes the fat-content and item-type charts. Further visuals show sales by outlet establishment year, outlet size, outlet location tier and a comparison table by outlet type.

![Dashboard](images/01_dashboard.png)

## Key findings

All figures were recomputed from the raw Excel file and match the dashboard.

- **Overall:** **$1.20M** in sales across **8,523** item records, an average of **$140.99** per record and an average rating of **3.97**.
- **Fat content:** low-fat items generate **64.6%** of sales ($776.3K) and regular items 35.4% ($425.4K).
- **Item types:** Fruits and Vegetables ($178.1K, 14.8%) and Snack Foods ($175.4K, 14.6%) lead; the top five types (adding Household, Frozen Foods and Dairy) make up about **59%** of sales.
- **Location:** Tier 3 outlets sell the most (**$472.1K, 39.3%**), followed by Tier 2 ($393.2K) and Tier 1 ($336.4K).
- **Outlet type:** Supermarket Type 1 accounts for **65.5%** of sales, but it also covers 6 of the 10 outlets: about **$131K per outlet**, the same as the single Type 2 and Type 3 outlets ($131.5K and $130.7K). The two Grocery Stores sell about $76K each.
- **Averages barely differ between segments:** average sales per record stay between $139.8 and $143.1 and ratings between 3.95 and 3.99 across outlet types, sizes and tiers, so differences in total sales come from the **number of items sold**, not from price or satisfaction.
- **Visibility:** Grocery Stores show higher item visibility (**0.105**) than supermarkets (about 0.06).

## Data notes and limitations

- Fat-content labels were inconsistent (`LF`, `low fat`, `reg`) and were standardized to *Low Fat* and *Regular* in Power Query (545 records).
- Ratings contain decimals (4,376 of 8,523 ratings are not whole numbers) and are imported as decimals, which gives an average of 3.97.
- **Outlet Size is not consistent per outlet:** outlets OUT010, OUT017 and OUT045 each appear with three different sizes, so the outlet-size breakdown should be read with caution.
- The "Outlet Establishment" chart shows sales by the year an outlet opened, not a time series. The 2018 peak reflects two outlets opened that year, and 2011 is low because that year only has one small Grocery Store.
- Item Weight is missing for 1,463 records (17.2%); it is not used in the dashboard.
- The data is a single snapshot with no sales dates, so no trend over time can be shown.

## Data model and key measures

**Model:** a single flat table, `Grocery Data` (8,523 rows), loaded from Excel in Power Query, and a `Metrics` field parameter that lets the user switch the measure shown in the visuals.

**Power Query steps:** promoted headers, set column types, standardized fat-content labels, and set number columns with an explicit `en-US` locale.

**Key measures (DAX):**

```DAX
Total Sales = SUM('Grocery Data'[Sales])

Average Sales = AVERAGE('Grocery Data'[Sales])

Average Rating = AVERAGE('Grocery Data'[Rating])

Number of Items = COUNTROWS('Grocery Data')
```

The `Metrics` field parameter maps the labels *Total Sales*, *Average Sales*, *Number of Items* and *Average Rating* to these four measures.

## How to open

1. Download `GroceryData.pbix` and `Grocery Data.xlsx` from this repository.
2. Open the `.pbix` in Power BI Desktop and, if prompted, point the data source to your local copy of the Excel file.
