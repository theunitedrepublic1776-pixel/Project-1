# Screenshots — AAL Sales Analysis Q4 2020

This folder contains all screenshots referenced in the project writeup.  
Screenshots are organised into three categories: **Code Snippets**, **Visualisations**, and **Output/Results**.

---

## Code Snippets

| File | Description |
|------|-------------|
| [`snippet_01_data_loading.png`](snippet_01_data_loading.png) | Library imports and loading the raw CSV with `pd.read_csv()` |
| [`snippet_02_data_cleaning.png`](snippet_02_data_cleaning.png) | Column whitespace stripping, date parsing, feature engineering, and missing-value checks |
| [`snippet_03_normalisation.png`](snippet_03_normalisation.png) | Min-Max normalisation of `Unit` and `Sales` using `sklearn.preprocessing.MinMaxScaler` |
| [`snippet_04_groupby_analysis.png`](snippet_04_groupby_analysis.png) | GroupBy aggregations for group/state rankings and weekly reporting |
| [`snippet_05_summary_stats.png`](snippet_05_summary_stats.png) | Descriptive statistics (`mean`, `median`, `std`, `min`, `max`, `mode`) and headline KPIs |

---

## Visualisations

| File | Description |
|------|-------------|
| [`fig_01.png`](fig_01.png) | **Box plots** — Distribution of Units Sold and Sales by demographic group |
| [`fig_02.png`](fig_02.png) | **Grouped bar chart** — State-wise total sales broken down by demographic group |
| [`fig_03.png`](fig_03.png) | **Faceted bar charts** — Group-wise sales comparison across all 7 states |
| [`fig_04.png`](fig_04.png) | **Time-of-day bar charts** — Overall sales and state-level sales by Morning / Afternoon / Evening |
| [`fig_05.png`](fig_05.png) | **Daily sales trend line** — Total sales per day across October–December 2020 (with shaded area) |
| [`fig_06.png`](fig_06.png) | **Weekly sales bar chart** — Total sales per ISO week number |
| [`fig_07.png`](fig_07.png) | **Monthly sales comparison** — Total sales and average transaction value per month |
| [`fig_08.png`](fig_08.png) | **Quarterly overview** — Pie chart of state share + grouped bar chart by state (Q4) |
| [`fig_09.png`](fig_09.png) | **Heatmap (State × Group)** — Total sales in AUD millions per state and demographic group |
| [`fig_10.png`](fig_10.png) | **Sales distribution** — Histogram with KDE overlay for Sales; box plot for Units |
| [`fig_11.png`](fig_11.png) | **KDE by group** — Overlapping kernel density plots showing Sales distribution per demographic group |
| [`fig_12.png`](fig_12.png) | **Heatmap (State × Time-of-Day)** — Total sales in AUD millions per state and time slot |

---

## Output / Results

| File | Description |
|------|-------------|
| [`output_01_sales_tables.png`](output_01_sales_tables.png) | Summary tables: Total sales ranked by State and by Demographic Group |
| [`output_02_summary_metrics.png`](output_02_summary_metrics.png) | Key Q4 2020 KPI card: total sales, total units, top state, top group, peak time, dataset shape |

---

## Quick Reference — Key Numbers

| Metric | Value |
|--------|-------|
| Total Q4 Sales | $340,302,500 |
| Total Units Sold | 136,121 |
| Top-Revenue State | VIC ($105,565,000 — 31.0%) |
| Bottom-Revenue State | WA ($22,152,500 — 6.5%) |
| Top-Revenue Group | Men ($85,750,000 — 25.2%) |
| Bottom-Revenue Group | Seniors ($84,037,500 — 24.7%) |
| Peak Time-of-Day | Morning |
| Strongest Month | December |
