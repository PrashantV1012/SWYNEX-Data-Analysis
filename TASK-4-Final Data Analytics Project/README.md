# Product Sales & Region Analysis — Data Analytics Final Project

## Project Overview
This project analyzes product sales performance across regions, products, salespeople, promotions, customer types, payment methods, returns, discounts, and delivery time.

The objective is to convert raw order-level data into a cleaned analytical dataset, exploratory analysis, a Power BI-style dashboard view, and actionable business insights.

> **Source basis:** The project uses the supplied final project report and the supplied cleaned workbook. The report states that the raw source contained 1,500 orders from January 2023 through June 2025.

## Business Problem
The business sells seven products through five regions, four stores, and six salespeople but lacked a consolidated view of revenue drivers and revenue leakage.

The analysis addresses:
- Which regions, products, and salespeople generate the most net sales?
- How has revenue moved over time?
- How much revenue is reduced through discounts?
- What is the order-level return rate, and how does it vary?
- Are there unusual orders or delivery issues requiring review?

## Dataset Information
- **Rows:** 1,500
- **Columns:** 22 in the cleaned workbook
- **Period:** January 2023 to June 2025
- **Products:** 7
- **Regions:** 5
- **Stores:** 4
- **Salespeople:** 6
- **Customer types:** Retail and Wholesale
- **Discounts:** 0%, 5%, 10%, 15%
- **Promotions:** FREESHIP, SAVE10, WINTER15, and No Promotion
- **Key measures:** Quantity, UnitPrice, GrossSales, NetSales, ShippingCost, DeliveryDays, ReturnedFlag

### Important limitation
The dataset contains **no cost or profit field**, so findings describe sales performance rather than profitability.

## Data Cleaning & Preparation
The supplied report documents the following checks and transformations:

1. Loaded 1,500 raw order rows.
2. Removed **0** full-row duplicates.
3. Removed **0** duplicate OrderIDs.
4. Replaced 370 blank Promotion values with **No Promotion**.
5. Dropped OrderDate because it was identical to Date on every row.
6. Added:
   - `DeliveryDays = DeliveryDate - Date`
   - `GrossSales = Quantity × UnitPrice`
   - `NetSales = GrossSales × (1 - Discount)`
   - `ReturnedFlag` as a readable kept/returned label.
7. Reconciled NetSales with TotalPrice: **0 mismatches**.
8. Final cleaned dataset: **1,500 rows × 22 columns**, with no blanks according to the supplied report.

## Analysis
Methods documented in the supplied report:
- Descriptive statistics
- Grouped summaries
- Monthly time-series aggregation
- Pearson correlation
- 1.5×IQR outlier screening

### Headline metrics
| Metric | Result |
|---|---:|
| Gross sales | $4,727,892.94 |
| Net sales | $4,379,992.43 |
| Discounts given | $347,900.51 |
| Discount as % of gross | 7.4% |
| Orders | 1,500 |
| Units | 15,616 |
| Average net sales/order | $2,919.99 |
| Return rate | 24.8% (372 orders) |
| Average delivery | 6.04 days |

### Key performance findings
- **Region:** North generated the highest net sales at **$967,958**; South generated **$827,768**.
- **Products:** Tablet, Laptop, and Printer were each around **$684K** in net sales.
- **Salesperson:** Bob generated **$796,781**, while Diana generated **$676,568**.
- **Returns:** Overall return rate was **24.8%**. Chair was highest among products at **28.2%**, followed by Laptop at **27.4%**.
- **Discounts:** $347,901 of gross sales was given away through discounts, equal to **7.4% of gross sales**.
- **Discount/returns relationship:** The report found Pearson correlation of **0.007**, effectively zero in this dataset.
- **Promotions:** FREESHIP generated the highest net sales among promotion groups; SAVE10 had the highest return rate at **26.0%**.
- **Outliers:** 17 orders were above the IQR fence of **$9,736.10** and were identified as review candidates rather than errors.
- **Trend:** 2024 net sales were **$1.772M**, versus **$1.698M** in 2023. 2025 contains only January–June and therefore should not be compared directly with full-year totals.

## Dashboard
The supplied report describes a one-page Power BI dashboard with:
- KPI cards for headline net sales and orders
- Monthly net-sales trend
- Net sales by region
- Product ranking/mix
- Salesperson performance
- Promotion contribution
- Sales by discount level
- Product × Region matrix
- Year slicer

A static dashboard snapshot is included as `dashboard_snapshot.png`. The supplied report notes that the interactive `.pbix` should be opened in Power BI Desktop.


## Business Insights & Recommended Actions
1. **Returns are the major leakage area.** Prioritize root-cause review for Chair and Laptop, and for East, West, and South where reported return rates exceed 26%.
2. **Use discount guardrails.** The report recommends testing tighter discount ranges because higher discount depth did not show a meaningful relationship with returns.
3. **Review promotion performance.** FREESHIP generated the most net sales, while SAVE10 had the highest reported return rate.
4. **Investigate unusual orders.** Review the 17 orders above $9,736 for pricing, quantity, and promotion anomalies.
5. **Investigate seasonality.** The report highlights the October 2023 dip and March 2023 peak.
6. **Share sales practices.** Review approaches used by higher-sales salespeople and identify transferable practices.
7. **Add profitability data.** Future versions should include product cost, gross margin, net margin, and return/refund cost so decisions can be based on profit rather than sales alone.

## Limitations
- 2025 covers only the first six months.
- Correlation does not establish causation.
- Return rate is measured at order level, not unit level.
- No profitability data is available.
- Shipping cost cannot be interpreted as profit.
- Findings describe this dataset and should not automatically be generalized beyond it.



## Tools
- Excel — data storage / cleaning validation
- Python / Pandas — analytical validation and dashboard snapshot
- Power BI — interactive dashboard described in the supplied report

## Conclusion
The project turns 1,500 order records into a structured sales-performance view. The most important management themes are **return reduction, disciplined discounting, promotion evaluation, regional/product mix management, and adding margin data for the next analytical iteration**.
