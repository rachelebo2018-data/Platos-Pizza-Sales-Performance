# Plato's Pizza Sales & Operations Performance Dashboard

## Project Overview
Before building the dashboard, the primary goal was simple: Mario, the owner of Plato's Pizza Restaurant, wanted to understand overall business performance, identify when customers buy the most, and determine which pizza products drive sales.

This project transforms historical transactional order logs into a structured Power BI dashboard. It delivers actionable business intelligence to guide staff scheduling, manage kitchen capacity, and optimize menu engineering.

## Dashboard Preview
![Plato's Pizza Dashboard](Platos_pizza_Sales_Dashboard.png)

---

## Skills Demonstrated
* **Data Preparation & ETL:** Cleaned and preprocessed transactional records in Microsoft Excel before refining transformations in Power Query Editor.
* **Data Modeling:** Built a 1-to-Many Star Schema model connecting fact table records with dimension lookup tables.
* **DAX Calculations:** Developed key performance measures using `SUM`, `SUMX`, `RELATED`, `DIVIDE`, and `DISTINCTCOUNT`.
* **Data Visualization & Business Storytelling:** Designed a structured executive layout in dark blue featuring KPI cards, horizontal bar charts, line graphs, and donut charts to analyze order traffic and hourly production volume.

---

## Tools Used
* **Microsoft Excel:** Initial data inspection, early cleaning, and dataset structuring.
* **Power Query Editor (Power BI):** Data cleaning, handling missing values, removing invalid records, validating data types, and creating custom time-based columns (day of week, hour of day).
* **Power BI Desktop:** Data modeling, DAX measure development, dynamic visual report building, and dashboard layout design.
* **GitHub:** Version control and technical portfolio documentation.

---

## Business Problem & Context
Plato's Pizza operates with **15 tables providing a total seating capacity of 60 seats**. While the dataset does not directly track dine-in seating, high order volumes during rush periods suggest seating capacity comes under severe pressure. Management lacked clear visibility into peak operational hours and product demand needed to balance kitchen throughput, table turnover, and menu management.

---

## Business Objectives
* Track core business health metrics: Total Revenue, Total Orders, Total Pizzas Sold, and Average Order Value.
* Identify demand patterns across days of the week and hours of the day to optimize shift planning.
* Analyze kitchen output by calculating the volume of pizzas produced during peak operational hours.
* Pinpoint the top 5 best-selling pizzas driving revenue and bottom 5 worst-selling pizzas to guide menu adjustments.
* Evaluate estimated seating capacity pressure during peak customer periods.

---

## Data Architecture & Modeling
The report is powered by a **Star Schema** data model, connecting four datasets (`orders`, `order_details`, `pizzas`, and `pizza_types`) via 1-to-many (`1:*`) single-direction relationships:

![Pizza Star Schema](Pizza_star_schema.png)

* **Fact Table:** `order_details` (`Order Details ID`, `Order ID`, `Pizza ID`, `Quantity`)
* **Dimension Tables:**
  * `orders` (`Order ID`, `Order date`, `Order day name`, `Order Hour`)
  * `pizzas` (`Pizza ID`, `Pizza Type ID`, `Price`, `Size`)
  * `pizza_types` (`Pizza Type ID`, `Pizza Name`, `Category`)
  * `Date Table` (`Date`, `Day`, `Day of Week`, `Month`, `Month no`, `Quarter`, `Year`)

---

## Key DAX Measures

```dax
1. Total Pizzas Sold: Calculates the overall volume of pizzas sold across all completed customer transactions by aggregating line-item quantities.
DAX: Total Pizzas Sold = SUM(order_details[Quantity])

2. Total Sales Revenue: Computes the total gross business earnings by multiplying ordered quantities by individual unit prices across related lookup tables.
DAX: Total Revenue = SUMX(order_details, order_details[Quantity] * RELATED(pizzas[Price]))

3. Total Unique Orders:  Counts the total number of distinct customer transactions placed, eliminating duplicate line items per order ID.
DAX: Total Orders = DISTINCTCOUNT(orders[Order ID])

4. Average Order Value: Determines the average monetary value generated per individual transaction using a safe division formula to handle zero-denominator exceptions
DAX: Average order value = DIVIDE([Total Revenue], [Total Orders])
```
# Analysis & Key Insights

## 1. KPI Overview – Business Health
* **Total Revenue:** $817.9K ($817,900)
* **Total Orders:** 21K (~21,000 orders)
* **Total Pizzas Sold:** 50K (~50,000 pizzas)
* **Average Order Value:** $38.31
* **Takeaway:** The figures demonstrate that Plato's Pizza operates on a solid revenue foundation with consistent customer spending across orders.

## 2. Demand Patterns by Day & Hour
* **Busiest Days of the Week:** Customer activity increases toward the end of the week. Friday leads total orders, followed by Thursday and Saturday, indicating that weekends drive higher traffic.
* **Busiest Hours of the Day:** Two major operational spikes occur during midday lunch (12:00 PM – 1:00 PM) and early evening dinner (5:00 PM – 6:00 PM). Hour 12 accounts for 13.67% and Hour 13 accounts for 12.94% of hourly order distribution.

## 3. Kitchen Output & Seating Capacity Insights
* **Pizza Production by Hour:** Peak hours show a dramatic spike in total pizzas produced, confirming these windows place maximum operational pressure on kitchen staff.
* **Seating Capacity Constraint:** With only 15 tables (60 seats), high order volumes during rush hours require faster table turnover or reliance on takeaway orders to sustain volume without degrading customer experience.

## 4. Product Performance & Revenue Concentration

### Volume & Sales Distribution
* **Peak Volume Concentration:** During the 4 major peak operational hours, Plato's Pizza produced ~24,000 pizzas, accounting for nearly **48% of total annual production**.
* **Pareto Revenue Contribution:** The Top 5 best-selling pizza categories generate approximately **24.19% of total revenue**, whereas the Bottom 5 worst-selling pizzas contribute a combined **8.54%**.

### Best-Selling Menu Performers (Top 5)
1. **The Classic Deluxe** (2,453 units sold) – Drives primary volume due to broad consumer appeal and consistent order frequency across lunch and dinner shifts.
2. **The Barbecue Chicken** (2,432 units sold) – High revenue contributor leveraging premium chicken pricing and strong dinner-shift demand.
3. **The Hawaiian** (2,422 units sold) – Consistent core performer providing steady baseline sales.
4. **The Pepperoni** (2,418 units sold) – Essential staple item maintaining predictable sales velocity across both weekdays and weekends.
5. **The Thai Chicken** (2,371 units sold) – Strong specialty item that expands basket sizes and supports higher Average Order Values (AOV).

### Underperforming Menu Items (Bottom 5)
1. **The Brie Carre** (480 units sold) – Severe outlier, underperforming all other menu items by over 450 units, indicating extremely low consumer adoption and high risk of perishable inventory spoilage.
2. **The Mediterranean** (934 units sold) – Low sales velocity suggests poor menu placement or niche ingredient appeal.
3. **The Calabrese** (937 units sold) – Underperforms core classic offerings, tying up raw ingredient prep time.
4. **The Spinach Supreme** (950 units sold) – Low turnover rate; requires promotion or recipe adjustment to justify ingredient storage costs.
5. **The Soppressata** (961 units sold) – Minimal contribution to overall sales volume.

### Strategic Inventory & Revenue Takeaway
A small, core group of pizzas generates the vast majority of business returns. The bottom-tier items exhibit slow inventory turnover, which inflates holding costs and creates raw ingredient waste without meaningfully contributing to total revenue.

---

## Strategic Recommendations
1. **Optimize Staff Scheduling:** Increase kitchen and service staff during midday lunch (12–1 PM) and evening dinner (5–6 PM) shifts to manage kitchen production stress and maintain fast table turnover.
2. **Promote Best-Sellers & Re-evaluate Menu:** Continue promoting top performers like The Classic Deluxe and Barbecue Chicken. Re-evaluate lowest-selling items—particularly **The Brie Carre** (under 500 units sold)—through recipe adjustments, targeted promotions, or potential removal to reduce raw inventory waste.
3. **Manage Seating & Order Flow:** Implement strategies during busy hours to encourage faster table turnover and streamline takeaway ordering processes to accommodate demand beyond the 60-seat physical capacity.

---

## Conclusion
This project demonstrates how raw transactional data can be transformed into actionable business intelligence using Power BI. By addressing peak-hour kitchen stress, optimizing seating turnover, and refining underperforming menu items, Mario can improve operational efficiency and drive sustainable business growth.

---

## How to Reproduce This Project
1. Clone or download this repository to your local machine.
2. Ensure `Pizza_star_schema.png` and `Platos_pizza_Sales_Dashboard.png` reside in the root repository directory.
3. Open the `.pbix` file in **Power BI Desktop**.
4. Verify local data source connections to refresh reports.

---

## Author
**Ebo Rachel Adebimpe**  
*Data Analyst *  
