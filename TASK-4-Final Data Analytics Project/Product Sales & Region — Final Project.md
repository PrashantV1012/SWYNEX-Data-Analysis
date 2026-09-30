Data Analytics Final Project

# Product Sales & Region Analysis

1,500 orders · Jan 2023 – Jun 2025 · Excel cleaning, Python EDA, Power BI dashboard

[Problem](#p)[Data](#d)[Cleaning](#c)[Analysis](#a)[Dashboard](#db)[Insights](#i)

**$4.38M**Net sales

**1,500**Orders

**15,616**Units sold

**$2,920**Avg net / order

**24.8%**Return rate

**6.04 d**Avg delivery

## 1. Problem statement

The business sells seven products through five regions, four stores and six salespeople, but has no consolidated view of what drives revenue and where it leaks. This project cleans the raw order data, analyses it, and delivers an interactive dashboard to answer:

- Which regions, products and salespeople generate the most net sales, and how has revenue moved over time?
- How much revenue is given away through discounts and promotions?
- What is the return rate, and does it vary by product, region or discount depth?
- Are there unusual orders or delivery issues that need operational review?

## 2. Dataset information

Source: `Product-Sales-Region-Raw-Data.xlsx` (one sheet, 1,500 rows × 19 columns). Each row is one order.

| Group | Columns |
| --- | --- |
| Order | OrderID, Date, OrderDate, DeliveryDate, CustomerName, CustomerType (Retail / Wholesale) |
| Geography & people | Region (5), StoreLocation (4), RegionManager, Salesperson (6) |
| Product & price | Product (7), Quantity, UnitPrice, Discount (0/5/10/15%), TotalPrice, ShippingCost |
| Commercial | PaymentMethod (5), Promotion (FREESHIP, SAVE10, WINTER15), Returned (0/1) |

No profit or cost field exists, so all results are about sales, not margin.

## 3. Data cleaning process

Raw and cleaned files were compared; every step below was verified against the data (1,500 rows in, 1,500 rows out).

| Step | Issue found | Action |
| --- | --- | --- |
| Integrity checks | No duplicate rows or OrderIDs; no missing values except Promotion | No rows removed |
| Missing promotion | 370 orders (24.7%) had a blank Promotion | Labelled “No Promotion” so they appear in analysis |
| Redundant column | `OrderDate` is identical to `Date` on every row | Dropped |
| Delivery time | Only start and end dates available | Added `DeliveryDays` = DeliveryDate − Date (range 2–10 days) |
| Sales measures | Only TotalPrice (already after discount) | Added `GrossSales` = Quantity × UnitPrice and `NetSales` = GrossSales × (1 − Discount); NetSales matches TotalPrice exactly |
| Return label | Returned stored as 0/1 | Added `ReturnedFlag` (Kept / Returned) for readable visuals |
| Types & headers | Dates and numbers needed consistent typing | Dates as dates, numeric fields as numbers, descriptive column names |

Result: `Product-Sales-Region-cleaned-Data.xlsx`, sheet “Sales”, 1,500 rows × 22 columns, no blanks.

## 4. Analysis

**Methods:** descriptive statistics, grouped summaries, time-series aggregation, Pearson correlation and 1.5×IQR outlier screening.

### Net sales by region

North

**$968k**

East

**$884k**

West

**$853k**

Central

**$847k**

South

**$828k**

### Net sales by product

Tablet

**$685k**

Laptop

**$684k**

Printer

**$684k**

Monitor

**$652k**

Chair

**$623k**

Desk

**$555k**

Phone

**$497k**

### Return rate by product

Chair

**28.2%**

Laptop

**27.4%**

Monitor

**26.4%**

Tablet

**24.2%**

Phone

**23.1%**

Printer

**22.3%**

Desk

**21.7%**

### Return rate by discount band

0%

**25.4%**

1–5%

**23.4%**

6–10%

**24.3%**

11–15%

**26.1%**

### Monthly net sales (Jan 2023 – Jun 2025)

Peak: Mar 2023 ($208.5k). Low: Oct 2023 ($78.4k).

### Regional detail

| Region | Orders | Net sales | Return rate | Avg delivery |
| --- | --- | --- | --- | --- |
| North | 309 | $967,958 | 22.7% | 6.39 d |
| East | 311 | $883,634 | 26.0% | 6.00 d |
| West | 284 | $853,479 | 26.1% | 6.01 d |
| Central | 301 | $847,154 | 23.3% | 5.88 d |
| South | 295 | $827,768 | 26.1% | 5.93 d |

### Yearly trend

| Year | Orders | Net sales | Avg order |
| --- | --- | --- | --- |
| 2023 | 579 | $1,697,870 | $2,932 |
| 2024 | 584 | $1,771,955 | $3,034 |
| 2025 (Jan–Jun) | 337 | $910,168 | $2,701 |

### Other findings

- **Discounts:** $347,901 (7.4% of gross sales). Correlation with returns is 0.007 — effectively none.
- **Order value is right-skewed:** mean $2,920 vs median $2,175. 17 orders exceed the IQR fence of $9,736 and should be reviewed.
- **Promotions:** FREESHIP is the largest ($1.24M, 24% returns); SAVE10 has the highest return rate (26.0%). Retail and Wholesale are almost equal in net sales ($2.20M vs $2.18M).
- **Salespeople:** Bob ($797k) and Alice ($786k) lead; Diana is lowest ($677k).
- Quantity (r = 0.67) and unit price (r = 0.68) track net sales mechanically; delivery time does not.

## 5. Dashboard (Power BI)

`Dashboard.pbix` is a one-page interactive report built on the cleaned data. It contains:

| Visual | Question answered |
| --- | --- |
| KPI card | Headline totals |
| Line chart (Year / Month) | Sales trend and seasonality |
| Column chart by Region | Where revenue is concentrated |
| Bar and column charts by Product | Product ranking and mix |
| Bar chart by Salesperson | Individual performance |
| Column chart by Promotion | Which campaigns drive sales |
| Bar chart by Discount | Sales at each discount level |
| Matrix (Product × Region) | Cross-view of where each product sells |
| Year slicer | Filters every visual at once |

The .pbix is a desktop file and can’t be embedded here; open it in Power BI Desktop. The charts above reproduce its main views.

## 6. Key business insights & recommendations

### Revenue is broad, not concentrated

North leads with $968k, but the gap to South is only $140k. Growth comes from lifting every region, not rescuing one.

### Three products carry the mix

Tablet, Laptop and Printer each earn about $684k. Phone is the weakest ($497k) and Desk is second lowest ($555k): candidates for promotion or range review.

### Returns are the biggest leak

1 in 4 orders is returned. Chair (28.2%) and Laptop (27.4%) are worst; East, West and South sit above 26%. Investigate quality and fulfilment there first.

### Deeper discounts don’t buy loyalty

Discounts cost $348k and show no link to return behaviour. Since deeper discounts don’t obviously lift sales, test tighter discount caps.

### Momentum is flat

2024 grew 4.4% over 2023. H1 2025 ($910k) is essentially level with H1 2024 ($912k) and H1 2023 ($903k), and its average order fell to $2,701. Watch order value.

### Large orders need review

17 unusually large orders can swing totals. Check pricing, quantity and promotion records before relying on averages.

### Recommended actions

1. Launch a returns root-cause review for Chair, Laptop and the East / West / South regions.
2. Set discount guardrails and A/B test 0–5% versus 11–15% offers.
3. Investigate the Oct 2023 dip and build seasonal planning around the Mar peak.
4. Share practices from top salespeople (Bob, Alice) with the lower-performing team.
5. Add cost and margin data so the next iteration can measure profit, not just sales.

### Limitations

2025 is a half year. Correlations are not causal. Return rate is order-level. No profitability data. Findings describe this dataset only.