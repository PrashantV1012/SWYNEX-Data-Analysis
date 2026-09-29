# Product Sales Dashboard (Power BI)

An interactive sales dashboard built from 1,500 retail orders (2023 to 2025). It tracks revenue, regional and product performance, discounts and returns, and is designed to answer one question quickly: **where are we making money, and where are we losing it?**

![Dashbord Screenshot:](TASK-3-SWYNEX-Interactive-Dashboard\Screenshot.png)

## Key findings

| Area | Finding |
|---|---|
| Revenue | **$4.38M** net sales from 1,500 orders. 2024 is the strongest full year ($1.77M vs $1.70M in 2023). 2025 is a partial year. |
| Regions | **North** leads (~$968K). **South** is lowest (~$828K). |
| Products | Tablet, Laptop and Printer are level at ~$684K each. **Phone** is the smallest (~$497K). |
| Returns | **24.8%** of orders are returned. Highest: **Chair (28.2%)** and **Laptop (27.4%)**. Lowest: **Desk (21.7%)**. |

Returns are the clearest improvement opportunity: roughly one in four orders comes back.

## Dashboard contents

- **Filters (slicers):** Year, Region, Product, Customer Type, Promotion, Store Location
- **Charts:** monthly net sales trend, net sales by region / product / salesperson / promotion, return rate by product, gross vs net sales by discount level
- **Interactivity:** click any visual to cross-filter the rest of the page

## Repository contents

| File | Description |
|---|---|
| `Dashbord.pbix` | Containes: date table, DAX measures, visual layout |
| `Screenshot.png` | Power BI dashbord screenshot |


## Data notes

- `NetSales` is gross sales after discount. `Returned` is a 0/1 flag; `ReturnedFlag` is the same as text.
- 2025 covers only part of the year, so year-over-year comparisons for 2025 are not like-for-like.

## Tools

Power BI Desktop, DAX, Excel, Python (pandas) for cleaning.

## Author

**Prashant Vishwkarma** · [LinkedIn](https://www.linkedin.com/in/prashantvishwkarma1012/) 