# 📦 SupplyChain Agent — AI-Powered Supply Chain Co-Pilot

This document serves as the central repository for the **Planning & Requirements** phase of the SupplyChain Agent project. It consolidates the PRD, User Stories, Prioritization, Roadmap, and Technical Feasibility into a single, comprehensive guide.

**Directory:** `/planning-and-requirements/`

-----

## 📑 Table of Contents

1.  [Product Requirements Document (PRD)](https://www.google.com/search?q=%231-product-requirements-document-prd)
2.  [User Stories](https://www.google.com/search?q=%232-user-stories)
3.  [Prioritization Matrix](https://www.google.com/search?q=%233-prioritization-matrix)
4.  [Product Roadmap (Now/Next/Later)](https://www.google.com/search?q=%234-product-roadmap)
5.  [Success Metrics & KPIs](https://www.google.com/search?q=%235-success-metrics--kpis)
6.  [Technical Feasibility Notes](https://www.google.com/search?q=%236-technical-feasibility-notes)
7.  [Dependency Map](https://www.google.com/search?q=%237-dependency-map)

-----

## 1\. Product Requirements Document (PRD)

### Document Info

| Field | Value |
| :--- | :--- |
| **Product** | SupplyChain Agent MVP |
| **Version** | 1.0 |
| **Date** | 2026-04-07 |
| **Status** | Draft |

### 1.1 Problem Statement

SMBs (50-500 employees) lose 5-15% revenue to stockouts and 20-30% in carrying costs due to disconnected spreadsheets and reactive processes. No affordable AI solution exists to bridge this gap.

### 1.2 Product Overview

A co-pilot that ingests Excel/PDF data, reasons via Claude (LLM), and executes workflows in n8n to deliver proactive alerts via Google Sheets, Email, and Slack.

### 1.3 Goals & Success Metrics

  * **Primary Goals:** Reduce stockouts by 50%, save 10+ hours/week per user, NPS \> 30.
  * **Success Metrics:** Forecast accuracy (MAPE) \< 25%, Alert lead time \> 3 days.

### 1.4 Scope

  * **In Scope:** 7 agent modules (n8n), Excel/CSV input, PDF extraction, Google Sheets storage, Human-in-the-loop approvals.
  * **Out of Scope:** Custom web UI, direct ERP APIs, real-time streaming, mobile app.

### 1.5 Functional Requirements (Highlights)

  * **FR-01 Data Ingestion:** Accept .xlsx/.csv, extract PDF text, read/write Google Sheets.
  * **FR-02 Demand Forecasting:** 4-week forecasts with confidence levels and anomaly detection.
  * **FR-03 Inventory Optimization:** Dynamic reorder points, health classification, and dead stock detection.
  * **FR-04 Supplier Management:** Composite scoring (Quality/Delivery/Cost) and risk flagging.
  * **FR-05 Logistics Monitoring:** Shipment tracking and delay impact assessment.
  * **FR-06 Risk & Disruption:** External risk scanning and mitigation recommendations.
  * **FR-07 Procurement:** Auto-generate PO drafts, human-in-the-loop email approval.
  * **FR-08 Communication:** Persona-specific daily briefings and critical alert routing.

### 1.6 Non-Functional Requirements

  * **Performance:** Workflows \< 5 mins, LLM response \< 30s.
  * **Privacy:** No customer data stored outside Google Sheets/n8n; no PII in LLM calls.
  * **Scalability:** 100-500 SKUs, 10-50 suppliers.

-----

## 2\. User Stories

### EPIC-01: Demand Forecasting

  * **US-01.1 Weekly Forecast:** Automatic 4-week forecast per SKU every Monday.
  * **US-01.2 Anomaly Detection:** Flag deviations \> 20% from trend.
  * **US-01.3 What-If Scenarios:** LLM-powered scenario queries (e.g., "Impact of 20% discount?").

### EPIC-02: Inventory Optimization

  * **US-02.1 Daily Health Check:** Classify SKUs (Critical, Low, Healthy, Overstock) at 7 AM.
  * **US-02.2 Reorder Recommendations:** Calculate quantity based on forecast and lead time.
  * **US-02.3 Dead Stock Detection:** Identify items with zero sales in 60 days.
  * **US-02.4 Warehouse Transfers:** Suggest movement from overstocked to low-stock locations.

### EPIC-03: Supplier Management

  * **US-03.1 Scorecards:** Weekly 0-100 scores based on OTD, Quality, and Price.
  * **US-03.2 Risk Alerts:** Alert on \>15% performance drops or single-source dependency.
  * **US-03.3 PDF Extraction:** Extract data from quality reports and contracts.

### EPIC-04: Logistics Monitoring

  * **US-04.1 Unified Dashboard:** Status tracking (On Track, At Risk, Overdue).
  * **US-04.2 Delay Impact:** Cross-reference delayed shipments with inventory stockout risk.
  * **US-04.3 Exception Alerts:** Immediate alerts for high-priority delays.

### EPIC-05: Risk & Disruption

  * **US-05.1 Daily Risk Scan:** Scan for disasters, geopolitics, and port congestion at 6 AM.
  * **US-05.2 Risk Mapping:** Link external risks to specific SKUs and revenue.
  * **US-05.3 Mitigation:** Specific steps (e.g., "Activate backup Supplier Y").
  * **US-05.4 Executive Briefing:** \< 200-word daily summary for VP Operations.

### EPIC-06: Procurement Automation

  * **US-06.1 Auto-PO Generation:** Draft POs when stock hits Critical/Low.
  * **US-06.2 Email Approval:** One-click approve/reject via webhook links.
  * **US-06.3 Supplier Comms:** Auto-send professional PO emails to vendors.
  * **US-06.4 Lifecycle Tracking:** Monitor PO status (Sent, Confirmed, In Transit).

### EPIC-07: Communication & Coordination

  * **US-07.1 Persona Briefings:** Tailored EOD summaries for SCM, Procurement, and Logistics.
  * **US-07.2 Critical Routing:** Immediate Slack/Email routing for high-severity issues.
  * **US-07.3 Decision Audit Trail:** Log every agent action and reasoning in Google Sheets.

-----

## 3\. Prioritization Matrix

### RICE Scoring & MoSCoW

| Epic | RICE Score | MoSCoW |
| :--- | :--- | :--- |
| **EP-02: Inventory Optimization** | 54.0 | **Must Have** |
| **EP-07: Communication & Briefings** | 63.8 | **Must Have** |
| **EP-06: Procurement Automation** | 29.8 | **Must Have** |
| **EP-01: Demand Forecasting** | 22.4 | Should Have |
| **EP-03: Supplier Management** | 19.2 | Should Have |
| **EP-04: Logistics Monitoring** | 20.0 | Could Have |
| **EP-05: Risk & Disruption** | 17.3 | Could Have |

**Build Sequence:**

1.  **Weeks 1-2:** Data Model + Inventory + Communication (First Demo).
2.  **Week 3:** Procurement Agent (Second Demo).
3.  **Week 4:** Demand Forecasting + Supplier Management.
4.  **Week 5:** Logistics + Risk Monitoring.

-----

## 4\. Product Roadmap

### NOW (Q2 2026): MVP Build & Beta

  * **Deliver:** 7 n8n workflows, 5 Excel templates, Persona briefings, Slack integration.
  * **Milestones:** Week 4 full pipeline demo; Week 5 beta onboarding.

### NEXT (Q3 2026): Validation & Growth

  * **Deliver:** Prophet statistical models, PDF auto-ingestion via email, Looker Studio dashboards.
  * **Goal:** 50 paying customers.

### LATER (Q4 2026+): Platform Evolution

  * **Deliver:** Migration to PostgreSQL, FastAPI backend, React Dashboard, Direct ERP integrations (Odoo, Zoho).

-----

## 5\. Success Metrics & KPIs

| Category | KPI | Target |
| :--- | :--- | :--- |
| **Product Health** | WAU | 60% of registered users |
| **Product Health** | Workflow Success Rate | \> 95% |
| **Business Impact** | Stockout Reduction | 50% in 3 months |
| **Business Impact** | Time Saved | 10+ hours/week |
| **Business Impact** | Forecast MAPE | \< 25% |
| **Business (Our Side)** | MRR | $10,000 (at 6 months) |

-----

## 6\. Technical Feasibility Notes

  * **Orchestration (n8n):** **High Feasibility.** Supports all nodes; use webhook chaining for agent-to-agent talk.
  * **Reasoning (Claude):** **High Feasibility.** Sonnet model for structured JSON; context window \> 200K.
  * **Storage (Google Sheets):** **Medium-High Feasibility.** Limits at 10M cells; mitigation: monthly archiving.
  * **Performance Budget:** Total daily pipeline should complete in \< 30 minutes (\~20 LLM calls).

-----

## 7\. Dependency Map

### Build Order & Internal Flow

```text
Data Templates (Foundation)
    │
    ├── Demand Forecasting ──────────────┐
    │                                    │
    ├── Inventory Optimization ◄─────────┘
    │       │
    │       ├── Procurement Agent ◄── Supplier Management
    │       │       │
    │       │       └── Logistics Monitoring
    │       │
    │       └── Risk & Disruption (Reads from all)
    │
    └── Communication Agent (Build Last)
```

### Risk & Mitigation

  * **LLM Hallucination:** Mitigated by confidence scores and human-in-the-loop review.
  * **Data Quality:** Mitigated by strict validation nodes and quality scoring.
  * **API Limits:** Mitigated by batching and staggered workflow triggers.
