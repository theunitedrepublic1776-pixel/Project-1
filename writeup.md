# AAL Sales Analysis — Q4 2020
## Writeup

**Company:** Australian Apparel Limited (AAL)  
**Dataset:** `AusApparalSales4thQrt2020.csv`  
**Author:** Nicholas D'Angelo  
**Date:** April 2026  

---

## 1. Problem Statement and Objectives

Australian Apparel Limited (AAL) operates across seven Australian states and territories, selling apparel to four distinct demographic groups: Kids, Men, Women, and Seniors. At the end of Q4 2020, management required a data-driven review of quarterly sales performance to guide strategic planning for the following year.

**Business Questions:**
- Which states and demographic groups generate the most revenue?
- When during the day do customers spend the most?
- How do sales evolve week-by-week and month-by-month across Q4?
- Where should the business invest to grow revenue in underperforming regions?

**Objectives:**
1. Clean and prepare the raw sales dataset for analysis.
2. Perform exploratory data analysis (EDA) to identify trends, rankings, and patterns.
3. Visualise findings using professional-quality charts.
4. Produce actionable recommendations for the sales and marketing team.

---

## 2. Data Description and Source

| Property | Detail |
|----------|--------|
| **Source** | Internal AAL transaction system |
| **File** | `AusApparalSales4thQrt2020.csv` |
| **Period** | October – December 2020 (Q4) |
| **Rows** | 7,560 |
| **Columns** | 6 |

### Column Descriptions

| Column | Type | Description |
|--------|------|-------------|
| `Date` | Date (string, `DD-Mon-YYYY`) | Transaction date |
| `Time` | Categorical | Time-of-day slot: Morning, Afternoon, Evening |
| `State` | Categorical | Australian state/territory: NSW, VIC, QLD, SA, WA, NT, TAS |
| `Group` | Categorical | Demographic group: Kids, Men, Women, Seniors |
| `Unit` | Integer | Number of units sold per transaction |
| `Sales` | Float | Revenue (AUD) for that transaction |

---

## 3. Methodology / Approach

### 3.1 Data Cleaning

1. **Column name normalisation** — leading/trailing whitespace was stripped from all column headers and string values.
2. **Date parsing** — the `Date` column was converted from the string format `DD-Mon-YYYY` to a proper `datetime64` type, enabling date arithmetic.
3. **Feature engineering** — three derived time columns were added: `Week` (ISO week number), `Month` (1–12), and `Quarter` (always 4 for this dataset), plus `DayName` for day-of-week analysis.
4. **Missing-value check** — all 7,560 rows across all 6 columns were confirmed non-null (`isna()` count = 0).
5. **Validity check** — zero and negative values for `Unit` and `Sales` were confirmed absent (count = 0).
6. **Conclusion:** The dataset arrived in excellent condition; no imputation or row removal was required.

### 3.2 Normalisation

Min-Max scaling was applied to `Unit` and `Sales`, mapping each to [0, 1]:

$$x_{\text{norm}} = \frac{x - x_{\min}}{x_{\max} - x_{\min}}$$

This was chosen over z-score standardisation because:
- Sales figures are all positive and bounded (no true Gaussian distribution assumption needed).
- Min-Max preserves relative distances and is directly interpretable (0 = minimum, 1 = maximum observed value).
- The normalised columns (`Unit_norm`, `Sales_norm`) are kept for model-readiness but all business metrics are reported using original dollar values.

### 3.3 Analysis Techniques

| Technique | Purpose |
|-----------|---------|
| **GroupBy + agg()** | Aggregate total sales by State, Group, Week, Month, and Time-of-Day |
| **GroupBy + transform()** | Add group-mean sales back as a new row-level column |
| **Descriptive statistics** | Mean, median, mode, std, min, max for Unit and Sales |
| **Pivot tables** | Cross-tabulation of Sales by State × Group and State × Time |
| **Trend analysis** | Daily, weekly, and monthly line/bar charts |
| **Distribution analysis** | Histograms, KDE plots, and box plots for Sales and Unit distributions |

### 3.4 Visualisation Library

**Seaborn** (built on Matplotlib) was selected because:
- It natively integrates with Pandas DataFrames.
- It produces publication-quality statistical charts with minimal code.
- `FacetGrid` / `catplot` enable multi-panel comparisons across states and groups.

---

## 4. Key Findings and Insights

### 4.1 Overall Performance

