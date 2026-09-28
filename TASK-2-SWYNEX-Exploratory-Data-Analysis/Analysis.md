# Product Sales & Region — Exploratory Analysis

## Dataset and method

- Source: `Product-Sales-Region-cleaned-Data.xlsx`
- Rows analyzed: **1,500**
- Date range: **2023-01-01 to 2025-06-30**
- Analysis methods: descriptive statistics, grouped summaries, time-series aggregation, Pearson correlations, and 1.5×IQR anomaly screening.
- A duplicated header row in the worksheet was removed before analysis.
- The columns `Column1`, `Column2`, and `Column3` were interpreted from the embedded header as DeliveryDays, GrossSales, and NetSales respectively. Internal consistency checks showed these fields reconcile with the source calculations.

## Key statistics

| Metric | Value |
|---|---:|
| Transactions | 1,500 |
| Gross sales | $4,727,892.94 |
| Net sales | $4,379,992.43 |
| Units sold | 15,616 |
| Average net sales/order | $2,919.99 |
| Median net sales/order | $2,174.72 |
| Return rate | 24.8% |
| Average discount | 7.3% |
| Average delivery time | 6.04 days |

## Charts

### Monthly net sales
![Monthly Net Sales](sales_analysis/monthly_net_sales.png)

### Net sales by region
![Net Sales by Region](sales_analysis/region_net_sales.png)

### Net sales by product
![Net Sales by Product](sales_analysis/product_net_sales.png)

### Return rate by discount band
![Return Rate by Discount Band](sales_analysis/return_by_discount.png)

### Quantity versus net sales
![Quantity vs Net Sales](sales_analysis/quantity_vs_net_sales.png)

## Useful insights

1. **Scale and revenue:** The dataset contains 1,500 transactions from 2023-01-01 to 2025-06-30. Gross sales total $4,727,892.94; net sales total $4,379,992.43. Discounts account for $347,900.51, or 7.4% of gross sales.
2. **Regional concentration:** North generates $967,957.98 in net sales, the highest of the five regions. The spread between North and South is $140,189.79.
3. **Product mix:** Tablet, Laptop, and Printer are the three largest products by net sales, each contributing roughly $684,539–$684,387. Chair has the highest product return rate at 28.2%.
4. **Returns:** Overall return rate is 24.8% (372 returned orders). Return rates vary materially by month; the highest monthly rate is 38.9%.
5. **Discounts and returns:** Discount percentage and return status have a near-zero linear correlation (0.007), so the dataset does not show a simple linear relationship between discount depth and returns. The 11–15% discount band has a 26.1% return rate versus 23.4% for 1–5%. This is descriptive, not causal.
6. **Order economics:** Average net sales per order are $2,919.99, while the median is $2,174.72; the gap indicates a right-skewed order-value distribution with some large orders.
7. **Time pattern:** 2024 has the highest annual net sales ($1,771,954.78) and the highest average order value ($3,034.17). 2025 covers only January–June, so its annual total should not be compared directly with full-year totals.
8. **Operational consistency:** Average delivery time is 6.04 days. Delivery time is not strongly correlated with net sales in this dataset, suggesting order size and price are more directly associated with sales value than delivery duration.
9. **Anomalies:** Using the 1.5×IQR rule on net sales, 17 orders are unusually high-value (above $9,736.10). These are not necessarily errors; they are candidates for business review because they can materially affect averages and totals.
10. **Volume drivers:** Quantity and net sales have a correlation of 0.666, while unit price and net sales correlate at 0.677. Both are mechanically related to transaction value, so these correlations describe sales construction rather than causal effects.

## Regional detail

| Region | Orders | Net sales | Return rate | Avg delivery |
|---|---:|---:|---:|---:|
| North | 309 | $967,957.98 | 22.7% | 6.39 days |
| East | 311 | $883,633.72 | 26.0% | 6.00 days |
| West | 284 | $853,478.86 | 26.1% | 6.01 days |
| Central | 301 | $847,153.68 | 23.3% | 5.88 days |
| South | 295 | $827,768.19 | 26.1% | 5.93 days |

## Product detail

| Product | Orders | Net sales | Return rate | Units |
|---|---:|---:|---:|---:|
| Tablet | 240 | $684,539.39 | 24.2% | 2,577 |
| Laptop | 226 | $684,417.24 | 27.4% | 2,408 |
| Printer | 211 | $684,387.42 | 22.3% | 2,336 |
| Monitor | 212 | $651,629.39 | 26.4% | 2,177 |
| Chair | 209 | $622,589.48 | 28.2% | 2,122 |
| Desk | 207 | $555,266.66 | 21.7% | 2,026 |
| Phone | 195 | $497,162.85 | 23.1% | 1,970 |

## Anomaly review

The IQR rule flags **17** unusually high net-sales orders. The highest-value orders should be checked against order quantity, pricing, promotions, and fulfillment records before being treated as errors. This screening is intended to prioritize review, not to label transactions as incorrect.

## Caveats

- The dataset ends in June 2025, so 2025 is a partial year.
- Correlation does not establish causation.
- Return rate is an order-level measure; it is not a unit-level return rate.
- No profitability field is available, so net sales less shipping cost is not presented as true profit.
