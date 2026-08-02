# Supply Chain Visibility & Optimization - Milestone 3

## Project Overview

This milestone focuses on developing two interactive Power BI dashboards:

- Supplier Performance Dashboard
- Transportation Analytics Dashboard

The objective is to evaluate supplier performance, benchmark suppliers, analyze transportation operations, monitor logistics costs, and support business decision-making using DAX measures, calculated columns, and interactive visualizations.

---

# Dashboard 1: Supplier Performance Dashboard

## Objective

The Supplier Performance Dashboard helps procurement teams evaluate suppliers based on quality, reliability, and lead time. It enables supplier benchmarking, identifies high-performing vendors, and supports strategic sourcing decisions.

---

## Key Performance Indicators (KPIs)

- Total Suppliers
- Average Quality Score
- Average Reliability %

---

# DAX Measures

## Total Suppliers

```DAX
Total Suppliers =
DISTINCTCOUNT ( Dim_supplier[supplier_name] )
```

Counts the total number of unique suppliers.

---

## Average Quality Score

```DAX
Avg Quality Score =
AVERAGE ( Dim_supplier[quality_score] )
```

Calculates the average quality score of all suppliers.

---

## Average Reliability %

```DAX
Avg Reliability % =
AVERAGE ( Dim_supplier[reliability_%] )
```

Calculates the average supplier reliability percentage.

---

# Calculated Columns

## Reliability Tier

```DAX
Reliability Tier =
SWITCH (
    TRUE(),
    Dim_supplier[reliability_%] >= 80, "High",
    Dim_supplier[reliability_%] >= 50, "Medium",
    "Low"
)
```

Classifies suppliers into High, Medium, and Low reliability tiers.

---

## Supplier Composite Score

```DAX
Supplier Composite Score =
( Dim_supplier[quality_score] * 0.4 )
+ ( Dim_supplier[reliability_%] * 0.4 )
+ ( ( 30 - Dim_supplier[lead_time_(days)] ) / 30 * 100 * 0.2 )
```

Calculates the overall supplier performance score using:

- 40% Quality Score
- 40% Reliability
- 20% Lead Time

---

## Supplier Rank

```DAX
Supplier Rank =
RANKX (
    ALL ( Dim_supplier ),
    Dim_supplier[Supplier Composite Score],
    ,
    DESC
)
```

Ranks suppliers based on the Supplier Composite Score.

---

# Supplier Scorecard Calculation Methodology

Each supplier is evaluated using a weighted composite score.

| Performance Metric | Weight |
|--------------------|--------|
| Quality Score | 40% |
| Reliability % | 40% |
| Lead Time | 20% |

The Supplier Composite Score is used to compare supplier performance and benchmark suppliers across the organization.

---

# Supplier Ranking & Benchmarking Approach

Suppliers are classified according to Reliability Tier:

| Reliability % | Tier |
|---------------|------|
| 80% and above | High |
| 50% – 79% | Medium |
| Below 50% | Low |

Supplier Rank is calculated using the Supplier Composite Score, helping identify the best-performing suppliers and those requiring improvement.

---

## Dashboard Visualizations

- KPI Cards
- Supplier Composite Score by Supplier
- Reliability Tier Distribution (Donut Chart)
- Lead Time vs Reliability Scatter Plot
- Quality Score Distribution (Histogram)
- Supplier Details Table
- Supplier Name Slicer
- Product Name Slicer

---

# Dashboard 2: Transportation Analytics Dashboard

## Objective

The Transportation Analytics Dashboard evaluates transportation costs, shipping performance, carrier efficiency, profitability, and discount trends to improve logistics operations.

---

## Key Performance Indicators (KPIs)

- Total Orders
- Average Profit Per Order
- Total Discount Given
- Average Discount Rate
- Same Day Share %

---

# DAX Measures

## Average Profit Per Order

```DAX
Avg Profit Per Order =
AVERAGE ( Fact_table[order_profit_per_order] )
```

Calculates the average profit generated per order.

---

## Total Discount Given

```DAX
Total Discount Given =
SUM ( Fact_table[order_item_discount] )
```

Calculates the total discount offered across all orders.

---

## Average Discount Rate

```DAX
Avg Discount Rate =
AVERAGE ( Fact_table[order_item_discount_rate] )
```

Calculates the average discount percentage applied to orders.

---

## Same Day Share %

```DAX
Same Day Share % =
DIVIDE (
    CALCULATE (
        DISTINCTCOUNT ( Fact_table[order_id] ),
        Fact_table[shipping_mode] = "Same Day"
    ),
    [Total Orders],
    0
)
```

Calculates the percentage of orders delivered through Same Day shipping.

---

# Transportation Cost Analysis Methodology

The dashboard analyzes logistics performance by monitoring:

- Profit generated from transportation
- Discount provided on orders
- Average discount rate
- Same Day shipment percentage
- Overall transportation efficiency

These metrics help evaluate operational performance and optimize transportation decisions.

---

# Route & Carrier Performance Evaluation

The Transportation Dashboard helps compare:

- Shipping performance
- Transportation efficiency
- Profitability
- Discount trends
- Same Day delivery share

These insights help businesses optimize logistics operations and improve customer service.

---

# Business Insights

## Supplier Performance Dashboard

- Identifies high-performing suppliers.
- Detects suppliers with poor reliability.
- Compares supplier quality scores.
- Benchmarks suppliers using a weighted score.
- Supports better supplier selection.
- Monitors supplier performance through interactive KPIs.

---

## Transportation Analytics Dashboard

- Evaluates transportation profitability.
- Monitors total discounts offered.
- Measures average discount rates.
- Tracks Same Day shipment percentage.
- Helps improve logistics efficiency.

---

# Business Recommendations

## Supplier Performance

- Prioritize High Tier suppliers for procurement.
- Improve collaboration with Medium Tier suppliers.
- Replace or improve Low Tier suppliers.
- Reduce supplier lead times.
- Continuously monitor supplier quality and reliability.

---

## Transportation Analytics

- Reduce excessive discounts where possible.
- Increase profitability through optimized shipping strategies.
- Improve Same Day delivery performance.
- Monitor transportation KPIs regularly.
- Optimize logistics operations using data-driven decisions.

---

# Tools & Technologies

- Power BI Desktop
- DAX
- Power Query
- Data Modeling

-
---

# Conclusion

This milestone demonstrates how Power BI can be used to evaluate supplier performance and transportation analytics through interactive dashboards. The implemented DAX measures, calculated columns, and visualizations provide valuable business insights that support supplier benchmarking, procurement planning, logistics optimization, and informed decision-making.
