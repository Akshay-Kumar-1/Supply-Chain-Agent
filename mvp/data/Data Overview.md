# Project Data Overview: Inventory & Supply Chain Analysis

This document outlines the structure and key scenarios embedded within the five input data files designed for agent analysis.
These files are cross-referenced via consistent **SKU IDs**, **Supplier IDs**, and **PO IDs** to allow for seamless data joining and complex relational analysis.

---

## 1. Inventory Master
**Scope:** 50 SKUs across 3 Warehouses and 5 Categories.

This file contains deliberately planted scenarios to test stock optimization and risk assessment:
* **Active Stockouts:** SKU-018, SKU-032, and SKU-044.
* **Safety Stock Violations:** 5 critical items are currently below safety stock levels.
* **Overstock Issues:** 5 items identified as overstocked (some exceeding $10\times$ monthly demand).
* **Supply Chain Risk:** 13 items with single-source dependency risks.
* **Perishability:** Specific items include shelf-life tracking requirements.

---

## 2. Sales History
**Scope:** 12 weeks of historical demand for 10 key SKUs.

The data reflects distinct demand patterns to test forecasting capabilities:
* **Strong Upward Trend:** SKU-001 (+45% growth over 12 weeks).
* **Accelerating Growth:** SKU-012 (+163% growth).
* **Spike Pattern:** SKU-005 shows irregular demand spikes.
* **Stable Demand:** SKU-002 and SKU-008.
* **Flat/Stagnant:** SKU-006 (confirming its status as overstock).

---

## 3. Supplier Master
**Scope:** 10 Suppliers.

This file highlights procurement risks and contractual obligations:
* **Underperforming Suppliers:** * **SUP-002:** OTD (On-Time Delivery) declining from 89% to 78% with rising defect rates.
    * **SUP-006:** 72% OTD with a failed audit status.
* **Contractual Risks:** * **SUP-007:** Contract expiring this month.
    * **SUP-004:** Contract expiring next month.
* **Geographic Concentration:** Risk identified with 2 suppliers in China and 1 in Taiwan.
* **Dependency Risk:** SUP-009 is the single source for 5 different SKUs.

---

## 4. Purchase Orders (POs)
**Scope:** 25 Open/Historical Purchase Orders.

Key performance indicators and bottlenecks included:
* **Financial Impact:** 4 overdue POs representing ₹4.48L in stuck capital.
* **Urgency:** 6 open POs marked with "Critical" urgency.
* **Delay Patterns:** * **SUP-006** is responsible for the most severe delays.
    * **SUP-002** shows a consistent pattern of late deliveries.

---

## 5. Shipments Tracking
**Scope:** 18 Shipments in transit/delivered.

Provides granular visibility into the final mile and carrier reliability:
* **Status Distribution:** * 5 On-track.
    * 4 Delayed in transit.
    * 1 Not yet shipped.
* **Carrier Performance:** * **DHL:** 0% on-time delivery rate.
    * **Delhivery:** 75% on-time delivery rate.
* **Critical Linkage:** 5 shipments are directly linked to items currently at stockout risk.

---

### Data Integrity Note
All files are designed for relational joins. Ensure that agents map the following keys across the dataset:
* `SKU_ID` (Inventory $\leftrightarrow$ Sales $\leftrightarrow$ POs)
* `Supplier_ID` (Supplier Master $\leftrightarrow$ POs)
* `PO_ID` (POs $\leftrightarrow$ Shipments)

Would you like me to generate a sample Python script that joins these files and flags the SKU-018, SKU-032, and SKU-044 stockouts against their respective incoming shipments?