| Metric | Value |
|--------|-------|
| **Total Q4 Sales** | $340,302,500 |
| **Total Units Sold** | 136,121 |
| **Dataset Coverage** | 7 states × 4 groups × 3 time slots × 92 days |

### 4.2 State Performance

| Rank | State | Total Sales | Share |
|------|-------|-------------|-------|
| 1 | **VIC** | $105,565,000 | 31.0% |
| 2 | **NSW** | $74,970,000 | 22.0% |
| 3 | **SA** | $58,857,500 | 17.3% |
| 4 | **QLD** | $33,417,500 | 9.8% |
| 5 | **TAS** | $22,760,000 | 6.7% |
| 6 | **NT** | $22,580,000 | 6.6% |
| 7 | **WA** | $22,152,500 | 6.5% |

- **VIC** dominates with ~31% of total Q4 revenue, more than double the third-ranked state (SA).
- **WA, NT, and TAS** are the three lowest-performing states, together accounting for only ~19.8% of revenue.

### 4.3 Demographic Group Insights

| Rank | Group | Total Sales | Share |
|------|-------|-------------|-------|
| 1 | **Men** | $85,750,000 | 25.2% |
| 2 | **Women** | $85,442,500 | 25.1% |
| 3 | **Kids** | $85,072,500 | 25.0% |
| 4 | **Seniors** | $84,037,500 | 24.7% |

- Sales are remarkably balanced across all four demographic groups — the spread between highest (Men) and lowest (Seniors) is only ~$1.7 million (~2%).
- This indicates broad market penetration rather than reliance on a single group.

### 4.4 Time-of-Day Insights

- **Morning** is the peak sales period across all states and groups.
- **Evening** is the off-peak period.
- This pattern is consistent across all seven states, suggesting a uniform consumer behaviour profile.

### 4.5 Weekly Trend

- Sales are broadly **stable week-to-week** throughout Q4.
- A slight lift is visible toward the **end of December**, consistent with holiday season spending.
- No major anomalies or outliers were detected in the weekly series.

### 4.6 Monthly Breakdown

| Month | Observation |
|-------|-------------|
| **October** | Solid start to Q4 |
| **November** | Consistent mid-quarter performance |
| **December** | **Strongest month** — driven by end-of-year retail demand |

---

## 5. Conclusions and Recommendations

### 5.1 Conclusions

1. AAL delivered **strong and broadly stable Q4 2020 performance** across all states and groups.
2. **Victoria is the dominant market**, contributing nearly a third of all revenue.
3. Revenue is **evenly split across demographic groups**, indicating healthy brand diversification.
4. **Morning shopping sessions** drive the highest revenue; evening sessions are underutilised.
5. **December outperforms** October and November, confirming the importance of holiday-season readiness.

### 5.2 Recommendations

| Priority | Area | Recommendation |
|----------|------|---------------|
| 🔴 High | **NT & TAS** | Launch targeted promotional campaigns (discount codes, influencer activations, pop-up events) to stimulate demand in the lowest-revenue territories. |
| 🔴 High | **Holiday Prep** | Pre-stock inventory in VIC and NSW ahead of December; initiate early-November marketing activation to sustain momentum through the quarter. |
| 🟡 Medium | **Evening Sales** | Schedule push notifications, email retargeting, and flash sales during evening windows to capture off-peak traffic. |
| 🟡 Medium | **Men's Category** | Invest in dedicated menswear campaigns (e.g., Next Best Offer programmes) to capitalise on Men's #1 ranking and widen the lead. |
| 🟢 Low | **Kids Range Expansion** | Expand the Kids product range in NSW and VIC — long-term brand loyalty investment with strong mid-term revenue upside. |
| 🟢 Low | **WA Growth** | WA ranks last by revenue but shows an opportunity: population-adjusted spend is low, suggesting under-penetration rather than product-market misfit. |

### 5.3 Technology Stack

| Component | Choice | Rationale |
|-----------|--------|-----------|
| Analysis | Pandas + NumPy + SciPy | Industry-standard, well-documented |
| Visualisation | Seaborn on Matplotlib | Statistical focus, polished defaults |
| Normalisation | Min-Max Scaler (scikit-learn) | Positive bounded data; preserves distances |
| Reporting | JupyterLab Notebook | Blends code, prose, and charts; exportable as HTML/PDF |

---

*End of Writeup — AAL Sales Analysis Q4 2020*
