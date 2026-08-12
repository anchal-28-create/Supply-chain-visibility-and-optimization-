# Supply Chain Visibility & Optimization Dashboard

## Project Overview

This project presents an interactive Power BI dashboard developed to analyze and optimize supply chain operations. The dashboard provides real-time insights into inventory, warehouse utilization, supplier performance, and order fulfillment, enabling better business decisions through data-driven analysis.

## Objectives

* Monitor inventory levels and warehouse capacity.
* Track supplier and warehouse performance.
* Analyze order fulfillment and stock movement.
* Identify slow-moving and dead stock.
* Improve supply chain visibility through interactive dashboards.

## Tools & Technologies

* Power BI
* Power Query
* DAX

## Dashboard Features

### Executive Dashboard

* Total Orders
* Total Warehouses
* Total Suppliers
* Inventory Value
* Warehouse Capacity Utilization
* Supplier Distribution
* Inventory Value by Category
* Regional Performance Analysis

### Warehouse Efficiency Dashboard

* Warehouse Capacity Usage
* Inventory Turnover
* Stock Status Analysis
* Dead Stock Monitoring
* Slow-Moving Inventory
* Reorder Recommendations
* Regional Inventory Trends

## Key KPIs

* Total Orders
* Total Warehouses
* Total Suppliers
* Total Inventory Value
* Warehouse Capacity Used %
* Inventory Turnover Ratio
* Dead Stock Count
* Reorder Quantity Suggested

## DAX Measures Used

Some of the key DAX measures implemented include:

*## Key DAX Measures

### Warehouse Analytics

```DAX
Total Warehouses =
DISTINCTCOUNT(Fact_table[warehouse_name])
```

```DAX
Max Utilization % =
MAXX(
    VALUES(Fact_table[warehouse_name]),
    CALCULATE(AVERAGE(Fact_table[utilization_%]))
)
```

```DAX
Min Utilization % =
MINX(
    VALUES(Fact_table[warehouse_name]),
    CALCULATE(AVERAGE(Fact_table[utilization_%]))
)
```

```DAX
Dead Stock Quantity =
SUMX(
    FILTER(
        VALUES(Fact_table[product_name]),
        CALCULATE(MAX(Fact_table[Stock Status])) = "Dead Stock"
    ),
    CALCULATE(AVERAGE(Fact_table[stock_qty]))
)
```

---

### Delivery Performance

```DAX
Late Orders =
CALCULATE(
    DISTINCTCOUNT(Fact_table[order_id]),
    Fact_table[delivery_status] = "Late delivery"
)
```

```DAX
Late Delivery % =
DIVIDE([Late Orders],[Total Orders],0)
```

```DAX
Late Delivery % Target = 0.2
```

---

### Warehouse Utilization KPI

```DAX
Warehouse Utilization Target = 80
```

Average Utilization (%) is displayed using a Gauge visual with a maximum value of **100%**.

---

### Supplier Performance

Supplier Reliability (%) is displayed using the average reliability score from the Supplier dimension table.

---

### Inventory KPIs

```DAX
Total Inventory Value =
SUMX(
    VALUES(Fact_table[product_name]),
    CALCULATE(AVERAGE(Fact_table[inventory_value]))
)
```

```DAX
Inventory Turnover Ratio =
DIVIDE([Total Sales],[Total Inventory Value],0)
```

---


## Business Insights

* Identified warehouses operating near full capacity.
* Detected slow-moving and dead stock requiring corrective action.
* Compared inventory value across different product categories.
* Evaluated supplier distribution and warehouse performance.
* Highlighted products requiring immediate replenishment.



