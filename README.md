# Plato's Pizza Sales Performance Dashboard

![Platos pizza Sales Dashboard](Platos_Pizza_Sales_Dashboard.png)

## Project Overview
An executive Power BI analytics dashboard built for Plato's Pizza to evaluate financial performance, identify peak operational bottlenecks, optimize menu strategy, and evaluate restaurant seating capacity utilization. Analyzing historical order records across multiple relational tables, the dashboard translates operational sales data into actionable business strategy.

---

## Key Performance Indicators
* **Total Revenue:** $817.9K
* **Total Orders:** 21K
* **Total Pizzas Sold:** 50K
* **Average Order Value (AOV):** $38.31
* **Busiest Day of the Week:** Friday
* **Busiest Order Hours:** 12:00 PM – 1:00 PM (Lunch) & 5:00 PM – 7:00 PM (Dinner)
* **Top-Selling Item:** The Classic Deluxe Pizza (2.5K units sold)
* **Lowest-Selling Item:** The Brie Carre Pizza (490 units sold)

---

## Workflow & Technical Approach
1. **Relational Data Modeling:** Connected four core relational datasets (`Orders`, `Order Details`, `Pizzas`, and `Pizza Types`) in Power BI using primary/foreign keys (`Order ID`, `Pizza ID`, `Pizza Type ID`) to build a normalized star schema.
2. **Data Cleansing & Time Intelligence (Power Query):** Handled missing values, formatted data types, and engineered custom time-based columns (`Day of Week`, `Order Hour`) from timestamp fields to isolate customer ordering patterns.
3. **DAX Measures & Business Logic:** Formulated measures for `Total Revenue`, `Total Orders`, `Total Pizzas Sold`, and `Average Order Value (AOV)` to evaluate financial throughput across dynamic slicers.
4. **UI/UX Design & Dashboard Layout:** Designed a dark-mode canvas utilizing high-contrast gold/green visual elements for positive performance and red highlights for underperforming menu items.
5. **Operational Analytics:** Incorporated peak-hour line charts, hourly pizza production donut distributions, horizontal bar breakdowns for top/bottom menu items, and seating capacity benchmarks.

---

## Business Insights & Strategic Recommendations
* **Peak Demand & Staffing Optimization:** Ordering volume surges toward late weekdays, peaking on **Friday**, with strong hourly rushes during lunch (12–1 PM) and dinner (5–7 PM). Management should adjust kitchen and front-of-house shift scheduling to match these exact demand spikes.
* **Kitchen Production Pressure:** High pizza volume during peak hours puts severe pressure on kitchen workflows. Pre-prep strategies for high-volume ingredients should be implemented prior to 12:00 PM and 5:00 PM rushes.
* **Menu Engineering & Portfolio Pruning:** **The Classic Deluxe** leads sales at 2,500 units, whereas **The Brie Carre** lags significantly at only 490 units sold. Management should consider recipe re-engineering, targeted promotions, or replacing underperforming menu items.
* **Seating Capacity vs. Table Turnover:** With 15 tables (60-seat capacity), peak-hour order volumes indicate potential seating bottlenecks. Staff should focus on faster table turnover times and promoting takeaway options during lunch/dinner rushes.

---

## Repository Files
* `Platos_Pizza_Sales_Dashboard.png` — High-resolution screenshot of the dashboard interface.
* `PROJECT SUMMARY REPORT.pdf` — Comprehensive executive summary detailing dataset relationships, findings, and operational strategy.
* `Platos Pizza Sales Performance.pbix` — Interactive Power BI workbook file.
